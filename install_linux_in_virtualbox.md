# Guide for installing Linux in VirtualBox

### Install VirtualBox on your computer
- Download and install Oracle VirtualBox (https://www.virtualbox.org/)
  - If installation on MacOS fails, consult e.g. http://osxdaily.com/2018/12/31/install-run-virtualbox-macos-install-kernel-fails/
- Start VirtualBox and install the Extension Pack

---
### Download the Linux iso file (disc image)
- Recommended Linux distribution: latest Lubuntu (https://en.wikipedia.org/wiki/Lubuntu), downloaded from **lubuntu.me** (not lubuntu.net); at the moment of writing, the filename of the downloaded file is "lubuntu-19.04-desktop-amd64.iso"
- Lubuntu is a lightweight version of Ubuntu, which has a different selection of pre-installed software, requires less resources and is in general more responsive. Any required software can also be installed later.

---
### Create a new Virtual Machine (VM) in VirtualBox
- VirtualBox -> "New"
- Enter Name: e.g. Lubuntu
- Make sure that Type is Linux
- Make sure that Version is **"Ubuntu (64 bit)"**
  - Note: if Ubuntu (64 bit) is not available, you will need to activate a **BIOS setting** for virtualization. Reboot your computer into BIOS and enable hardware virtualization. This will appear as "Virtualization Technology" and/or "VT-x or AMD-V" or similar (different manufacturers word it differently). You can consult e.g. https://forums.virtualbox.org/viewtopic.php?f=1&t=62339, https://superuser.com/questions/1241956/virtualbox-only-allowing-32-bit-os and https://www.howtogeek.com/213795/how-to-enable-intel-vt-x-in-your-computers-bios-or-uefi-firmware/ for instructions and troubleshooting.
- Most other settings: the defaults are ok
- Memory: 1-2 GB should be ok, 4 GB is even better (can be changed later)
- Virtual hard disk size: 30-50 GB are recommended (less might be not enough; can't be changed later)
- Your new VM is saved as a folder with a few files in it (on Windows, it should be located in the folder C:\Users\your-user\VirtualBox VMs)
- The VM is essentially a simulated computer, with a hard drive (currently empty), an optical disc drive (where you can "insert" a disc/disc image), and simulated audio/graphics hardware

---
### Install the Lubuntu guest
- The operating system (OS) that runs on your computer is called **host**, the OS in the VM is called **guest**
- In VirtualBox: Select the VM -> "Start"
- It should ask you for a disc (the hard drive is empty, so it is looking for a bootable disc) -> select the iso file
- Boot the OS (this is called "live OS" because it's booted directly from the disc/iso file, without being installed on the hard drive)
- There should be an option to install the OS; start the installer and follow the installation instructions
  - If there are checkboxes like "Download updates while installing" and "Install this third-party software", check them
  - The option "Erase disk and install Lubuntu" is fine, because you are using a virtual hard drive which should not have any partitions anyway
- The guest OS is now being installed within the VM
- After the installation is complete: reboot the VM
  - you *might* need to remove the disc image from the optical drive (to make sure that the VM boots from the hard drive and not from the disc image): VirtualBox -> VM -> Settings -> Storage -> Select optical disc -> Look for option "Remove Disc from Virtual Drive"; seems to not be necessary with Lubuntu

---
### Linux basics
- Open a terminal: Application menu -> System Tools -> Qterminal
- Start programs/run commands: type the name of the program/command and hit Enter
- **Abort program/command running in the terminal**: press Strg-C (this key combination sends the "SIGINT" (interrupt) signal to a running process)
- **Abort non-responsive graphical application**: enter `xkill` in the terminal and click on the non-responsive application
  - only use this if absolutely necessary
- Get previously entered command using up/down keys
  - e.g. enter `ls` + Enter -> "list" the directory contents
  - press the up key -> it brings up the previously entered `ls` command
- **Search** for previously entered commands using Strg-R

---
### Update the guest and install the guest additions
- **Update** the Lubuntu guest: Open a terminal and enter `sudo apt update && sudo apt upgrade`
  - `sudo` (*superuser do*) grants admin rights and is required for all system-relevant tasks
  - `apt` is the command that manages installing/removing/updating most software on Ubuntu (actually Debian, which Ubuntu is based on)
  - `apt update` is used to download package information, while `apt upgrade` actually installs the updated package versions
  - `update`/`upgrade` are **arguments** that modify the command behavior (tell the command what to do)
  - `&&` is an operator that connects two commands and executes the second one only if the first one successfully completed; you could also execute the `apt update` and `apt upgrade` commands subsequently
  - This might take a while and should update all installed software ("packages") to their latest versions
- The guest additions is additional software that improves the integration of the guest with the host
- The guest additions can be installed from the (virtual) **"Guest Additions disc image"** that comes with VirtualBox:
  - You might need some additional packages like "build-essential" (unless already installed): `sudo apt install build-essential`
  - In the VM window menu bar: Devices -> Insert Guest Additions CD image...
  - In the guest, the disc should be now accessible under /media/your-username/VBox_GAs_x.y.z/ (x, y, z are version numbers)
  - You probably can't install it from file manager, because the exeuction of VBoxLinuxAdditions.run requires root permissions
  - So, you have to use the terminal:
    - Use the `ls` (*list*) command to look at directory contents:
    `ls /media/your-username` (press **Tab** once or twice to auto-complete paths, e.g. you can write `ls /me<Tab>/<Tab><Tab>`) -> should list files/folders in the directory "/media/your-username".
    - Enter the directory using the `cd` (*change directory*) command:
    `cd /media/your-username/VBox_GAs_6.0.10/`
    - Install the guest additions package:
    `sudo ./VBoxLinuxAdditions.run`
- On the internet, you might read that guest additions can (or should) be installed from the repository (which is essentially an app store/software collection specific to each Linux distribution and version), using the command `sudo apt install virtualbox-guest-x11 virtualbox-guest-utils virtualbox-guest-dkms`
  - Usually, it's easier to install software from the repository, but in this case it might not work as well (e.g., for me, the shared clipboard wouldn't work)

---
### Some useful VirtualBox options
- **Shared clipboard** (very useful): VM -> Settings -> General -> Advanced -> Shared Clipboard: Bidirectional
- Drag'n'Drop: VM -> Settings -> General -> Advanced -> Drag'n'Drop: Bidirectional

---
### Share a folder between the host and the guest
- A **shared folder** is a useful way of exchanging files between the guest and the host systems. If you save all important files in the shared folder, you can delete the VM any time without loosing your data.
- In the guest, you need to add your user to a group that can access shared folders. In the terminal:
`sudo adduser your-username vboxsf`
  - After this, you need to log out from the guest and then log in again
- In VirtualBox, select your VM -> Settings -> Shared Folders -> Add shared folder: select the folder you want to share
  - check the checkboxes Auto-mount and Make Permanent
- In the guest, the shared folder should now be accessible under /media/sf_shared-folder-name/ and visible in the file manager
  - try to create a text file in this folder and access it from your host, or the other way round
- Consult e.g. https://websiteforstudents.com/access-virtualbox-host-folders-from-ubuntu-17-10-guest-machines/ for troubleshooting

---
### Troubleshooting
- Problems can be related to the guest (and need to be addressed within the guest), or to the host/VirtualBox, and addressed e.g. by changing VirtualBox settings (usually a shutdown of the guest is required)
- Graphics issues:
  - Host: VM -> Settings -> Display -> **Video Memory**: Increase to 128 MB (shut down the guest first)
  - Host: VM -> Settings -> Display: Try checking/unchecking "Enable 3D acceleration" (should probably be unchecked)
  - Host: VM -> Settings -> Display -> **Graphics Controller**: Try switching to VBoxSVGA or VBoxVGA
- Memory:
  - Host: VM -> Settings -> System -> Base memory: Increase to ~4 GB
- Sound issues: 
  - Host: VM -> Settings -> Audio -> **Audio Controller**, you can try to switch between AC97 and Intel HD Audio
  - Guest: Applications -> Sound & Video -> PulseAudio Volume Control, you can try to change some settings
  - Still sound issues: well, that's annoying. (There might be a solution, but it can be difficult to find, or you might need to wait for updates. This also explains why Linux hasn't become more popular than Windows or MacOS :) 
- Some media can't be played: install the package "lubuntu-restricted-extras" with additional media codecs and fonts (https://help.ubuntu.com/community/RestrictedFormats):
  `sudo apt install lubuntu-restricted-extras`
- Other problems:
  - Start with reading the distribution release notes (e.g. https://lubuntu.me/disco-released/), check for known bugs and workarounds; e.g. one Lubuntu bug concerns missing proprietary drivers (shouldn't be an issue for an installation within VirtualBox, but can be a problem if Lubuntu is installed directly on a computer)
  - Try to determine in which situation the problem occurs, e.g. does rebooting the VM help?
  - Google is your friend
- System is slow: this shouldn't happen with Lubuntu, and is probably a host issue rather than a guest issue. One thing you can try is installing an alternative (very lightweight) window manager like IceWM (https://wiki.ubuntuusers.de/IceWM/)
- Advanced VirtualBox-related topics: https://wiki.ubuntuusers.de/VirtualBox/Problembehebung/
- Note: You WILL encounter bugs; Linux was designed for system stability, transparency and production/development rather than a polished user experience

---
### Updates
- Guest: Update regularly using `sudo apt update && sudo apt upgrade` or the update dialogue
- Host:
  - Keep the OS updated
  - When updating VirtualBox, *completely shutdown the VM* before that
    - Be careful with major (e.g. Virtualbox 6 -> 7) or minor (e.g. VirtualBox 6.0 -> 6.1) releases, they can break things (you might even need to downgrade again)
    - Maintenance releases (e.g. VirtualBox 6.0.8 -> 6.0.10) usually don't break things

---
### Where to go from here
- **Back up** your VM. You can do it based on the instructions in https://www.osradar.com/how-to-backup-vms-on-virtualbox/ and https://www.lifewire.com/create-virtual-machines-clones-and-snapshots-in-virtualbox-4177998, however I highly recommend to also completely shut down your VM and copy the complete VM-folder to an external hard drive. The VM-folder should be located in the folder "VirtualBox VMs" in your home directory. (More information in https://forums.virtualbox.org/viewtopic.php?f=6&t=81581). If something breaks in your VM which you can't repair and you have a backup of a working state, you can always take the backup. This is usually much faster than doing an installation from scratch.
- Tweak Lubuntu settings:
  - right-click on Desktop -> Desktop preferences -> change background image
  - right-click on Panel in the lower part of the Desktop -> Manage Widgets -> add CPU monitor
- Become comfortable with the command line: **linuxcommand.org**
- Navigate the filesystem using `pwd`, `ls` and `cd`
- Use manpages (`man ls`) or simplified manpages, https://tldr.ostera.io/
- Learn how to use a non-GUI text editor, nano (https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/) or vim
- There is a ton of good introductory linux/shell tutorials on YouTube

