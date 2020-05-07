<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<H1>Guide for installing Ubuntu in VirtualBox</H1>

* TOC
{:toc}

### Install VirtualBox on your computer

- Download and install [Oracle VirtualBox](https://www.virtualbox.org/)
  - General note: During all steps of the tutorial, you might encounter problems of some sort. As we are using well-known and popular software like VirtualBox or Ubuntu, those problems have usually been discussed online and there is some solution available. An internet search for your particular problem based on the most important keywords can help find these discussions and the solution
  - E.g., if installation on MacOS fails, you can search for "virtualbox macos installation failed" and find links like [osxdaily.com](http://osxdaily.com/2018/12/31/install-run-virtualbox-macos-install-kernel-fails/) or [medium.com](https://medium.com/@DMeechan/fixing-the-installation-failed-virtualbox-error-on-mac-high-sierra-7c421362b5b5), which say that this can be related to a MacOS security feature (Gatekeeper) and explain how to fix it
- Run VirtualBox and install the Extension Pack

---
## Download the Linux iso file (disc image)

- Recommended Linux distribution is the latest [Xubuntu](https://en.wikipedia.org/wiki/Xubuntu). You can download the iso file from the [official download page](https://xubuntu.org/download/). The downloaded file should have a name like `xubuntu-<version>-desktop-amd64.iso` (for an explanation what "amd64" means, see e.g. [askubuntu.com](https://askubuntu.com/a/67468/))
- Xubuntu is Ubuntu but with a different [Desktop environment](https://www.lifewire.com/linux-desktop-environment-explained-4121640) ([more info](https://wiki.archlinux.org/index.php/Desktop_environment)), called [Xfce](https://en.wikipedia.org/wiki/Xfce). It has a different selection of pre-installed software, requires less resources and is generally more responsive than the default GNOME desktop environment 

---
## Create a new Virtual Machine (VM) in VirtualBox

- VirtualBox → "New"
- Enter `Name`: e.g. `Xubuntu`
- Make sure that `Type` is `Linux`
- Make sure that `Version` is `Ubuntu (64 bit)`
  - Note: if the option `Ubuntu (64 bit)` is not available, you probably need to activate a **BIOS setting** for virtualization. Reboot your computer into BIOS/UEFI and enable hardware virtualization. This will appear as `Virtualization Technology` and/or `VT-x or AMD-V` or similar (different manufacturers word it differently). You can consult e.g. the following links for instructions and troubleshooting: [forums.virtualbox.org](https://forums.virtualbox.org/viewtopic.php?f=1&t=62339), [superuser.com](https://superuser.com/questions/1241956/virtualbox-only-allowing-32-bit-os), [docs.fedoraproject.org](https://docs.fedoraproject.org/en-US/Fedora/13/html/Virtualization_Guide/sect-Virtualization-Troubleshooting-Enabling_Intel_VT_and_AMD_V_virtualization_hardware_extensions_in_BIOS.html), [howtogeek.com](https://www.howtogeek.com/213795/how-to-enable-intel-vt-x-in-your-computers-bios-or-uefi-firmware/)
  - If you have multiple BIOS options related to virtualization, e.g. `VTx` and `VTd`, you probably should enable both
- Most other settings: the defaults are ok
- Memory: at least 4 GB is recommended (can be changed later)
- Virtual hard disk size: 30-50 GB are recommended (less might be not enough; can't be changed later)
- Your new VM is saved as a folder with a few files in it (on Windows, it should be located in the folder "C:\Users\your-user\VirtualBox VMs")
- The VM is essentially a simulated computer, with a hard drive (currently empty), an optical disc drive (where you can "insert" a disc/disc image), and simulated audio/graphics hardware

---
## Install the guest OS (operating system)

- The operating system (OS) that runs on your computer is called **host**, the OS in the VM is called **guest**
- In VirtualBox: Select the VM → "Start"
- It should ask you for a disc (the hard drive is empty, so it is looking for a bootable disc) → select the iso file
- Boot the OS (this is called [live OS](https://en.wikipedia.org/wiki/Live_CD) because it's booted directly from the disc/iso file, without being installed on the hard drive)
  - If there is an error message like "Hardware acceleration is not available on your system" when trying to install or launch a VM, try to search for "virtualbox error" + error message text. It's possible that this error occurred because virtualization wasn't activated in your computer's BIOS/UEFI, and should be easy to fix
- There should be an option to install the OS; start the installer and follow the installation instructions
  - Please select English as your installation language; additional languages can be added later
  - Pay attention that the settings are correct, e.g. the keyboard layout should correspond to your keyboard (e.g., if you have a German keyboard, you should select a German keyboard layout)
  - If there are checkboxes like "Download updates while installing" and "Install this third-party software", check them
  - The option "Erase disk and install Xubuntu" is fine, because you are using a virtual hard drive which should not have any partitions anyway
- The guest OS is now being installed within the VM
- After the installation is complete: reboot the VM
  - You might need to remove the disc image from the optical drive first (to make sure that the VM boots from the hard drive and not from the disc image): VirtualBox → Select the VM → Settings → Storage → Select optical disc → Look for option "Remove Disc from Virtual Drive"

---
## Linux basics (general information)

- This is how you [open a terminal](https://docs.xubuntu.org/1910/user/C/command-line.html): Application menu → Accessories → Terminal emulator (it's called "emulator" for [historical reasons](https://superuser.com/a/930427))
- This is how you start programs/run commands: type the name of the program/command in the terminal and hit Enter
- **Abort program/command** running in the terminal: press **Strg-C** (this key combination sends the "SIGINT" (interrupt) signal to a running process)
- **Abort non-responsive graphical application**: enter `xkill` in the terminal and click on the non-responsive application
  - only use this if absolutely necessary
- Get previously entered command using up/down keys
  - e.g. enter `ls` + Enter → "list" the directory contents
  - press the "arrow up" key → it brings up the previously entered `ls` command
- **Search** for previously entered commands using **Strg-R**
- When you interact with the terminal, you should always **read the output/error messages**. You might be used from Windows that, whenever a message appears, you click "Cancel" or "Continue" to make it go away; this is different in Linux. The messages are usually informative and let you know what's happening and if there are any problems. E.g., if you run a command, and the terminal says "Building modules...", then it's building modules, and you have to wait. If it says "Successfully installed", then the package was successfully installed. If the message says "Failed to fetch http://some/web/url", then it failed to fetch this address, possibly because the url wasn't valid or there was no internet connection. If the command didn't complete successfully, try to search for the respective error message, which can help to find a solution

---
## Update the guest and install the guest additions

- **Update** the Ubuntu guest: Open a terminal, type `sudo apt update && sudo apt upgrade` and press Enter
  - `sudo` (*superuser do*) grants admin rights and is required for all system-relevant tasks
  - `apt` is [the command](https://askubuntu.com/questions/155538/what-is-apt-and-aptitude-in-ubuntu) that manages installing/removing/updating most software on Ubuntu (actually Debian, which Ubuntu is based on)
  - `update`/`upgrade` are **arguments** that modify the command behavior (tell the command what to do):
    - the subcommand `apt update` is used to download package information from all configured sources
    - `apt upgrade` operates on this data to to actually install the updated package versions
  - `&&` is an **operator** that can be used to connect commands; it executes the second command [only if](https://unix.stackexchange.com/a/24685) the first one completed successfully. You could also execute `apt update` and `apt upgrade` one after the other, with the same effect
  - This might take a while and should update all installed software ("packages") to their latest versions
- The [guest additions](https://www.virtualbox.org/manual/ch04.html) is additional software that improves the integration of the guest with the host, e.g. it enables the auto-resizing of the OS in the VirtualBox window
- The guest additions can be installed from the (virtual) **"Guest Additions disc image"** that comes with VirtualBox:
  - You might need some additional packages like "build-essential" (unless already installed): `sudo apt install build-essential`
  - In the VM window menu bar: Devices → Insert Guest Additions CD image...
  - In the guest, the disc should be now accessible under _/media/your-username/VBox_GAs_x.y.z/_ (x, y, z are version numbers)
  - You probably can't use the file manager to install it (even though you can view the files), because the execution of _VBoxLinuxAdditions.run_ requires root permissions; so you have to use the terminal:
    - Use the `ls` (*list*) command to look at directory contents:
    `ls /media/your-username` (press **Tab** once or twice to auto-complete paths, e.g. you can write `ls /me<Tab>/<Tab><Tab>`) → should list files/folders in the directory _/media/your-username_
    - Enter the directory using the `cd` (*change directory*) command:
    `cd /media/your-username/VBox_GAs_6.0.10/`
    - Install the guest additions package by running the installation script:
    `sudo ./VBoxLinuxAdditions.run`
- On the internet, you might read that guest additions can (or should) be installed from the repository (an app store/software collection specific to a Linux distribution), using a command like `sudo apt install virtualbox-guest-x11 virtualbox-guest-utils virtualbox-guest-dkms`
  - It's usually easier to install software from the repository, but for guest additions it might not work very well (e.g., for me, the shared clipboard wouldn't work after installation)
  - General info on software installation: [help.ubuntu.com](https://help.ubuntu.com/community/SoftwareManagement)
  - Xubuntu [software installation](https://docs.xubuntu.org/1910/user/C/managing-applications.html): Start menu → Software, Start menu → Settings Manager → Software & Updates

---
## Some useful VirtualBox options

- **Shared clipboard** (very useful): VM → Settings → General → Advanced → Shared Clipboard: Bidirectional
- Drag'n'Drop: VM → Settings → General → Advanced → Drag'n'Drop: Bidirectional

### Share a folder between the host and the guest

- A **shared folder** offers a way of passing files between the guest and the host systems. If you save your files in the shared folder, you can delete the VM itself at any time without loosing your data
- In the guest, you need to add your user to a group that can access shared folders. In the terminal:
`sudo adduser your-username vboxsf`
  - After this, you need to log out from the guest and then log in again
- In VirtualBox, select your VM → Settings → Shared Folders → Add shared folder: select the folder you want to share
  - check the checkboxes Auto-mount and Make Permanent
- In the guest, the shared folder should now be accessible under /media/sf_shared-folder-name/ and visible in the file manager
  - try to create a text file in this folder and access it from your host, or the other way around
- Consult e.g. [websiteforstudents.com](https://websiteforstudents.com/access-virtualbox-host-folders-from-ubuntu-17-10-guest-machines/) for troubleshooting

---
## Troubleshooting

- Problems can be related to the guest (and need to be addressed within the guest), or to the host/VirtualBox, and addressed e.g. by changing VirtualBox settings (usually a shutdown of the guest is required)
- Graphics issues (like displaying errors or freezes):
  - Host: VM → Settings → Display → **Video Memory**: Increase to 128 MB (shut down the guest first)
  - Host: VM → Settings → Display: Try checking/unchecking "Enable 3D acceleration" (should probably be unchecked)
  - Host: VM → Settings → Display → **Graphics Controller**: Try switching to VBoxSVGA or VBoxVGA
- Memory (system suddenly becomes very slow):
  - Host: VM → Settings → System → Base memory: Increase to at least ~3-4 GB
- Sound issues: 
  - Host: VM → Settings → Audio → **Audio Controller**, try to switch between AC97 and Intel HD Audio
  - Guest: Applications → Sound & Video → PulseAudio Volume Control, try to change some settings
  - Still sound issues: well, that's annoying. (There might be a solution, but it can be difficult to find, or you might need to wait for updates. This also explains why Linux hasn't become more popular than Windows or MacOS :) 
- Some media can't be played: install the package `ubuntu-restricted-extras` with additional media codecs and fonts ([help.ubuntu.com](https://help.ubuntu.com/community/RestrictedFormats)):
  `sudo apt install ubuntu-restricted-extras`
- Other problems:
  - Try to determine in which situation the problem occurs, e.g. does rebooting the VM help?
  - Use a search engine to search for the problem online. Try to describe the problem as concise as possible. E.g., if the menu bar of the VirtualBox window has dis appeared, and you can't select Devices → Insert guest additions CD image, you can search for "virtualbox menu bar missing"; you will usually find blogs or forum discussions on how to fix the problem (like [askubuntu.com](https://askubuntu.com/questions/59103/why-has-virtualboxs-menu-disappeared))
- Running a **system monitor** at all times to keep track of the memory usage and CPU load is a good idea, and helps to diagnose problems
  - Guest: Use some type of [system monitor](http://www.linuxandubuntu.com/home/10-best-linux-task-managers) like gnome-system-monitor (you might need to install it first, `sudo apt install gnome-system-monitor`), or a similar program ([Conky](https://www.lifewire.com/beginners-guide-to-conky-4043352)).
  - Host: Use the Task Manager (Windows) or equivalent
  - High CPU load or memory usage can substantially slow down the system. If they are caused by a software problem, restarting the offending program can help
- Random freezes of the guest OS → try to modify these host VM settings:
  - Display → "Enable 3D acceleration" = off
  - System → Processor → Number of virtual CPUS: 1 processor → 2, 3 or 4 processors (try and see if this helps)
  - System → Processor → "Enable PAE/NX": toggle this off if it’s on, or on if it’s off, and see if this helps
  - Display → increase "Video memory" to 128 MB
  - System → Acceleration → Paravirtualization Interface: try "Minimal" or "Legacy"
  - Try a different (older) version of VirtualBox
- Still problems with the guest, like freezes, high CPU load for no reason, etc.: One possibility is to try another desktop environment; suggested options are LXQt, Xfce and MATE. There are others, but they are less performant. After the corresponding environment is installed, it can be selected in the "Session" field at login
- Guest system is generally slow: this shouldn't happen with Xubuntu, and is probably a host issue rather than a guest issue (e.g. not enough RAM, slow CPU, slow overall performance) 
- Advanced VirtualBox-related topics: e.g. [wiki.ubuntuusers.de](https://wiki.ubuntuusers.de/VirtualBox/Problembehebung/)
- General note: You will most probably encounter bugs in Linux; Linux was designed for system stability, transparency and production/development rather than a polished user experience
  - If the problem is Linux-related, also read the distribution [release notes](https://wiki.xubuntu.org/start?do=index) and check for known bugs and workarounds.

---
## Updates

- Guest: **Update regularly** using `sudo apt update && sudo apt upgrade` or the update dialogue
- Host:
  - Keep the OS updated
  - When updating VirtualBox, *completely shutdown the VM* before that
    - Major (e.g. Virtualbox 5 → 6) and even minor (e.g. VirtualBox 6.0 → 6.1) releases introduce new features and can therefore break things (in the worst case, you need to downgrade again)
    - Maintenance releases (e.g. VirtualBox 6.0.8 → 6.0.10) are bug fix releases and usually don't break things
    - If there are problems after a VirtualBox update (e.g. a VM that used to work suddenly doesn't start and you see strange error messages), try rebooting the computer, possibly twice

---
## Where to go from here

- **Back up** your VM. You can do it based on the instructions on [osradar.com](https://www.osradar.com/how-to-backup-vms-on-virtualbox/) and [lifewire.com](https://www.lifewire.com/create-virtual-machines-clones-and-snapshots-in-virtualbox-4177998), however I highly recommend to also completely shut down your VM and copy the complete VM-folder to an external hard drive. The VM-folder should be located in the folder "VirtualBox VMs" in your home directory. (More information on [virtualbox.org](https://forums.virtualbox.org/viewtopic.php?f=6&t=81581). If your VM is broken beyond repair and you have a functional backup, you can restore it from the backup. This is usually easier than performing an installation from scratch.
  - You can import it later like this: Machine → Add → Navigate to the _.vbox_ file in the VM folder ([superuser.com](https://superuser.com/questions/633431/whats-the-recommended-way-to-move-a-virtualbox-vm-to-another-computer), [superuser.com](https://superuser.com/questions/745844/how-can-i-import-an-existing-vbox-virtual-machine-in-virtualbox/746429))
- Customitize your Xubuntu installation [just for fun](https://itsfoss.com/customize-xfce/)
- Become comfortable with the command line early on. Even though tasks like software installation can be done via GUIs (graphical user interfaces), GUIs are usually "frontends" to command-line tools like `apt` that operate in the background. Linux GUIs can also be buggy, because neither users nor developers like them very much
- Check out some introductory Linux and [Bash tutorials](https://www.youtube.com/watch?v=oxuRxtrO2Ag), and learn the command line (e.g. [linuxcommand.org](linuxcommand.org))
- Navigate the filesystem using `pwd`, `ls` and `cd`
- Use manpages (`man ls`) or simplified manpages, [tldr.ostera.io](https://tldr.ostera.io/)
- Learn how to use a non-GUI text editor, [nano](https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/) or [vim](https://www.youtube.com/watch?v=ggSyF1SVFr4)
