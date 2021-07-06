When working on a project with others, you need a project folder
to which the collaborators have access. To learn more about file
permissions, see e.g.
[linuxcommand.org](https://linuxcommand.org/lc3_lts0090.php) and the links below.
You can view a user's primary group and secondary groups using the `id` command.

If you trust other members of your primary group (they may view the files, and you don't
expect anybody to delete the files), an easy way to make the project folder writeable for your
collaborators is to modify the group permissions.

- Create the project folder in the directory`/proj`: `mkdir
  /proj/<your-project>`. You should select a name that clearly identifies
  your project. It can be helpful to prepend the year, e.g.
  `2021-LochNess-amplicons` (if you are working on amplicons from Loch Ness)
- Add group writing permissions: `chmod g+w /proj/<your-project>`
- Newly created folders inside `<your-project>` will by default be writeable by
  the folder owner, but not by others. You can change the permissions manually
  after creating folders (as above), or you can set the default permissions for newly
  created folders. To change the default permissions, execute this command on
  your project directory: `setfacl -d -m g::rwx /proj/<your-project>`. After this,
  newly created folders will have group writing permissions by default. (Check with `getfacl
  /proj/<your-project>`)

In case the project folder should only be accessible by you and your collaborators:

- Ask the server administrator to create a new Linux group for you and your
  collaborators (please provide the user names). Only these users will be
  granted reading and writing permissions on the project folder.

In case you are using Jupyter:

- The file explorer in Jupyter uses your home folder as root folder, therefore it
  can't access the path `/proj/...` directly. However, you can simply create a
  symbolic link in your home folder to `/proj/<your-project>`

Links:

- File permissions:
  [linuxcommand.org](https://linuxcommand.org/lc3_lts0090.php),
  [Wikipedia](https://en.wikipedia.org/wiki/File-system_permissions),
  [kb.iu.edu](https://kb.iu.edu/d/abdb),
  [wiki.archlinux.org](https://wiki.archlinux.org/title/File_permissions_and_attributes),
  [networkworld.com](https://www.networkworld.com/article/3409781/mastering-user-groups-on-linux.html)
- ACLs:
  [bytexd.com](https://bytexd.com/intro-to-acl-using-getfacl-setfacl-commands/)
- Related questions/answers:
  [Stackexchange](https://unix.stackexchange.com/questions/1314/how-to-set-default-file-permissions-for-all-folders-files-in-a-directory),
  [Stackexchange](https://unix.stackexchange.com/questions/12842/make-all-new-files-in-a-directory-accessible-to-a-group),
  [Stackoverflow](https://stackoverflow.com/questions/1321168/bash-scripting-how-to-set-the-group-that-new-files-will-be-created-with), [askubuntu.com](https://askubuntu.com/questions/487527/give-specific-user-permission-to-write-to-a-folder-using-w-notation)
  [askubuntu.com](https://askubuntu.com/questions/402980/give-user-write-access-to-folder),
  [superuser.com](https://superuser.com/questions/235297/allow-specific-user-permission-to-read-write-my-folder)