<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>Guide for installing Ubuntu in VirtualBox</H1>

**Table of contents**

* TOC
{:toc}

There are numerous tutorials which guide you through the installation of Ubuntu on VirtualBox. This document tries to address some points not mentioned in these tutorials, and provide additional links and information. Possibly useful tutorials are:

- [YouTube tutorial](https://www.youtube.com/watch?v=sB_5fqiysi4)
- [itsfoss.com tutorial](https://itsfoss.com/install-linux-in-virtualbox/)
- [lifewire.com tutorial](https://www.lifewire.com/install-ubuntu-linux-windows-10-steps-2202108)
- [nakivo.com tutorial](https://www.nakivo.com/blog/install-ubuntu-on-virtualbox-virtual-machine/)

## Install VirtualBox on your computer

- Download and install [Oracle VirtualBox](https://www.virtualbox.org/)
  - Note: During all steps of the tutorial, you can encounter problems of some sort. For widely used software like VirtualBox and Ubuntu, these problems have usually been discussed online and a solution exists. A web search for your particular problem based on important keywords (e.g. the error message) can help
  - E.g., if installation on macOS fails, you can search for "virtualbox macos installation failed" and find links like [osxdaily.com](http://osxdaily.com/2018/12/31/install-run-virtualbox-macos-install-kernel-fails/) or [medium.com](https://medium.com/@DMeechan/fixing-the-installation-failed-virtualbox-error-on-mac-high-sierra-7c421362b5b5), which say that this can be related to a macOS security feature (Gatekeeper) and explain how to fix it
- Run VirtualBox and install the Extension Pack (additional Oracle proprietary components which extend the functionality of the base package)

---
## Download the Linux iso file (disk image)

- Recommended Linux distribution is the latest [Xubuntu](https://en.wikipedia.org/wiki/Xubuntu). You can download the iso file from the [official download page](https://xubuntu.org/download/). The downloaded file should have a name like `xubuntu-<version>-desktop-amd64.iso` (for an explanation what "amd64" means, see e.g. [askubuntu.com](https://askubuntu.com/a/67468/))
- Xubuntu is Ubuntu but with a different [Desktop environment](https://www.lifewire.com/linux-desktop-environment-explained-4121640) ([more info](https://wiki.archlinux.org/index.php/Desktop_environment)), called [Xfce](https://en.wikipedia.org/wiki/Xfce). It has a different selection of pre-installed software, requires less resources and is generally more responsive than the default GNOME desktop environment 
  - While there are differences between Ubuntu and Xubuntu, they are superficial, as Xubuntu *is* Ubuntu with a different look; therefore most Ubuntu-related tutorials apply to Xubuntu as well

---
## Create a new Virtual Machine (VM) in VirtualBox

- VirtualBox → "New"
- Enter `Name`: e.g. `Xubuntu`
- Make sure that `Type` is `Linux`
- Make sure that `Version` is `Ubuntu (64 bit)`
  - Note: if the option `Ubuntu (64 bit)` is not available, you probably need to activate a **BIOS setting** for virtualization. Reboot your computer into [BIOS/UEFI](https://www.youtube.com/watch?v=SlzwMKcCoMI) and enable hardware virtualization. This will appear as `Virtualization Technology` and/or `VT-x or AMD-V` or similar (different manufacturers word it differently). You can consult e.g. the following links for instructions and troubleshooting: [forums.virtualbox.org](https://forums.virtualbox.org/viewtopic.php?f=1&t=62339), [superuser.com](https://superuser.com/questions/1241956/virtualbox-only-allowing-32-bit-os), [docs.fedoraproject.org](https://docs.fedoraproject.org/en-US/Fedora/13/html/Virtualization_Guide/sect-Virtualization-Troubleshooting-Enabling_Intel_VT_and_AMD_V_virtualization_hardware_extensions_in_BIOS.html), [howtogeek.com](https://www.howtogeek.com/213795/how-to-enable-intel-vt-x-in-your-computers-bios-or-uefi-firmware/), [YouTube video](https://www.youtube.com/watch?v=yZw_8Y-v298)
  - If you have multiple BIOS options related to virtualization, e.g. `VTx` and `VTd`, you should probably enable both
- Most other settings: the defaults are ok
- Memory: at least 4 GB is recommended (can be changed later)
- Virtual hard disk size: 30-40 GB is recommended (less might be not enough; can't be changed later)
- Your new VM is saved as a folder with a few files in it (on Windows, it should be located in the folder "C:\Users\your-user\VirtualBox VMs")
- The VM is a virtual computer, with emulated hardware like a hard disk (currently empty), an optical disk drive (where you can "insert" a disk/disk image), CPU, audio and graphics devices

---
## Install the guest operating system (OS)

- Your computer is called **host**, the VM is called **guest**
- In VirtualBox: Select the VM → "Start"
  - It will ask you to select a start-up disk (the hard disk is empty, so it's looking for a bootable disk); click the folder button ("Choose a virtual optical disk file...") → "Add disk image" → navigate to the iso file and confirm → "Choose"; you just inserted a disk image into the virtual optical drive
  - If there was no such dialogue and the VM says "no bootable medium found", you can insert the disk by going to VirtualBox → VM → Settings → Storage → select the optical drive (below the "Controller: IDE") → "Choose a disk file..." (blue CD-shaped button on the right) → select the iso file and confirm
  - There might be a message about mouse pointer integration, that's [ok](https://superuser.com/questions/1375772/what-is-mouse-pointer-integration/1375774) (unless you are playing [Warcraft](https://superuser.com/questions/377861/how-do-i-trap-the-mouse-pointer-within-a-virtualbox-guest-os))
- The OS should boot now; this is called [live OS](https://en.wikipedia.org/wiki/Live_CD), because it boots directly from the disk/iso file, without being installed on the hard drive
  - If there is an error like `Hardware acceleration is not available on your system` when trying to install/launch a VM, search for "virtualbox error" + error message text. It's probable that this error occurred because virtualization wasn't activated in BIOS/UEFI, and should be easy to fix
- You should see an option to install the OS; start the installer and follow the instructions
  - Always read the questions and messages, when Linux interacts with you; it's not Windows, where many dialogues aren't helpful
  - Select English as your installation language; additional languages can be added later
  - Pay attention that the settings are correct, e.g. the **keyboard layout** should correspond to your keyboard (if you have a German keyboard, select a German keyboard layout)
  - Check useful options like "Download updates while installing" and "Install this third-party software" (explanation: [reddit](https://www.reddit.com/r/Ubuntu/comments/2xcoie/what_does_install_this_third_party_software_do/), [Wikipedia](https://en.wikipedia.org/wiki/Ubuntu-restricted-extras#Background))
  - The option "Erase disk and install Xubuntu" is ok, because you are using a virtual hard disk which you just created, and it doesn't have any partitions
- The guest OS is now being installed within the VM
- After the installation is complete: reboot the VM
  - You might need to remove the disk image from the optical drive first (to make sure that the VM boots from the hard drive and not from the live CD): VirtualBox → Select the VM → Settings → Storage → select optical disk → Look for option "Remove Disk from Virtual Drive"
  - But probably Ubuntu does it for you

---
## Linux basics

- To [open a terminal](https://docs.xubuntu.org/1910/user/C/command-line.html): Application menu → Accessories → Terminal emulator (it's called "emulator" for [historical reasons](https://superuser.com/a/930427))
- To start programs/run commands: type the program/command in the terminal and hit <kbd>Enter</kbd>
- **Abort program/command** running in the terminal: press **<kbd>Ctrl</kbd>+<kbd>C</kbd>** (this key combination sends the "SIGINT" (interrupt) signal to a running process)
- **Abort non-responsive graphical application**: enter `xkill`  + <kbd>Enter</kbd> in the terminal and click on the non-responsive application (only use this if absolutely necessary)
- If you need to repeat a command, you don't have to re-type it. The entered commands are saved, and you can access the Bash history using the <kbd>&uarr;</kbd> and <kbd>&darr;</kbd> keys ([more](https://www.howtogeek.com/howto/44997/how-to-use-bash-history-to-improve-your-command-line-productivity/))
  - E.g. enter `ls` + <kbd>Enter</kbd> → "list" the contents of the current directory
  - Press the <kbd>&uarr;</kbd> key to bring up the previously entered command (`ls`)
- **Search** for previously entered commands using **<kbd>Ctrl</kbd>+<kbd>R</kbd>**
- There are several more useful [keyboard shortcuts](https://linuxreviews.org/Basic_Linux_Keyboard_Shortcuts)
- If you can't wait to learn more Bash commands, a selection of important ones is [here](https://towardsdatascience.com/basics-of-bash-for-beginners-92e53a4c117a) or [here](https://help.ubuntu.com/community/UsingTheTerminal)
- When you interact with the terminal, you should always **read the output/error messages**. You might be used from Windows that, whenever a message appears, you click "Cancel" or "Continue" to make it go away. Messages on Linux are usually more informative and tell you what's happening and if there were problems. E.g., if you run a command, and a message says `Building modules...`, then it's building modules, and you have to wait. If it says `Successfully installed`, then the package was successfully installed. If it says `Failed to fetch http://some/web/url`, then the resource couldn't be fetched, maybe because the url was invalid or there was no internet connection. If the command didn't complete successfully, try to search for the respective error message, which can help to find a solution

---
## Update the guest and install the guest additions

- You can use the "Software Updater" for updates, which seems easier, because it's a graphical user interface (GUI). However, it's just a [frontend](https://askubuntu.com/a/539067) for Ubuntu's Advanced Packing System (APT) command-line tools, and you have more control and a better understanding of the OS if you directly use the command line
- **Update** the Ubuntu guest: Open a terminal and type `sudo apt update && sudo apt upgrade` + <kbd>Enter</kbd>
  - It should ask you for your password; type the password (it's invisible) + <kbd>Enter</kbd>
  - `sudo` (*superuser do*) grants [root](https://unix.stackexchange.com/a/254470) privileges and is required for all system-relevant tasks
  - `apt` is [a command](https://askubuntu.com/questions/155538/what-is-apt-and-aptitude-in-ubuntu) that manages installing/removing/updating most software on Ubuntu (actually Debian, which Ubuntu is based on)
  - `update`/`upgrade` are **arguments** that modify the command behavior (tell the command what to do):
    - The subcommand `apt update` updates the list of available packages and their versions in the configured sources (repositories)
    - `apt upgrade` uses this information to fetch and install packages that have new versions
  - `&&` is an **operator** that can be used to connect commands; it executes the second command [only if](https://unix.stackexchange.com/a/24685) the first one completed successfully. You could also execute `apt update` and `apt upgrade` one after the other, with the same effect
  - This might take a while and should update all installed software (packages) to their latest versions (more info: [apt tutorial](https://itsfoss.com/apt-command-guide/))
- The [guest additions](https://www.virtualbox.org/manual/ch04.html) is additional software that improves the integration of the guest with the host, e.g. it enables the auto-resizing of the OS in the VirtualBox window
- The guest additions can be installed from the (virtual) **"Guest Additions disk image"** that comes with VirtualBox:
  - You might need some additional packages like "build-essential" (probably already installed): `sudo apt install build-essential`
  - In the VM window menu bar: Devices → Insert Guest Additions CD image...
  - In the guest, the disk should be now accessible under */media/your-username/VBox_GAs_x.y.z/* (x, y, z are version numbers)
  - You probably can't use the file manager to install it (even though you can view the files), because the execution of _VBoxLinuxAdditions.run_ requires root permissions; so you have to use the terminal:
    - Use the `ls` command to *list* the directory contents:
    `ls /media/your-username` (press **Tab** once or twice to auto-complete paths, e.g. you can write `ls /me<Tab>/<Tab><Tab>`) → should list files/folders in the directory */media/your-username*
    - Enter the directory using the `cd` (*change directory*) command (using <Tab> in the same way):
    `cd /media/your-username/VBox_GAs_6.0.10/`; inspect the directory contents via `ls`
    - Install the guest additions package by running the installation script:
    `sudo ./VBoxLinuxAdditions.run`
- Some websites suggest to install the guest additions from the repository (which is a distribution-specific app store/software collection), using a command like `sudo apt install virtualbox-guest-x11 virtualbox-guest-utils virtualbox-guest-dkms`
  - Usually, this approach is better, but in this case I had problems after installation, e.g. the shared clipboard wouldn't work
  - One downside if guest additions are installed from the virtual disk, is that they are not updated automatically later
  
---
## VirtualBox basics

- Examine the VirtualBox menu bar and status bar (the symbols in the lower right corner of the VM)
- Shutting down the VM: You can do it from within the guest, like a regular computer; if you close the VM window, you will be presented with [three shutdown options](https://www.virtualbox.org/manual/ch01.html#intro-save-machine-state); "power off" should only be used as a last resort, if the VM is frozen (it's like pulling the power cord)
- **Shared clipboard** (very useful): VM → Settings → General → Advanced → Shared Clipboard: Bidirectional
- Drag'n'Drop: VM → Settings → General → Advanced → Drag'n'Drop: Bidirectional

### Share a folder between the host and the guest

- A **shared folder** is an easy way to pass files between the guest and the host OS. If you save your files in the shared folder, you can regularly back them up together with the rest of host OS, and you can delete the VM at any time without loosing your data
- In the guest, you need to add your user to a group that can access shared folders. In the terminal:
`sudo adduser your-username vboxsf`
  - After this, you need to log out from the guest and then log in again
- In VirtualBox, select your VM → Settings → Shared Folders → Add shared folder: select the folder you want to share
  - Check the checkboxes `Auto-mount` and `Make Permanent`
- In the guest, the shared folder should now be accessible under */media/sf_shared-folder-name/* and visible in the file manager
  - Try to create a text file in this folder and access it from your host, or the other way around
- Consult e.g. [websiteforstudents.com](https://websiteforstudents.com/access-virtualbox-host-folders-from-ubuntu-17-10-guest-machines/) for troubleshooting

---
## Troubleshooting

- Problems can be related to the guest (and need to be addressed within the guest), or to the host/VirtualBox, and addressed e.g. by changing VirtualBox settings (usually a shutdown of the guest is required)
- Graphics issues (display problems, freezes): Can be related to several VM display settings, VirtualBox → VM → Settings → Display
  - **Video Memory**: Increase to 128 MB (shut down the guest first)
  - Try checking/unchecking "Enable 3D acceleration" (should probably be unchecked)
  - **Graphics Controller**: Try switching to VBoxSVGA or VBoxVGA
- Memory (system suddenly becomes extremely slow):
  - VM → Settings → System → Base memory: Increase to at least ~4 GB
- Sound issues: 
  - VM → Settings → Audio → **Audio Controller**, try to switch between AC97 and Intel HD Audio
  - Guest: Applications → Sound & Video → PulseAudio Volume Control, try to change some settings
  - Still sound issues: well, that's annoying. (There might be a solution, but it can be difficult to find, or you might need to wait for updates. This also explains why Linux hasn't become more popular than Windows or macOS :) 
- Some media can't be played: install the package `ubuntu-restricted-extras` with additional media codecs and fonts ([help.ubuntu.com](https://help.ubuntu.com/community/RestrictedFormats)):
  `sudo apt install ubuntu-restricted-extras`
- Other problems:
  - Try to [categorize and isolate](https://www.virtualbox.org/manual/ch12.html#ts_categorize-isolate) the problem. Determine in which situation the problem occurs, e.g. does rebooting the VM help?
  - Use a search engine to search for the problem online. Try to describe the problem as concise as possible. E.g., if the menu bar of the VirtualBox window has dis appeared, and you can't select Devices → Insert guest additions CD image, you can search for "virtualbox menu bar missing"; you will usually find blogs or forum discussions on how to fix the problem (like [askubuntu.com](https://askubuntu.com/questions/59103/why-has-virtualboxs-menu-disappeared))
- Running a **system monitor** at all times to keep track of the memory usage and CPU load is a good idea, and helps to diagnose problems
  - Guest: Use a [system monitor](http://www.linuxandubuntu.com/home/10-best-linux-task-managers) like GNOME System Monitor (to install it: `sudo apt install gnome-system-monitor`), [`top`](https://www.lifewire.com/linux-top-command-2201163) or [Conky](https://www.lifewire.com/beginners-guide-to-conky-4043352)
  - Host: Use the Task Manager (Windows) or equivalent
  - High CPU load or memory usage can substantially slow down the system. If they are caused by a software problem, restarting the offending program can help
- Random freezes of the guest OS → try to modify these host VM settings:
  - Display → "Enable 3D acceleration" = off
  - System → Processor → Number of virtual CPUS: 1 processor → 2, 3 or 4 processors (try and see if this helps)
  - System → Processor → "Enable PAE/NX": toggle this off if it’s on, or on if it’s off, and see if this helps
  - Display → increase "Video memory" to 128 MB
  - System → Acceleration → Paravirtualization Interface: try "Minimal" or "Legacy"
  - Try a different (older) version of VirtualBox
- Still problems with the guest (freezes, high CPU load for no reason, etc.): One possibility is to try another desktop environment; recommended options are LXQt, Xfce and MATE. There are others, but they may be less performant. Installed environments can be selected in the "Session" field [at login](https://www.howtogeek.com/193129/how-to-install-and-use-another-desktop-environment-on-linux/)
- Guest system is generally slow: this shouldn't happen with Xubuntu, and is probably a host issue rather than a guest issue (e.g. not enough RAM, slow CPU, slow overall performance) 
- Advanced VirtualBox-related topics: e.g. [wiki.ubuntuusers.de](https://wiki.ubuntuusers.de/VirtualBox/Problembehebung/)
- General note: You will most likely encounter at least some problems with Linux; Linux was designed for system stability, transparency and development rather than a polished user experience
  - If the problem is Linux-related, also read the distribution [release notes](https://wiki.xubuntu.org/start?do=index) and check for known bugs and workarounds.

---
## Updates

- Guest: **Update regularly** using `sudo apt update && sudo apt upgrade` or the update dialogue
- Host:
  - Keep the OS updated
  - When updating VirtualBox, *completely shutdown the VM* before that
    - Major (e.g. Virtualbox 5 → 6) and even minor (e.g. VirtualBox 6.0 → 6.1) releases introduce new features and can therefore break things (worst case, you need to downgrade again)
    - Maintenance releases (e.g. VirtualBox 6.0.8 → 6.0.10) are bug fix releases and usually don't break things
    - If there are problems after a VirtualBox update, e.g. a VM that used to work doesn't boot and you get strange error messages: "Have You Tried Turning It Off and On Again?" (try rebooting the computer, possibly twice)

---
## Where to go from here

- **Back up your VM.** You can do it based on the instructions on [osradar.com](https://www.osradar.com/how-to-backup-vms-on-virtualbox/) and [lifewire.com](https://www.lifewire.com/create-virtual-machines-clones-and-snapshots-in-virtualbox-4177998), however I highly recommend to also completely shut down your VM and copy the complete VM-folder to an external hard drive. The VM-folder should be located in the folder "VirtualBox VMs" in your home directory (more info on [virtualbox.org](https://forums.virtualbox.org/viewtopic.php?f=6&t=81581)). If your VM is broken beyond repair and you have a functional backup, you can restore it from the backup. This is usually easier than performing an installation from scratch.
  - You can import it later like this: Machine → Add → Navigate to the _.vbox_ file in the VM folder ([superuser.com](https://superuser.com/questions/633431/whats-the-recommended-way-to-move-a-virtualbox-vm-to-another-computer), [superuser.com](https://superuser.com/questions/745844/how-can-i-import-an-existing-vbox-virtual-machine-in-virtualbox/746429))
- Take a [quick Xubuntu tour](https://www.youtube.com/watch?v=V_gODEnrxI0)
- Customitize your Xubuntu installation [just for fun](https://itsfoss.com/customize-xfce/) ([more](https://www.lifewire.com/customize-xfce-desktop-environment-2202080))
- Learn about [Xubuntu software management](https://docs.xubuntu.org/current/user/C/managing-applications.html) and install some useful programs using the command line or GUIs (Start menu → Software; Start menu → Settings Manager → Software & Updates)
  - Some tutorials use `apt` for software installation, while others use [`apt-get`](https://itsfoss.com/apt-get-linux-guide/); the differences are [marginal](https://itsfoss.com/apt-vs-apt-get-difference/)
  - More info: [help.ubuntu.com](https://help.ubuntu.com/community/SoftwareManagement)
- **Learn the command line.** Even though some tasks like software installation can be done via GUIs, they are just frontends to command-line tools like `apt`, and it's preferable to use the original thing. Linux GUIs can also be buggy, because neither users nor developers like them very much
  - Go through an introductory Linux/Bash tutorial, like [this YouTube video](https://www.youtube.com/watch?v=oxuRxtrO2Ag) and [this online book](linuxcommand.org)
  - Cheat sheets like [this one](https://devhints.io/bash) can help, but none of them will be as good as your own cheat sheet; a text file with important commands is a good start
  - Take [an interactive course](https://linuxsurvival.com/) or [play a game](https://overthewire.org/wargames/bandit/)
  - Get help on Bash commands using the manpages (`man ls`) or the [**TLDR** ("Too Long; Didn't Read") manpages](https://tldr.ostera.io/) (enter the "command name" in the corresponding box, try `ls`)
- Learn how to use a **non-GUI text editor**, [nano](https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/) or [vim](https://www.youtube.com/watch?v=ggSyF1SVFr4)
