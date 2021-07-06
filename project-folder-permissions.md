When working on a project with others, you need to provide access to the project folder
for all collaborators, but possibly not for others. This requires an understanding of
Unix file permissions.

* TOC
{:toc}

## Unix file permissions

Unix file permissions are based on three types of
permissions (read, write and execute permissions) for three types of users (the
owner, the group and others; see
[linuxcommand.org](https://linuxcommand.org/lc3_lts0090.php), [Stackexchange](https://unix.stackexchange.com/questions/21251/execute-vs-read-bit-how-do-directory-permissions-in-linux-work) and the links
below). Every file/directory is owned by one user and one group. Every user belongs to a primary group, which determines the group
ownership of files/folders created by this user, and secondary groups, which
determines the permissions the user has on files/folders owned by these groups.
Additional noteworthy flags:

- Setgid ("set group ID"): When set on a directory, new files and subdirectories created within
  it inherit its group ID, rather than the primary group ID of the user who
  created the file ([Wikipedia](https://en.wikipedia.org/wiki/Setuid))
- Sticky bit: When set on a directory, files in that directory may only be
  deleted or renamed by the directory owner or the file owner
  ([Wikipedia](https://en.wikipedia.org/wiki/Sticky_bit)). This is relevant,
  because otherwise users with write/execute permissions on the directory can delete files
  in this directory
  ([Stackexchange](https://unix.stackexchange.com/questions/48579/why-can-rm-remove-read-only-files))
  
Some useful commands are:

- `chown` - change file owner and group
- `chmod` - change file permissions
- `chgrp` - change group ownership
- `id <username>` - view user groups (a similar command is `groups`)
- `getent group <groupname>` - view group members

## Access control lists (ACL)

Access-Control Lists, or ACL, provide an additional flexible mechanism for fine-grained permissions
control
([geeksforgeeks.org](https://www.geeksforgeeks.org/access-control-listsacl-linux/),
[bytexd.com](https://bytexd.com/intro-to-acl-using-getfacl-setfacl-commands/)).
Relevant commands:

- `setfacl` - set file access control lists
- `getfacl` - get file access control lists

## Creating a project directory

An easy way to make the project folder writeable for your
collaborators is to modify the group permissions.

- Create the project folder in the directory`/proj`: `mkdir
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

In case the project folder should only be accessible by you and your collaborators:

- Ask the server administrator to create a new Linux group for you and your
  collaborators (please provide the user names). The administrator will set the group ownership of the
  project directory to this group, and only these users (the
  members of the newly created group) will have reading and writing
  permissions on the project directory. (The owner can later modify the permissions
  for "group" and "others", if required, also by using `setfacl` to make
  newly created files/directories group-writeable by default.)
- Alternatively, the directory owner can limit the permissions for "group" and "others", and
  set permissions for single users using `setfacl`
  ([askubuntu.com](https://askubuntu.com/a/809562)). This can be done without the server administrator.

## Jupyter

In case you are using Jupyter:

- The file explorer in Jupyter uses your home folder as root folder, therefore it
  can't access the path `/proj/...` directly. However, you can simply create a
  symbolic link in your home folder to `/proj/<your-project>`

## Links

- File permissions:
  [linuxcommand.org](https://linuxcommand.org/lc3_lts0090.php),
  [wpollock.com](https://wpollock.com/AUnix1/FilePermissions.htm),
  [Wikipedia](https://en.wikipedia.org/wiki/File-system_permissions),
  [linux.com](https://www.linux.com/training-tutorials/understanding-linux-file-permissions/),
  [kb.iu.edu](https://kb.iu.edu/d/abdb),
  [wiki.archlinux.org](https://wiki.archlinux.org/title/File_permissions_and_attributes),
  [Wikipedia: Sticky bit](https://en.wikipedia.org/wiki/Sticky_bit)
- Related questions/answers:
  [Stackexchange](https://unix.stackexchange.com/questions/1314/how-to-set-default-file-permissions-for-all-folders-files-in-a-directory),
  [Stackexchange](https://unix.stackexchange.com/questions/12842/make-all-new-files-in-a-directory-accessible-to-a-group),
  [Stackoverflow](https://stackoverflow.com/questions/1321168/bash-scripting-how-to-set-the-group-that-new-files-will-be-created-with), [askubuntu.com](https://askubuntu.com/questions/487527/give-specific-user-permission-to-write-to-a-folder-using-w-notation)
  [askubuntu.com](https://askubuntu.com/questions/402980/give-user-write-access-to-folder),
  [superuser.com](https://superuser.com/questions/235297/allow-specific-user-permission-to-read-write-my-folder),
  [serverfault.com](https://serverfault.com/questions/347589/who-can-delete-a-file),
  [Stackoverflow](https://stackoverflow.com/questions/3740152/how-to-change-permissions-for-a-folder-and-its-subfolders-files-in-one-step)
- Groups:
  [networkworld.com](https://www.networkworld.com/article/3409781/mastering-user-groups-on-linux.html),
  [linuxize.com](https://linuxize.com/post/how-to-list-groups-in-linux/),
  [askubuntu.com](https://askubuntu.com/questions/538130/what-is-the-difference-between-primary-group-and-secondary-group-in-ubuntu),
  [Stackexchange](https://unix.stackexchange.com/questions/274200/primary-and-secondary-groups),
  [askubuntu.com](https://askubuntu.com/a/589308)