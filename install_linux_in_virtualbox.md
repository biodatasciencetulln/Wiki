<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>Guide for installing Ubuntu in VirtualBox</H1>

**Table of contents**

- TOC
{:toc}

Used software: VirtualBox 7, Xubuntu 24.04

Note for Apple silicon computers (Macbooks with M1 chip or later): VirtualBox is not available for Apple silicon, alternatives are:

- [VMware Fusion Pro](https://knowledge.broadcom.com/external/article/368667/download-and-license-information-for-vmw.html) (in case of problems see [reddit](https://www.reddit.com/r/vmware/comments/1cry8ej/comment/l426xtq/)): free for personal use; see [companion guide](https://community.broadcom.com/vmware-cloud-foundation/discussion/version-28-of-the-fusion-companion-guide-is-now-available) (v28 at the time of writing; you need only the "Ubuntu" section from the guide), [YouTube tutorial](https://www.youtube.com/watch?v=4dFy-4pw8NA), [forum](https://community.broadcom.com/communities/communityhomeblogs?CommunityKey=0c3a2021-5113-4ad1-af9e-018f5da40bc0)
- [UTM](https://docs.getutm.app/guides/ubuntu/): open source; see [website](https://mac.getutm.app/), [GitHub](https://github.com/utmapp/UTM/)
- [Parallels Desktop](https://www.parallels.com/products/desktop/): popular, but requires a paid license
- UTM and VMware Fusion Pro both work well, you can also try out both; here is a [short installation guide](install_linux_in_UTM.md) for UTM

All functionality of VirtualBox is explained in the [official documentation](https://docs.oracle.com/en/virtualization/virtualbox/index.html), especially the User Manual (as [PDF](https://download.virtualbox.org/virtualbox/UserManual.pdf) or <a href="https://www.virtualbox.org/manual/">web page</a>). Apart from the documentation, there are many tutorials on the Internet for all purposes; e.g. for installing Ubuntu on VirtualBox, you can find

- a tutorial from Canonical, the company behind Ubuntu: [ubuntu.com](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox); however, it uses the VirtualBox option for unattended install, and we don't want this, because this takes away control from the user and can introduce additional problems
- many videos on [YouTube](https://www.youtube.com/watch?v=DhVjgI57Ino) (also [YouTube](https://www.youtube.com/watch?v=v1JVqd8M3Yc), [YouTube](https://www.youtube.com/watch?v=wX75Z-4MEoM); hint: the [Return YouTube Dislike](https://chromewebstore.google.com/detail/return-youtube-dislike/gebbhagfogifgggkldgodflihgfeippi?hl=en) extension is helpful for a quick assessment of the video)
- tutorials by more or less well-known web-portals like [itsfoss.com](https://itsfoss.com/install-linux-in-virtualbox/), companies like [nakivo.com](https://www.nakivo.com/blog/install-ubuntu-on-virtualbox-virtual-machine/), or private individuals

Here, we discuss some points in more detail, with additional information and links. It's probably a lot of new information for you, but remember the [Pareto principle](https://betterexplained.com/articles/understanding-the-pareto-principle-the-8020-rule/): 20% of the work produce 80% of the result.

**Note**: Please make a full backup of your computer before making any modifications.

## Install VirtualBox on your computer

- Download and install [Oracle VirtualBox](https://www.virtualbox.org/) (Oracle is the company behind VirtualBox)
  - Note: During all steps of the tutorial, you might encounter some problems. For widely used software like VirtualBox and Ubuntu, these problems have usually been discussed online and a solution exists. A **web search** for your particular problem based on **important keywords** (e.g. the error message) can help
  - E.g., if installation on macOS fails, you can search for "virtualbox macos installation failed" and find links like [osxdaily.com](http://osxdaily.com/2018/12/31/install-run-virtualbox-macos-install-kernel-fails/) or [medium.com](https://medium.com/@DMeechan/fixing-the-installation-failed-virtualbox-error-on-mac-high-sierra-7c421362b5b5), which say that this can be related to a macOS security feature (Gatekeeper) and explain how to fix it
  - Of course, you can also talk to LLMs like ChatGPT - but you shouldn't rely on them especially for recent or non-trivial problems, as they lack an actual "understanding" of the problem, are prone to **hallucinations** (a better term might be <a href="https://www.scientificamerican.com/article/chatgpt-isnt-hallucinating-its-bullshitting/">bullshitting</a>) and may not have the latest information
- When you run VirtualBox, it may suggest to install the Oracle **Extension Pack**. It contains additional Oracle proprietary components which extend the functionality of the base package ([VirtualBox Manual](https://www.virtualbox.org/manual/ch01.html#intro-installing)). While VirtualBox is licensed under the GPL2 license and therefore free for any use, the Extension Pack has a more restrictive license. This license includes educational use ([VirtualBox Licensing FAQ](https://www.virtualbox.org/wiki/Licensing_FAQ)), but the interpretation is ambiguous, and VirtualBox can be used without it. Therefore, the installation of the Oracle extension pack is currently not recommended

---

## Download the Linux ISO file (disk image)

- Recommended Linux distribution is the latest [Xubuntu](https://en.wikipedia.org/wiki/Xubuntu) LTS release (currently 24.04, [ubuntu.com](https://ubuntu.com/blog/what-is-an-ubuntu-lts-release)). You can download the [ISO file](https://www.howtogeek.com/356714/what-is-an-iso-file-and-how-do-i-open-one/) from the [official download page](https://xubuntu.org/download/). The downloaded disk image should have a name like `xubuntu-<version>-desktop-amd64.iso` (for an explanation what `amd64` means, see e.g. [askubuntu.com](https://askubuntu.com/a/67468/))
  - If your host OS is Windows, it's highly recommended to make it display file extensions ([howtogeek.com](https://www.howtogeek.com/205086/beginner-how-to-make-windows-show-file-extensions/)); the downloaded ISO file should have the `.iso` file extension
- **Xubuntu is Ubuntu** with a different [desktop environment](https://askubuntu.com/questions/18078/what-is-the-difference-between-a-desktop-environment-and-a-window-manager), called [Xfce](http://www.linuxandubuntu.com/home/xfce-desktop-environment-a-linux-desktop-environment-for-everyone). It has a different **selection of pre-installed software** ([docs.xfce.org](https://docs.xfce.org/)), requires less resources and is more responsive than the default GNOME desktop environment
  - The differences are mostly [superficial](https://askubuntu.com/questions/1177309/does-every-ubuntu-question-answer-apply-to-its-derivatives-xubuntu-lubuntu) (related to specific software and settings). All Ubuntu derivatives (or <a href="https://ubuntu.com/desktop/flavours">flavors</a>) use the same software sources and the same commands, therefore most Ubuntu-related tutorials also apply to Xubuntu
  - Another interesting and even more lightweight (needs less RAM, very responsive) Ubuntu flavor is [Lubuntu](https://lubuntu.me/), using the LXQt desktop environment (possibly less stable than Xfce). You can also use the default [Ubuntu](https://ubuntu.com/download/desktop) with the GNOME desktop environment, if you prefer (performant hardware is recommended)

---

## Create a new Virtual Machine (VM) in VirtualBox

- VirtualBox → "New" (for details, see [docs.oracle.com](https://docs.oracle.com/en/virtualization/virtualbox/7.0/user/Introduction.html#create-vm-wizard))
- `Name`: e.g. `Xubuntu`
- `Folder`: default (the new **VM is saved as a folder** with a few files in it; on Windows, it may be located in the folder `C:\Users\<username>\VirtualBox VMs`)
- `ISO Image`: Select the downloaded ISO file (`xubuntu-<version>-desktop-amd64.iso`)
- `Type`: `Linux` (should have been auto-selected)
- `Version`: **`Ubuntu (64 bit)`** (should have been auto-selected)
  - If the option `Ubuntu (64 bit)` is not available, you probably need to
    activate a **BIOS setting for virtualization**. Reboot your computer into
    [BIOS/UEFI](https://www.youtube.com/watch?v=SlzwMKcCoMI) and enable hardware
    virtualization. This will appear as `Virtualization Technology` and/or `VT-x
or AMD-V` or similar (different manufacturers word it differently). See
    [forums.virtualbox.org](https://forums.virtualbox.org/viewtopic.php?f=1&t=62339)
    and
    [superuser.com](https://superuser.com/questions/1241956/virtualbox-only-allowing-32-bit-os),
    [howtogeek.com](https://www.howtogeek.com/213795/how-to-enable-intel-vt-x-in-your-computers-bios-or-uefi-firmware/),
    [support.bluestacks.com](https://support.bluestacks.com/hc/en-us/articles/360058102252-How-to-enable-Virtualization-VT-on-Windows-10-for-BlueStacks-5),
    [wiki.2n.com](https://wiki.2n.com/faqac/en/virtualizace-vt-x-amd-v-povoleni-virtualizace-na-vasem-pocitaci-pro-spusteni-2n-access-commander-100572533.html),
    [YouTube](https://www.youtube.com/watch?v=yZw_8Y-v298) for instructions. If
    you have multiple BIOS options related to virtualization, e.g. `VTx` and
    `VTd`, you should probably enable both. (You can check if virtualization is
    enabled using system information, `msinfo32`
    ([stackoverflow.com](https://stackoverflow.com/a/49013155/)); the Task Manager method is less reliable)
  - It's also possible that the 64 bit option is available, but when you start your VM later, it aborts with a cryptic error message, or it just shows a black screen. This can be related to the same issue. If restarting the VM doesn't help, try activating the virtualizaton settings in BIOS to solve the problem
  - There are other possible reasons that can prevent a normal operation of VirtualBox (e.g., an error message appears when you try to start the VM). The error messages are usually not very informative, and your best bet is a web search for the respective message. One issue is related to third-party software that somehow interferes, e.g. antivirus software like McAfee or Trusteer Endpoint Protection. You can try to uninstall this software as explained [here](https://forums.virtualbox.org/viewtopic.php?f=25&t=82106#p388051), reboot the computer and run the VM again to check if this helped. Another option is to follow the instructions [here](https://forums.virtualbox.org/viewtopic.php?f=6&t=82277) to disable the startup of a VirtualBox service; the service probably needs to be started manually as explained [here](https://forums.virtualbox.org/viewtopic.php?f=6&t=82277&start=30#p465502) or using a task scheduler as explained [here](https://forums.virtualbox.org/viewtopic.php?f=6&t=82277&start=30#p465550)
- Now, you have two options. You can proceed with the **unattended guest OS installation**, which is now the default option, as described in [ubuntu.com](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox). In this case, VirtualBox pre-configures and performs some actions described later in this tutorial automatically (especially [Install the guest operating system (OS)](#install-the-guest-operating-system-os) and installing the guest additions).
  - If you choose to continue with the unattended installation, in the next step you get to the "Unattended Guest OS Install Setup" dialog, where you pick a username and a [hostname](https://itsfoss.com/change-hostname-ubuntu/) (the [domain name](https://superuser.com/questions/59093/difference-between-host-name-and-domain-name) doesn't matter)
  - However, for more control and a better understanding of what is going on, it is preferable to **perform a regular installation**. (Also, you may be using other virtualization software in the future, which doesn't have such convenience options.) For this, check the box `Skip Unattended Installation`. The continuation of this tutorial will assume a regular installation.
- Click `Next`
- Most other settings: **the defaults** are OK
  - Memory: ≥4 GB is recommended (can be changed later); it's better to not allocate more than half of the host memory to the guest (e.g. if the host has 16 GB RAM, you can give 8 GB to the guest), so that the host still has enough memory and won't crash
  - Processors: ≥2 is recommended (can be changed later); again, don't give the VM more than half of your physical processors
  - Virtual hard disk size: ≥60 GB is recommended, 80-100 GB is even better (changing this later is [annoying](https://www.howtogeek.com/124622/how-to-enlarge-a-virtual-machines-disk-in-virtualbox-or-vmware/), because you'll also need to change the partition size on the virtual HDD)
- In the "Summary" you see the final setup of the VM that you are about to create. The **VM is a virtual computer**, with emulated hardware like a hard disk (currently empty), an optical disk drive (where you can "insert" a CD image), CPU, audio and graphics devices
  - It's important to realize that the guest OS doesn't know that it lives in a VM rather than on a physical computer; this is why later, during installation, it says "Erase disk and install Ubuntu"

---

## Install the guest operating system (OS)

- Your physical computer is called **host**, the VM is called **guest**; the operating system (OS) running on the host is called host OS, and on the guest it's the guest OS ([VirtualBox Manual](https://www.virtualbox.org/manual/ch01.html#virtintro)); often people don't make the distinction between the computer and the OS, and just call them host or guest
- In VirtualBox: Select the VM → "Start"
  - In older VirtualBox versions, you needed to **select a start-up disk** (the emulated hard disk is still empty, so the VM is looking for a bootable disk); in VirtualBox 7, you already selected the ISO file in the previous step, so the OS boots from this ISO (it corresponds to a DVD inserted into an optical drive of a computer)
  - If you wanted, you could select a different disk file by going to VirtualBox Manager → VM → Settings → Storage → click on the CD-shaped optical drive (below the "Controller: IDE") → "Choose a disk file..." (blue CD-shaped button on the right) → select the ISO file
  - There might be a message about mouse pointer integration, that's [OK](https://superuser.com/questions/1375772/what-is-mouse-pointer-integration/1375774) (unless you are playing [Warcraft](https://superuser.com/questions/377861/how-do-i-trap-the-mouse-pointer-within-a-virtualbox-guest-os))
- The OS should boot now; this is called [live OS](https://en.wikipedia.org/wiki/Live_CD), because it **runs directly from a removable medium** (in this case a disk image), without being installed on the hard disk
  - If you get an error like "Hardware acceleration is not available on your system" when trying to install/launch a VM, do a web search for "virtualbox error" + error message text. This error probably occurred because virtualization wasn't activated in BIOS/UEFI, and is easy to fix
- You should see an option to **install the OS**; start the installer and follow the instructions
  - Always **read the questions and messages** when Linux talks to you; unlike in Windows, many messages and dialogs are actually helpful, and provide important information
  - Verify the settings, e.g. the **keyboard layout** should correspond to your keyboard (if you have a German keyboard, select a German keyboard layout)
  - Check useful options like "Download updates while installing" and "Install third-party software ..." (explanation: [reddit](https://www.reddit.com/r/Ubuntu/comments/2xcoie/what_does_install_this_third_party_software_do/), [Wikipedia](https://en.wikipedia.org/wiki/Ubuntu-restricted-extras#Background))
  - The option "Erase disk and install Xubuntu" is OK, because you are using a virtual hard disk that you just created, and it doesn't have any data and partitions on it
  - The guest OS is now being installed on the emulated hard disk (within the VM)
- Once the installation has finished, it will ask you to reboot
  - It might ask to remove the installation medium (the disk image) from the (virtual) optical disk drive, so that the OS boots from the hard disk image and not again as live OS; you can do it manually (VirtualBox → VM → Settings → Storage → select optical disk → look for option "Remove Disk from Virtual Drive"), but probably Ubuntu does it for you

---

## Linux basics

- To [open a
  terminal](https://docs.xubuntu.org/current/user/C/command-line.html):
  Application menu → Accessories → Terminal emulator (it's called "emulator" for
  [historical reasons](https://superuser.com/a/930427))
- Start programs/run commands: type the program/command in the terminal and
  hit <kbd>Enter</kbd>
- **Abort program/command** running in the terminal: press
  **<kbd>Ctrl</kbd>+<kbd>C</kbd>** (this key combination sends the "SIGINT"
  (interrupt) signal to a running process)
- **Abort non-responsive graphical application**: enter `xkill` +
  <kbd>Enter</kbd> in the terminal and click on the non-responsive application
  (only use this if absolutely necessary)
- The Bash shell stores the history of commands you run
  ([more](https://www.howtogeek.com/44997/how-to-use-bash-history-to-improve-your-command-line-productivity/))
  - Use the arrow keys <kbd>&uarr;</kbd>/<kbd>&darr;</kbd> to repeat
    previously typed commands: E.g. enter `ls` + <kbd>Enter</kbd> → _list_ the
    contents of the current directory; now, press the <kbd>&uarr;</kbd> key to
    bring up the previously entered command
  - **Search** for previously entered commands using
    **<kbd>Ctrl</kbd>+<kbd>R</kbd>**
- [Here](https://linuxreviews.org/Basic_Linux_Keyboard_Shortcuts) are the most
  useful keyboard shortcuts
- The Linux **file system** has a single hierarchical directory structure. The
  top directory is `/`, called **root directory** (or simply root). All files
  and folders are part of this hierarchy. Devices like disks, external memory
  devices and network resources (e.g. shared folders) are also part of the
  hierarchy. It'll help to know at least the [basic navigation
  commands](http://linuxcommand.org/lc3_lts0020.php), `pwd`, `cd` and `ls`
- If you can't wait to learn more Bash commands, the **basics** are
  [here](https://towardsdatascience.com/basics-of-bash-for-beginners-92e53a4c117a)
  or [here](https://help.ubuntu.com/community/UsingTheTerminal)
- When you interact with the terminal, you should always **read the output/error
  messages**, even if you don't understand everything they say. You might be
  used from Windows that you just click "Cancel" or "Continue" to make the
  messages go away. Messages on Linux are usually more informative and tell you
  what's happening and if a problem occurred. E.g., if you run a command, and a
  message says `Building modules...`, then it's building modules, and you have
  to wait. If it says `Successfully installed`, then the package was
  successfully installed. If it says `Failed to fetch http://some/web/url`, then
  the resource couldn't be fetched, maybe because the URL was invalid or there
  was no Internet connection. If the command didn't complete successfully, try
  to search for the respective error message, which can help to find a solution
- Keeping track of the system state, like processor load, RAM
  usage, [swap](https://serverfault.com/questions/48486/what-is-swap-memory)
  usage, network usage and disk usage, helps to diagnose problems. For
  example, if RAM and swap space are filled up, the system will freeze. It's
  therefore recommended to add the [system load
  monitor](https://docs.xfce.org/panel-plugins/xfce4-systemload-plugin/start) to
  the [Xfce panel](https://docs.xfce.org/xfce/xfce4-panel/start) by right-clicking on the panel and selecting `Panel` → `Add New Items`

---

## Update the guest

After a fresh install, it's good practice to update the OS, to ensure that it's fully up to date. You can do this by using the built-in update/software management mechanism. (Unlike some other distributions, Ubuntu provides only well-tested software packages via this mechanism, which rarely lead to problems. Instead, updates can for example provide the latest drivers that better support recent hardware.)

- It's tempting to use the "Software Updater" GUI (graphical user interface) for installing updates. However, it's just a [frontend](https://askubuntu.com/a/539067) for Ubuntu's Advanced Packing System (APT) command-line tools, and you have more control and a better understanding of what's happening if you **use the command line**
- Open a terminal, type `sudo apt update && sudo apt upgrade` (copy-pasting probably won't work yet) + <kbd>Enter</kbd>. It should ask you for your password. Type the password (it's invisible) + <kbd>Enter</kbd>. After an additional confirmation step, the command will update all installed software (packages) to their latest versions.
  - `sudo` (_superuser do_) grants [root privileges](https://unix.stackexchange.com/a/254470) and is required for all system-relevant tasks
  - `apt` is [a command](https://askubuntu.com/questions/155538/what-is-apt-and-aptitude-in-ubuntu) that manages installing/removing/updating most software on Ubuntu and Debian, which Ubuntu is based on; more info: [apt tutorial](https://itsfoss.com/apt-command-guide/)
  - `update` and `upgrade` are **arguments** that modify the command behavior (tell the command what to do):
    - The subcommand `apt update` updates the list of available packages and their versions in the configured sources (repositories)
    - `apt upgrade` uses this information to fetch and install packages that have new versions
  - `&&` is an **operator** that can be used to connect commands; it executes the second command [only if](https://unix.stackexchange.com/a/24685) the first one completed successfully. You can also execute `apt update` and `apt upgrade` on two separate lines
- After `apt` is finished (the command prompt returns and you can enter new commands), [reboot](https://xubuntu.github.io/xubuntu-docs/user/C/introduction.html#session-management) the guest. Upon reboot, there should be no apparent changes. To make sure that you have the latest software versions, you can repeat the command `sudo apt update && sudo apt upgrade`; this time, `apt` should tell you that there is nothing to update.

---

## Install the guest additions

The [guest additions](https://www.virtualbox.org/manual/UserManual.html#guestadditions) are VirtualBox-related drivers/software provided by Oracle that improve the **integration of the guest** with the host. For example, they enable auto-resizing of the guest in the VirtualBox window, and clipboard sharing between guest and host. Installation instructions are given in [docs.oracle.com](https://docs.oracle.com/en/virtualization/virtualbox/7.0/user/guestadditions.html#additions-linux-install), but other tutorials like [askubuntu.com](https://askubuntu.com/questions/22743/how-do-i-install-guest-additions-in-a-virtualbox-vm), [YouTube](https://www.youtube.com/watch?v=VTI8h1N51gY) (min 14:00), [itsfoss.com](https://itsfoss.com/virtualbox-guest-additions-ubuntu/) etc. can also be helpful.

- There are two ways to install the guest additions, from the **Guest Additions CD image** that comes with VirtualBox, or **from the repository**, a distribution-specific app store/software collection. The currently **recommended way** is the installation from the CD image, because this guarantees that it matches the VirtualBox version.
  - This is unusual; installation from the repository is _usually_ preferable, because such software will automatically be updated whenever you run `apt update && apt upgrade`
- **A.** Installation from CD image.
  - Prerequisites (might be already installed): `sudo apt install build-essential dkms linux-headers-$(uname -r)`
  - VM window menu bar: Devices → "Insert Guest Additions CD image..."
    - If this doesn't work, the virtual optical drive is probably occupied by
      another CD/DVD, and you should eject it first (using the [eject
      icon](https://help.ubuntu.com/stable/ubuntu-help/files-removedrive.html)
      in the file manager, or "Devices" → "Optical drives" → "Remove disk from
      virtual drive", or shut down the guest and do it from the Settings →
      Storage section in the VirtualBox Manager)
  - The disk image will be mounted under `/media/<username>/VBox_GAs_<x>.<y>.<z>/` (x, y, z are version numbers). **Mounting** makes file systems (files and directories on a storage device such as hard drive, CD, or network share) available for use, and associates them with a particular point in the file system hierarchy (its mount point)
  - If the guest OS has autorun enabled, a system dialog will appear (Ubuntu); otherwise you need to run the installer manually (Xubuntu):
  - Open the CD icon on your Desktop/in File Manager; right-click → "Open Terminal Here"
  - Use the `pwd` (_print working directory_) command to check if the **working directory** (= **current directory**) is `/media/<username>/VBox_GAs_<x>.<y>.<z>/`
  - If it's not, navigate there using the `cd` (_change directory_) command: `cd /media/<username>/VBox_GAs_<x>.<y>.<z>/` (use Tab completion)
  - Shell has a very useful [Tab completion](https://en.wikipedia.org/wiki/Command-line_completion) feature: When typing something, press **Tab** (once or twice) for autocompletion. It will autocomplete paths, shell commands, file names etc.
  - Use `ls` to inspect the contents of the current directory (should correspond to what you see in the File Manager)
  - Install the guest additions by running the installer with root privileges: `sudo ./VBoxLinuxAdditions.run` (using Tab completion, you can type e.g. `sudo ./VBoxL<Tab>` → will autocomplete the path; if it doesn't, you're probably in the wrong directory or mistyped something)
  - Read the output messages to make sure that the installation completed without errors. E.g., if you get the message `sudo: ./VBoxAdditions.run: command not found`, you're probably in the wrong directory
  - Eject the guest additions CD
    ([forums.virtualbox.org](https://forums.virtualbox.org/viewtopic.php?f=1&t=85799))
- **B.** Installation from the repository.
  - Not required if method A. worked
  - This method might be better suited for guest OSes that are to be managed automatically by shell scripts, e.g. Ubuntu Server
  - In the terminal: `sudo apt install virtualbox-guest-x11 virtualbox-guest-utils virtualbox-guest-dkms`
  - Note that installing the prerequisites separately is not required in this case, because the **dependencies** are installed automatically by the package manager (APT)
- Reboot the guest

How do you know that the installation was successful (apart from carefully reading all the messages in the terminal during installation)? For example, these features should work now:

- Shared clipboard (VM window menu bar → Devices → Shared Clipboard → Bidirectional): you can now copy-paste between guest and host!
  - If it still doesn't work, try to install this package: `sudo apt install virtualbox-guest-x11` (if it asks you about keeping the current file or installing the new one, select the new one: `Y`) and reboot ([superuser.com](https://superuser.com/a/1367954))
- Drag'n'Drop (after it's switched on)
- Auto-resizing the window ([docs.oracle.com](https://docs.oracle.com/en/virtualization/virtualbox/7.0/user/Introduction.html#intro-resize-window)) and full-screen view (convenient for working with the VM)
  - In case of problems ([forums.virtualbox.org](https://forums.virtualbox.org/viewtopic.php?t=91084)), see the "Troubleshooting" section below → "Graphics issues"; at any case, **increase the Video Memory** to ≥128 MB
  - If problems remain, try the alternative way of installing the guest additions ("B. Installation from the repository")

---

## VirtualBox basics

- Examine the **VirtualBox menu bar** and **status bar** (the symbols in the lower right corner of the VM window; [docs.oracle.com](https://docs.oracle.com/en/virtualization/virtualbox/7.0/user/BasicConcepts.html#user-interface))
- **Shutting down** the VM: You can do it in the [regular way](https://xubuntu.github.io/xubuntu-docs/user/C/introduction.html) from within the guest. If you close the VM window instead, you will be presented with [three shutdown options](https://www.virtualbox.org/manual/ch01.html#intro-save-machine-state); "Power off the machine" should only be used if the VM is frozen (it's a hard shutdown, like pulling the power cord)
- **Shared clipboard** (very useful): VM → Settings → General → Advanced → Shared Clipboard: Bidirectional
- Drag'n'Drop: VM → Settings → General → Advanced → Drag'n'Drop: Bidirectional
- Sometimes it's convenient to use the full-screen mode: Menu bar → View → Full-screen mode (or use the keyboard shortcut "Host+F", where they Host key is the right Ctrl key on your keyboard ([docs.oracle.com](https://docs.oracle.com/en/virtualization/virtualbox/7.0/user/Introduction.html#keyb_mouse_normal:~:text=To%20return%20ownership%20of%20keyboard%20and%20mouse%20to%20your%20host%20OS%2C%20Oracle%20VM%20VirtualBox%20reserves%20a%20special%20key%20on%20your%20keyboard%3A%20the%20Host%20key.%20By%20default%2C%20this%20is%20the%20right%20Ctrl%20key%20on%20your%20keyboard.))
- Examine the settings that are available to you in VirtualBox Manager ([docs.oracle.com](https://docs.oracle.com/en/virtualization/virtualbox/7.0/user/Introduction.html#gui-virtualboxmanager)), including the options available upon right-click on your VM (some settings are available only when the VM is shut down)

### Share a folder between the host and the guest

- A **shared folder** is an easy way to pass files between the guest and the host OS. If you **save your files in the shared folder**, you can regularly back them up together with the rest of the host, and you can delete the VM at any time without losing your data
- In VirtualBox: VM → Settings → Shared Folders → Add shared folder: select the
  folder you want to share ([websiteforstudents.com](https://websiteforstudents.com/access-virtualbox-host-folders-from-ubuntu-17-10-guest-machines/))
  - Check the checkboxes "Auto-mount" and "Make Permanent" ([superuser.com](https://superuser.com/a/1254589))
- In the guest, the shared folder should now be mounted under `/media/`; use the command `ls /media/` to double-check (shared folders have an \_sf\_\_ prefix)
  - However, if you try to look inside using `ls /media/sf_<shared-folder-name>` (use Tab completion) or the file manager, you'll probably see "Permission denied"
  - This is because every Linux file/folder has read/write/execute permissions for the **file owner**, [the **group**](https://linuxize.com/post/how-to-list-groups-in-linux/), and **other users**, so... 9 separate permissions. `ls -l /media/` shows that the owner of the shared folder is `root`, the group is `vboxsf`, and other users [don't have read/write access](http://linuxcommand.org/lc3_lts0090.php)
  - To see which groups you're part of, enter the command `groups`
  - The best way to access the shared folder is to add your user to the `vboxsf` group: `sudo adduser <username> vboxsf` (replace `<username>` by your username, e.g., if your username is `thanos`, the command is `sudo adduser thanos vboxsf`)
  - For the change to take effect, log out and log in again
  - Run `groups` again to check your groups, you should now be in the `vboxsf` group
  - The shared folder should be accessible under `/media/sf_<shared-folder-name>/`
  - Try to create a text file in this folder and access it from your host, and
    the other way around
  - Using shared folders can in rare cases lead to [strange
    bugs](https://unix.stackexchange.com/questions/52951/gedit-wont-save-a-file-on-a-virtualbox-share-text-file-busy)

---

## Troubleshooting

- Problems can be related to the guest (and need to be addressed within the guest), or to the host/VirtualBox, and addressed e.g. by changing VirtualBox settings (usually a shutdown of the guest is required)
- **Graphics issues** (display problems, freezes): Can be related to several VM display settings, VirtualBox → VM → Settings → Display (these and other settings are explained on [docs.oracle.com](https://docs.oracle.com/en/virtualization/virtualbox/7.0/user/BasicConcepts.html#settings-system))
  - **Video Memory**: Increase to 128 MB (shut down the guest first)
  - Try checking/unchecking "Enable 3D acceleration"
  - **Graphics Controller**: Try switching to VBoxSVGA or VBoxVGA (with or without 3D acceleration)
  - Try switching the guest between scaled mode and full-screen mode ([askubuntu.com](https://askubuntu.com/a/1231687))
- **Memory** (system suddenly becomes extremely slow):
  - VM → Settings → System → Base memory: Increase to at least ~4 GB
- **Sound issues**:
  - VM → Settings → Audio → **Audio Controller**, try to switch between AC97 and Intel HD Audio
  - Guest: Applications → Sound & Video → PulseAudio Volume Control, try to change some settings
  - Still sound issues: well, that's annoying. (There might be a solution, but it can be difficult to find, or you might need to wait for updates. This also explains why Linux hasn't become more popular than Windows or macOS :)
- Some **media** can't be played: install the package `ubuntu-restricted-extras` with additional media codecs and fonts ([help.ubuntu.com](https://help.ubuntu.com/community/RestrictedFormats)):
  `sudo apt install ubuntu-restricted-extras`
- Other problems:
  - Try to [categorize and isolate](https://www.virtualbox.org/manual/ch12.html#ts_categorize-isolate) the problem. **Determine in which situation** the problem occurs, e.g. does rebooting the VM help?
  - Inspect the log file `VBox.log` with diagnostic information (select the VM in the list on the left, right-click → `Show Log...`; or view it in the VM log file folder `$HOME/VirtualBox VMs/<VM-name>/Logs`) ([virtualbox.org](https://www.virtualbox.org/manual/ch12.html#collect-debug-info))
  - Use a search engine to search for the problem online. Try to describe the problem as concise as possible. E.g., if the menu bar of the VirtualBox window disappeared, and you can't select Devices → Insert guest additions CD image, you can search for "virtualbox menu bar missing"; you will usually find blogs or forum discussions on how to fix the problem (in this case, [askubuntu.com](https://askubuntu.com/questions/59103/why-has-virtualboxs-menu-disappeared) or [superuser.com](https://superuser.com/questions/1176587/i-hid-the-menu-bar-in-virtual-box-how-to-show-it-again))
- **Run a system monitor at all times** to keep track of memory usage
  and CPU load and to diagnose problems
  - Guest: Use a system monitor/task manager like a panel widget ([docs.xfce.org](https://docs.xfce.org/xfce/xfce4-panel/start#external_plugins)), the GNOME System Monitor (install
    with `sudo apt install gnome-system-monitor`),
    [`htop`](https://spin.atomicobject.com/2020/02/10/htop-guide/), or
    [Conky](https://github.com/brndnmtthws/conky/wiki)
  - Host: Use the Task Manager (Windows) or equivalent
  - High CPU load or memory usage can slow down or freeze the system. If they
    are caused by a software problem, restarting the offending program can help
- Random freezes of the guest OS → try to modify these host VM settings:
  - Display → "Enable 3D acceleration" = off
  - System → Processor → Number of virtual CPUs: 1 processor → 2, 3 or 4 processors (try and see if it helps)
  - System → Processor → "Enable PAE/NX" ([docs.oracle.com](https://docs.oracle.com/en/virtualization/virtualbox/7.0/user/BasicConcepts.html#settings-processor)): toggle this off or on, and see if it helps
  - Display → increase "Video memory" to 128 MB
  - System → Acceleration → Paravirtualization Interface: try "Minimal" or "Legacy"
  - Try a different (older) version of VirtualBox
- Still problems with the guest (freezes, high CPU load for no reason, etc.): One possibility is to try another desktop environment; recommended options are Xfce, MATE and LXQt). There are others, but they may be less performant. Installed environments can be selected in the "Session" field [at login](https://www.howtogeek.com/193129/how-to-install-and-use-another-desktop-environment-on-linux/)
- Overall slow guest OS: This shouldn't happen with Xubuntu, and is probably a host issue rather than a guest issue (e.g. not enough RAM, slow CPU, slow host OS)
- Advanced VirtualBox-related topics: e.g. [wiki.ubuntuusers.de](https://wiki.ubuntuusers.de/VirtualBox/Problembehebung/)
- Note: You will most likely encounter at least some problems with Linux; Linux was designed for system stability, transparency and customizability rather than a polished user experience
  - If the problem is Linux-related, also read the distribution [release notes](https://wiki.xubuntu.org/start?do=index) and check for known bugs and workarounds

---

## Updates

- Guest: **Update regularly** using `sudo apt update && sudo apt upgrade` or the update dialog
- Host:
  - Keep the OS updated
  - When updating VirtualBox, **completely shut down the VM** before that
    - Major (e.g. Virtualbox 5 → 6) and minor (e.g. VirtualBox 6.0 → 6.1) releases introduce new features, and can break things (e.g. prevent the VM from starting up)
    - Maintenance releases (e.g. VirtualBox 6.0.8 → 6.0.10) are bug fix releases and usually don't break things
    - In case of problems after a VirtualBox update, e.g. VM doesn't boot with an error message, **reboot the host** again (<q>have you tried turning it off and on again?</q>)
    - If you have problems with a VM after a VirtualBox update, revert to an older VirtualBox version, until the problem is fixed
    - After updating VirtualBox, update the guest additions as well, so that they match the VirtualBox version

---

## Back up your VM

Even though the whole installation and setup process can be done quickly, it's convenient to have a ready-to-go VM as backup, e.g. you can keep it on an external hard drive. If the VM you are working with breaks beyond repair, you can restore it from the backup. This is quicker than an installation from scratch. (You can perform another backup later, after installing all the necessary programs in your VM like Anaconda, VS Code etc.)

- There are multiple options for different use cases ([cloning](https://docs.oracle.com/en/virtualization/virtualbox/7.0/user/storage.html#cloningvdis), [snapshots](https://www.virtualbox.org/manual/ch01.html#snapshots), [exporting](https://superuser.com/questions/788625/sharing-a-virtualbox-image-clone-export-or-copy) and full copy of the VM folder); this is nicely explained on [YouTube](https://www.youtube.com/watch?v=jPiVasVHW8s), [forums.virtualbox.org](https://forums.virtualbox.org/viewtopic.php?f=1&t=81897), [superuser.com](https://superuser.com/questions/633431/whats-the-recommended-way-to-move-a-virtualbox-vm-to-another-computer)
- The only reliable option for a complete backup is a **full copy of the VM folder**. For this, shut down the VM and copy the VM folder (located in the folder "VirtualBox VMs" in your home directory, see [VirtualBox Manual](https://www.virtualbox.org/manual/ch10.html#vboxconfigdata), [forums.virtualbox.org](https://forums.virtualbox.org/viewtopic.php?f=6&t=81581)) to another location, e.g. an external hard drive.
- To **import** a VM, e.g. from a backup: Machine → Add → Navigate to the `.vbox` file in the VM folder ([superuser.com](https://superuser.com/questions/745844/how-can-i-import-an-existing-vbox-virtual-machine-in-virtualbox/746429))

---

## Where to go from here

Here are some ideas what you can do with your fresh and shiny Linux OS.

- Take a [quick Xubuntu tour](https://www.youtube.com/watch?v=V_gODEnrxI0)
- **Customize** your Xubuntu installation [just for fun](https://linuxhint.com/customize-xfce-desktop)
- Learn about Xubuntu software management ([xubuntu.github.io](https://xubuntu.github.io/xubuntu-docs/user/C/index.html) → "5. Software Management") and install some programs using the command line or GUIs (Start menu → search term "software")
  - Some tutorials use `apt` for **software installation**, others use [`apt-get`](https://itsfoss.com/apt-get-linux-guide/); the differences are [marginal](https://itsfoss.com/apt-vs-apt-get-difference/)
  - More info: [help.ubuntu.com](https://help.ubuntu.com/community/SoftwareManagement), [help.ubuntu.com](https://help.ubuntu.com/stable/ubuntu-help/addremove.html.en)
  - Apart from `apt`, Ubuntu increasingly uses another package management system, Snap (<a href="https://en.wikipedia.org/wiki/Snap_(software)">Wikipedia</a>, [snapcraft.io](https://snapcraft.io/about)); some applications like Firefox or Chromium are only available as snap packages. Snaps are updated automatically, or manually using the `snap refresh` command (see [snapcraft.io](https://snapcraft.io/docs/getting-started))
- Learn about the [Linux file system](http://linuxcommand.org/lc3_lts0040.php) ([YouTube tutorial](https://www.youtube.com/watch?v=HbgzrKJvDRw))
- **Learn the command line.** Even though some tasks like software installation can be done via GUIs, they are just frontends to command-line tools like `apt`, and it's preferable to use the original thing. Linux GUIs can also be buggy, because neither users nor developers like them very much
  - Take an **introductory Linux/Bash tutorial**, like [this YouTube video](https://www.youtube.com/watch?v=oxuRxtrO2Ag), [this short tutorial](https://ubuntu.com/tutorials/command-line-for-beginners) or [this comprehensive tutorial](http://linuxcommand.org/)
  - Cheat sheets like [this](https://devhints.io/bash) or [this](https://www.educative.io/blog/bash-shell-command-cheat-sheet) can help, but none will be as good as your own cheat sheet; a **text file with important commands** is a good start
  - Take [an interactive course](https://linuxsurvival.com/) or [play a game](https://overthewire.org/wargames/bandit/)
  - Get help on Bash commands using the manpages (`man ls`) or the [**TLDR** ("Too Long; Didn't Read") manpages](https://tldr.inbrowser.app/) (enter the "command name" in the corresponding box, try `ls`)
  - AI tools like ChatGPT, Microsoft Copilot or Claude are highly useful for discussing Linux and command line-related questions; as always with LLMs, you shouldn't take the results for granted especially for non-trivial questions, but always double-check them
- Learn how to use a **non-GUI text editor** like [nano](https://www.howtogeek.com/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/) or [vim](https://www.youtube.com/watch?v=ggSyF1SVFr4), you will definitely need it later
- Install Anaconda for Linux ([installation instructions](https://docs.anaconda.com/anaconda/install/linux/))
  - The [getting started](https://docs.anaconda.com/anaconda/user-guide/getting-started/) and [cheat sheet](https://docs.anaconda.com/anaconda/user-guide/cheatsheet/) sections provide basic information about Anaconda
