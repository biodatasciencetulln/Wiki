When working on a project with others, you need to provide access to the project directory
for your collaborators, but possibly not for other people. This requires an understanding of
Unix file permissions.

* TOC
{:toc}

## Unix file permissions

Unix file permissions are based on three types of
permissions (read, write and execute permissions) for three types of users (the
owner, the group and others); see
[linuxcommand.org](https://linuxcommand.org/lc3_lts0090.php), and the links
below. Every file/directory is owned by one user and one group. Every user belongs to a primary group, which determines the group
ownership of files/directories created by this user, and secondary groups, which
determines the permissions the user has on files/directories owned by these
groups. The meaning of the permission bits differs for regular files and
directories
([Stackexchange](https://unix.stackexchange.com/questions/21251/execute-vs-read-bit-how-do-directory-permissions-in-linux-work)).
Additional noteworthy flags:

- Setgid ("set group ID"): When set on a directory, new files and subdirectories created within
  it inherit its group ID, rather than the primary group ID of the user who
  created the file ([Wikipedia](https://en.wikipedia.org/wiki/Setuid))
- Sticky bit ('restricted deletion flag'): When set on a directory, files in
  that directory may only be deleted or renamed by the directory owner or the
  file owner ([Wikipedia](https://en.wikipedia.org/wiki/Sticky_bit)). Such a
  directory displays a 't' in the last position (e.g. `drwxr-xr-t`) This is
  relevant, because otherwise users with write/execute permissions on the
  directory can delete files in this directory
  ([Stackexchange](https://unix.stackexchange.com/questions/48579/why-can-rm-remove-read-only-files))
  
Useful commands and examples:

- `chown` - change file owner and group
- `chmod` - change file permissions
  - `chmod -R g+w <directory>` - add group writing permissions (recurse into directories)
  - `chmod g+s <directory>` - set setgid bit on directory
  - `find <directory> -type d -exec chmod g+s '{}' \;` - set setgid bit
      on existing subdirectories
  - `find <directory> -type d -exec chmod 755 {} \;` - set directory and subdirectories to 755 (`drwxr-xr-x`)
  - `find <directory> -type f -exec chmod 644 {} \;` - set files in
    directory and subdirectories to 644 (`-rw-r--r--`)
- `chgrp` - change group ownership
  - `chgrp -R <groupname> <directory>` - change group ownership (recurse
    into directories)
- `id <username>` - view user groups (a similar command is `groups`)
- `getent group <groupname>` - view group members
- `stat` - display file or file system status
- `newgrp <groupname>` - change the current group ID
- `sg <groupname> <command>` - execute a command (or set of commands)
  with changed group ID

## Access control lists (ACL)

Access-Control Lists, or ACL, provide an additional flexible mechanism for fine-grained permission
control
([geeksforgeeks.org](https://www.geeksforgeeks.org/access-control-listsacl-linux/),
[bytexd.com](https://bytexd.com/intro-to-acl-using-getfacl-setfacl-commands/)).
Relevant commands:

- `setfacl` - set file access control lists
  - `setfacl -d -m g::rwX <directory>` - set default ACL for the group
    ("X" sets execute permission on directories, but not on files; see
    [computerhope.com](https://www.computerhope.com/unix/usetfacl.htm),
    [ubuntu.com](http://manpages.ubuntu.com/manpages/impish/en/man1/setfacl.1.html))
  - `setfacl -d -m o::rx <directory>` - set default ACL for others
  - `setfacl -m group:<groupname>:rwx <directory>` - set ACL for the group (on
    existing files)
  - `setfacl -m u:<username>:rwx <directory>` - set permissions for specific user
- `getfacl` - get file access control lists

## Creating a project directory

An easy way to make the project directory writeable for your
collaborators is to modify the group permissions.

- Create the project folder in the `/proj` directory: `mkdir
  /proj/<your-project>`. You should select a name that clearly identifies
  your project. It can be helpful to prepend the year, e.g.
  `2021-LochNess-amplicons` (if you are working on amplicons from Loch Ness).
- Add group writing permissions: `chmod g+w /proj/<your-project>`
- Newly created directories inside `<your-project>` will by default be writeable by
  the owner, but not by others. You can change the permissions manually
  after creating directories (as above), or you can set the default permissions for newly
  created files/directories. To change the default permissions, execute this command on
  your project directory: `setfacl -d -m g::rwx /proj/<your-project>`. After this,
  newly created files/directories will have group writing permissions by default. (Check with `getfacl
  /proj/<your-project>`)

In case the project directory should only be accessible by you and your collaborators:

- Ask the server administrator to create a dedicated Unix group for the project, with
  you and your collaborators as members (please provide the user names). The
  administrator will give the group ownership of the project directory, give
  it writing permissions and set the setgid bit, so that newly created files/directories
  inherit the group ID. The owner can later modify the permissions for
  "group" and "others", e.g. restrict the access for "others", or use `setfacl`
  to make newly created files/directories group-writeable by default.
- Alternatively, the directory owner can restrict access for "group" and "others", and
  set permissions for single users using `setfacl`
  ([askubuntu.com](https://askubuntu.com/a/809562)). As this doesn't involve
  creating new groups, it can be done without the server administrator.

## Jupyter

In case you are using Jupyter:

- The file explorer in Jupyter uses your home directory as root directory, therefore it
  can't access the path `/proj/...` directly. However, you can simply create a
  symbolic link to `/proj/<your-project>` in your home directory.

## Links

- File permissions:
  [wpollock.com](https://wpollock.com/AUnix1/FilePermissions.htm),
  [linux.com](https://www.linux.com/training-tutorials/understanding-linux-file-permissions/),
  [kb.iu.edu](https://kb.iu.edu/d/abdb),
  [Wikipedia](https://en.wikipedia.org/wiki/File-system_permissions),
  [wiki.archlinux.org](https://wiki.archlinux.org/title/File_permissions_and_attributes)
- Related questions/answers:
  [Stackexchange](https://unix.stackexchange.com/questions/12842/make-all-new-files-in-a-directory-accessible-to-a-group),
  [askubuntu.com](https://askubuntu.com/questions/487527/give-specific-user-permission-to-write-to-a-folder-using-w-notation),
  [askubuntu.com](https://askubuntu.com/questions/402980/give-user-write-access-to-folder)
- Groups:
  [networkworld.com](https://www.networkworld.com/article/3409781/mastering-user-groups-on-linux.html),
  [linuxize.com](https://linuxize.com/post/how-to-list-groups-in-linux/),
  [askubuntu.com](https://askubuntu.com/questions/538130/what-is-the-difference-between-primary-group-and-secondary-group-in-ubuntu),
  [Stackexchange](https://unix.stackexchange.com/questions/274200/primary-and-secondary-groups),
  [askubuntu.com](https://askubuntu.com/a/589308)
