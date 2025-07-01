<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>Ubuntu virtualization on Apple silicon</H1>

**Note**: Please make a full backup of your computer before making any modifications.

**Important note**: For Apple Silicon computers (which have an ARM-based CPU architecture), you need software that is specifically written for this architecture. Such installers usually include ‘arm64’ or ‘aarch64’ in their file names. Not all software packages are available for all CPU architectures.

## Installation of UTM and VMware Fusion

- [UTM](https://mac.getutm.app/) is a free and open-source frontend for the open-source [QEMU](https://en.wikipedia.org/wiki/QEMU) virtualization software. QEMU is known for its broad OS compatibility, sometimes at the cost of stability and advanced features.
- [VMware Fusion](https://en.wikipedia.org/wiki/VMware_Fusion) is now also [free](https://blogs.vmware.com/cloud-foundation/2025/03/10/vmware-fusion-workstation-going-free-new-resources/) for private and commercial use. It was developed specifically for macOS by the company [VMware](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion), which is now owned by [Broadcom](https://en.wikipedia.org/wiki/Broadcom). Previously, there was a separate product, [VMware Fusion Pro](https://techdocs.broadcom.com/us/en/vmware-cis/desktop-hypervisors/fusion-pro/13-0/using-vmware-fusion.html); this is no longer the case.

Some users prefer UTM for its open-source nature and broad OS support. Others say that VMware Fusion is more stable and reliable. Both apps work well; you can try both and see which one works best for you. A popular commercial alternative is [Parallels Desktop](https://www.parallels.com/products/desktop/), but it requires a paid license. You probably don't need it, unless you have a specific application for which the free options are not suitable.

- Install UTM according to [docs.getutm.app](https://docs.getutm.app/installation/macos/)
    - Additional links: [GitHub](https://github.com/utmapp/UTM/)
- Install VMware Fusion according to [knowledge.broadcom.com](https://knowledge.broadcom.com/external/article/368667/download-and-license-information-for-vmw.html)
    - Additional links: [Broadcom forum](https://community.broadcom.com/communities/communityhomeblogs?CommunityKey=0c3a2021-5113-4ad1-af9e-018f5da40bc0)
    - The download requires creating a Broadcom account. Alternatively, you can install the [Homebrew](https://brew.sh/) package manager (also see [mac.install.guide](https://mac.install.guide/homebrew/3)), and use it to install and update other programs. For example, the command `brew install --cask utm` installs UTM ([formulae.brew.sh](https://formulae.brew.sh/cask/utm)), and the command `brew install --cask vmware-fusion` installs VMware Fusion ([formulae.brew.sh](https://formulae.brew.sh/cask/vmware-fusion)) without a Broadcom account. If you have never worked with a package manager before, it's easier to perform the installation manually, without Homebrew.

My tutorial for [installing Linux in VirtualBox](https://biodatasciencetulln.github.io/Wiki/install_linux_in_virtualbox.html) also contains important information that you should read even if you use VMWare or UTM.

## Installation of Ubuntu in UTM

- Official [documentation](https://docs.getutm.app/basics/basics/), especially the [Ubuntu guide](https://docs.getutm.app/guides/ubuntu/)
- Recommended YouTube walkthrough through the complete installation process: "Install a Linux VM in UTM \| Get Into Linux \| MacOS" by TatOG Tech, 06/2023 ([YouTube](https://www.youtube.com/watch?v=FS-HJTM6Oec)). This video provides a comprehensive guide on installing a Linux virtual machine (VM) on macOS using UTM.

Canonical currently doesn't provide an official Ubuntu Desktop release for platforms other than [x86_64](https://www.techtarget.com/whatis/definition/x86-64) and Raspberry Pi. The best approach to set up Ubuntu Desktop on an ARM-based Mac is to install **Ubuntu Server** for ARM and then convert it to Ubuntu Desktop by installing additional software, the **desktop environment**. This is currently the preferred method for both UTM and VMware Fusion. You will need the ISO file of the latest [Ubuntu Server](https://ubuntu.com/download/server/arm) LTS release, currently 24.04.

- "Server" just means that the downloaded operating system (OS) doesn't have a desktop environment/GUI.
- Generally, you don't have to use the Ubuntu LTS (Long-Term Support) version, but the [extended support](https://ubuntu.com/about/release-cycle) is convenient, and many tutorials are oriented towards LTS versions.

Notes related to the YouTube walkthrough:

- You can leave the virtual drive size at 64 GB (default setting), or increase it to ~80-100 GB (recommended).
- The "shared directory" is a macOS directory that the VM will be able to access (you can also add it later).
- For Ubuntu, it's currently recommended to install Ubuntu Server ([ubuntu.com](https://ubuntu.com/download/server/arm)) and add the GUI ("graphical user interface", i.e. the desktop environment) in the next step, rather than directly installing Ubuntu Desktop ([askubuntu.com](https://askubuntu.com/questions/1405124/install-ubuntu-desktop-22-04-arm64-on-macos-apple-silicon-m1-pro-max-in-parall), not recommended).
  - On Apple Silicon, you need software intended for ARM architecture; x86 installers won't work, unless you use UTM "Emulation" instead of "Virtualization", which is much slower.
- Create a new virtual machine (VM) and run the Ubuntu installer as shown in the YouTube video.
  - During the installation, you are presented with some scary-sounding options, but remember that the installation happens only within the VM, so you can always repeat it if something doesn't work. The default settings are fine ([ubuntu.com](https://ubuntu.com/server/docs/install/step-by-step)).
- At 9:40 in the video, he uses the program SSH (the command `ssh username@ip-address`) to log in to the VM without the UTM GUI, just via the command line. This has the same effect as opening a terminal in the VM, and entering commands there. You can try this, even if a GUI (interacting with the VM via the UTM window) is probably more familiar for you.
  - Note that you cannot run graphical applications via SSH without an additional option `-X`, which enables [X11 forwarding](https://unix.stackexchange.com/questions/12755/how-to-forward-x-over-ssh-to-run-graphics-applications-remotely), also see [unix.stackexchange.com](https://unix.stackexchange.com/questions/566/how-does-ssh-x-function). If you want to run graphical applications, simply do it directly in the UTM window, not via SSH.
- The next step is to install system updates via `sudo apt update && sudo apt upgrade`; this is explained in detail in the [VirtualBox tutorial](install_linux_in_virtualbox.md).
- Installing the `qemu-guest-agent` and `spice-vdagent` packages is explained in the [UTM docs](https://docs.getutm.app/guest-support/linux/); this is the equivalent of VirtualBox guest additions.
  - The QEMU guest agent is a program intended to run in the background in VMs that use the QEMU hypervisor ([qemu-project.gitlab.io](https://qemu-project.gitlab.io/qemu/interop/qemu-ga.html)).
  - The SPICE agent is another helper program (technical details: [spice-space.org](https://www.spice-space.org/index.html), [manpages.ubuntu.com](https://manpages.ubuntu.com/manpages/lunar/man1/spice-vdagent.1.html)).
- Apart from the GNOME desktop (installed via the package `ubuntu-desktop`), there are other desktop environments like Xfce ([howtogeek.com](https://www.howtogeek.com/193129/how-to-install-and-use-another-desktop-environment-on-linux/), which can be installed via `sudo apt install xubuntu-desktop` instead of `ubuntu-desktop`. This is a matter of taste.
- Set up a shared folder according to the instructions in [docs.getutm.app](https://docs.getutm.app/guest-support/linux/#virtfs).
- Note that during startup of your VM you may briefly see some log messages ([askubuntu.com](https://askubuntu.com/questions/982632/what-are-the-messages-i-see-during-the-startup-shutdown-process-of-ubuntu)) and possibly even some error messages; this is part of the normal boot process.
- If you get a warning about low disk space, inspect the disk usage in the [disk usage analyzer](https://help.gnome.org/users/baobab/stable/); did you select an appropriate disk size when configuring the VM in UTM?

### Problems?

- Try searching for the respective issue
  - on GitHub ([UTM issues](https://github.com/utmapp/UTM/issues), [UTM discussions](https://github.com/utmapp/UTM/discussions/))
  - on Reddit (via Google: simply add `reddit` to your search query, or `site:reddit.com`, see [techlicious.com](https://www.techlicious.com/tip/google-search-tips-everone-should-know/))
  - on Google
- Display resolution: in case of problems, try to set another resolution in the VM settings, e.g. 1440x900
- If the VM freezes regularly, try changing the "Emulated Display Card" in the VM Display settings, e.g. to virtio-ramfb ([forums.macrumors.com](https://forums.macrumors.com/threads/utm-virtualisation-of-ubuntu-20-04-randomly-freezes-on-apple-silicon-m2.2388950/))

### Additional links

- Ubuntu server tutorial and How-to guides: [ubuntu.com](https://documentation.ubuntu.com/server/tutorial/)
- Blogs:
  - [sachin-the-learner.hashnode.dev](https://sachin-the-learner.hashnode.dev/install-ubuntu-using-utm-on-mac)
  - [medium.com](https://medium.com/@lizrice/linux-vms-on-an-m1-based-mac-with-vscode-and-utm-d73e7cb06133)

### Additional notes for hackers

- The Ubuntu installer sets up an "LVM partitioning scheme". More information:
  - [ubuntu.com](https://ubuntu.com/server/docs/install/storage)
  - [digitalocean.com](https://www.digitalocean.com/community/tutorials/an-introduction-to-lvm-concepts-terminology-and-operations) - introduction to LVM concepts
  - [discourse.ubuntu.com](https://discourse.ubuntu.com/t/how-is-the-size-of-the-lvm-container-decided/24608)
  - [askubuntu.com](https://askubuntu.com/questions/1269493/how-to-make-lv-use-all-disk-space-in-pv)
- In some cases, you will need to change the VM settings in UTM
  - For example, if you use a VPN on your host machine, you may need to change the network mode to "Emulated VLAN" to be able to connect to the internet from within the VM ([UTM docs](https://docs.getutm.app/settings-qemu/devices/network/network/), [GitHub](https://github.com/utmapp/UTM/issues/3238))
- Ubuntu is not the only Linux distro that can be run on UTM ([docs.getutm.app](https://docs.getutm.app/guides/guides/))
- UTM can also run Windows VMs, see e.g. [eshop.macsales.com](https://eshop.macsales.com/blog/72081-utm-virtual-machine-on-m1-mac/) (07/2021)

## Installation of Ubuntu in VMware Fusion

- Recommended YouTube walkthrough: "How to install Ubuntu on Macbook M1 or M2 Using VMWare Fusion" by Murphy Tsai, 05/2023 ([YouTube](https://www.youtube.com/watch?v=4dFy-4pw8NA))
- [Companion guide](https://community.broadcom.com/vmware-cloud-foundation/viewdocument/the-unofficial-fusion-for-apple-sil): version 32 at the time of writing; you need only the "Ubuntu" section from the guide
- Note: The companion guide suggests installing `ubuntu-desktop` or `ubuntu-desktop-minimal`, which installs the [GNOME desktop](https://www.reddit.com/r/gnome/comments/9do3s1/please_tell_in_simple_term_what_is_gnome_will_i/). After installing the GNOME desktop, you can customize the resolution as explained in [this video](https://youtu.be/kDosGTdwqO0?t=610). 
  - Instead of `ubuntu-desktop`, you could also install `xubuntu-desktop`, which installs the XFCE desktop (and thus, effectively, Xubuntu). However, setting a high resolution didn't work for me in Xubuntu; after setting the "scaling" option to 200%, the screen remained black. Therefore, this is currently not recommended. You will often encounter different sorts of problems like this, especially in non-standard configurations. Just be mindful about this, and don't let it discourage you.
- Ubuntu has additional useful settings. For example, you can visit [extensions.gnome.org](https://extensions.gnome.org/) to learn more about GNOME extensions, and install e.g. a system monitor like [this one](https://extensions.gnome.org/extension/6807/system-monitor/).
- After setting up the VM, you can make a complete backup of the VM as explained in the [best practices](https://knowledge.broadcom.com/external/article/303386/#:~:text=There%20is%20no,back%20it%20up.) for virtual machine backup (programs and data) in VMware Fusion. For instructions how to locate the VM file for backup, see [here](https://knowledge.broadcom.com/external/article/344570/locating-the-virtual-machine-bundle-in-v.html).
  - It's good practice to backup the VM in regular time intervals, so that you can quickly revert to the last working version if needed.

### Problems and solutions

Below are examples of encountered problems.

- After the installation of the OS, one keyboard key didn't work.
  - Solution: Debugging together with Claude showed that deactivating the checkbox "Enable Mac OS Host Keyboard Shortcuts" ([techdocs.broadcom.com](https://techdocs.broadcom.com/us/en/vmware-cis/desktop-hypervisors/fusion-pro/13-0/using-vmware-fusion/configuring-vmware-fusion/setting-fusion-preferences/enable-or-disable-mac-os-shortcuts-on-the-keyboard-and-mouse-preference-pane.html)) fixed the problem. This option allows the host system to intercept key presses before they reach the guest OS. In case of other key mapping problems, see [this thread](https://community.broadcom.com/vmware-cloud-foundation/discussion/dead-keys-on-host-system-prevent-vmware-guest-from-receiving-keystrokes-at-all). If you want to use the same key bindings in the VM as on the host, you can add additional key mappings, e.g. <kbd>⌘</kbd> → <kbd>Ctrl</kbd>, and <kbd>⌘</kbd> + <kbd>Tab</kbd> → <kbd>Alt</kbd> + <kbd>Tab</kbd>, as explained [here](https://community.broadcom.com/vmware-cloud-foundation/discussion/dead-keys-on-host-system-prevent-vmware-guest-from-receiving-keystrokes-at-all#:~:text=Command%2DTab%20%C2%A0%2D%3E%20Alt,removes%20windows%20key). One possible (untested) alternative is a project like [toshy](https://github.com/RedBearAK/toshy). In all cases, you should clearly differentiate between the host system, the VMware application, and the guest system, to clearly understand who does what. For example, the key mappings are managed by VMware, while the keyboard layout within the guest is something else entirely and managed by the guest OS, which doesn't involve the host or VMware.
- Key combination <kbd>⌘</kbd> + <kbd>F</kbd> didn't work as expected in the text editor.
  - Solution: See the problem above. Deactivating the key mapping <kbd>⌘</kbd> + <kbd>F</kbd> in the preset VMware keyboard settings fixed the issues.
- The default terminal text size was too small, and the window size was inconvenient.
  - Solution: The default font and terminal size were set in the preferences of the Terminal app.
- The dock was inconvenient to use, because it was located at the same side as the macOS dock.
  - Solution: [Dock](https://askubuntu.com/questions/1332616/whats-the-difference-between-dash-and-dock) settings were discovered using the [search bar](https://itsfoss.com/gnome-search/). The dock location was changed, icons were resized, and auto-hide was enabled. After installing [GNOME extensions](https://extensions.gnome.org/), more fine-grained settings like "pressure threshold" for "intelligent autohide" were available, and were set to more convenient values. One alternative approach is to replace the built-in [Ubuntu dock](https://extensions.gnome.org/extension/1300/ubuntu-dock/) extension by the [Dash to Panel](https://extensions.gnome.org/extension/1160/dash-to-panel/) extension.
- The shared folder wasn't accessible ("mounted") in the VM. (When mounted correctly, the folder should be visible if you execute the command `ls /mnt/hgfs` in the terminal.)
  - Solution: See section "Shared folders do not automatically mount" in the "Unofficial Fusion for Apple Silicon Companion Guide". A temporary solution was to uncheck and then again check the box "Enable Shared Folders" in the VM settings. A permanent solution requires to modify a system file (`/etc/fstab`) and reboot. After this, you can execute the command `ln -s /mnt/hgfs/<shared folder>`, which creates a "symbolic link" in your home directory to the shared folder. This allows to conveniently access the folder, e.g. via the Files app.
- Using the touch ID for unlocking the VM is not possible.
  - Solution: This is currently not possible. To make using the VM more convenient, you can change other settings, e.g. disable automatic screen lock.
- After quitting and restarting VMware, it asks if you moved or copied the VM.
  - Solution: See [this thread](https://community.broadcom.com/vmware-cloud-foundation/question/after-macos-15sequoia-repetitive-asks-if-ive-moved-or-copied-the-file). As a temporary solution, you can simply answer "moved" every time it asks.
- The time in the VM was wrong (UTC time, not local time), even though [time synchronization](https://knowledge.broadcom.com/external/article/344340/enabling-time-synchronization-between-th.html) was enabled.
  - Solution: Additional [research](https://community.broadcom.com/communities/community-home/digestviewer/viewthread?GroupId=7171&MessageKey=adc94593-6490-4b59-9ad3-e77da294d831&CommunityKey=fb707ac3-9412-4fad-b7af-018f5da56d9f#:~:text=Generally%20speaking%2C%20time%20synchronization%20is%20only%20applied%20to%20system%20time%20which%20should%20be%20on%20the%20UTC%20time%20scale%2C%20and%20time%20zone%20/%20day%20light%20savings%20are%20managed%20by%20the%20OS%20as%20offsets.) showed that the time synchronization is only applied to system time which should be on the UTC time scale, and time zone / day light savings are managed by the OS as offsets. A search for "time zone" in the Ubuntu activities search bar, and setting the correct time zone in the settings fixed the issue.
- VMware process `vmnet-natd` runs at 100% CPU (see e.g. [community.broadcom.com](https://community.broadcom.com/vmware-cloud-foundation/discussion/1220-high-cpu-vmnet-natd)).
  - Solution: Requires further investigation, see e.g. "Understanding networking types in VMware Fusion" ([knowledge.broadcom.com](https://knowledge.broadcom.com/external/article/303393/understanding-networking-types-in-vmware.html)) and "How does networking inside a virtual machine work?" ([community.broadcom.com](https://community.broadcom.com/vmware-cloud-foundation/viewdocument/understanding-networking-in-vmware?CommunityKey=0c3a2021-5113-4ad1-af9e-018f5da40bc0&tab=librarydocuments)). Try switching to bridged mode.
 
**Hint**: If the given explanations are too brief or technical, or a command doesn't work as expected, you can discuss them with an LLM like Gemini, Claude or ChatGPT.

The GNOME philosophy differs from more traditional desktops like XFCE. It focuses on minimalism and touchscreen-friendliness, whereas XFCE and other traditional desktops prefer a conventional, menu-driven interface akin to older Windows versions, offering extensive customization and a lighter resource footprint. Especially on GNOME, keyboard shortcuts can significantly boost your productivity. For instance, Super (Windows key) opens the activities overview, and Alt + Tab allows to quickly switch between open windows.

## Installation of Anaconda

- For installing Anaconda in the Linux VM, download the `Linux-aarch64` installer (it has a filename like `Anaconda3-202x.xx-Linux-aarch64.sh` on [anaconda.com](https://www.anaconda.com/download#download))
- The installation instructions are found in the official documentation, on [docs.anaconda.com](https://docs.anaconda.com/anaconda/install/)); read them carefully and follow them step by step
  - If some of the software packages listed in the "Prerequisites" section ([docs.anaconda.com](https://docs.anaconda.com/anaconda/install/linux/)) can't be installed (e.g. because the package is not found), install only those packages for which it's possible
- In case of problems, you can also install Anaconda directly on the host system, just make sure to use the right installer ("Apple silicon")
