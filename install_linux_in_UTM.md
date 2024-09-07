<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>Ubuntu virtualization on Apple silicon</H1>

**Note**: Please make a full backup of your computer before making any modifications.

VirtualBox is not available for Apple silicon. Alternatives are:

- [VMware Fusion Pro](https://knowledge.broadcom.com/external/article/368667/download-and-license-information-for-vmw.html): free for personal use
- [UTM](https://mac.getutm.app/): open source
- UTM and VMware Fusion Pro both work well; you can also try out both, and stick to the one that works best for you
- A commercial alternative is [Parallels Desktop](https://www.parallels.com/products/desktop/), which is popular, but requires a paid license
- Note that my tutorial for [installing Linux in VirtualBox](https://biodatasciencetulln.github.io/Wiki/install_linux_in_virtualbox.html) is mostly oriented towards VirtualBox, but also contains universally useful information, which you should read

Important note: For Apple Silicon computers (ARM-based CPU architecture), you need software that is specifically written for this architecture. Such installers usually include ‘arm64’ or ‘aarch64’ in their file names.

Canonical does not provide an official Ubuntu Desktop release for platforms other than x86_64 and Raspberry Pi. The best approach to set up Ubuntu Desktop on ARM is to install Ubuntu Server for ARM and then convert it to Ubuntu Desktop by installing additional software (the desktop environment). This is currently the preferred method with both UTM and VMware Fusion. You will need the ISO file of the latest [Ubuntu Server](https://ubuntu.com/download/server/arm) LTS release (currently 24.04).

## Installation in UTM

Links:

- [UTM homepage](https://mac.getutm.app/) and [GitHub](https://github.com/utmapp/UTM/)
- Official [documentation](https://docs.getutm.app/basics/basics/), especially the [Ubuntu guide](https://docs.getutm.app/guides/ubuntu/)
- Recommended YouTube walkthrough through the complete installation process: "Install a Linux VM in UTM \| Get Into Linux \| MacOS" by TatOG Tech, 06/2023 ([YouTube](https://www.youtube.com/watch?v=FS-HJTM6Oec)).

Additional notes:

- If you have a large enough hard drive, you can leave the virtual drive size at 64 GB (default setting)
- The "shared directory" is a macOS directory that the VM will be able to access; you can also add it later
- For Ubuntu, currently it's recommended to install Ubuntu Server ([ubuntu.com](https://ubuntu.com/download/server/arm)) and add the GUI ("graphical user interface", i.e. the desktop environment) in the next step, rather than directly installing Ubuntu Desktop ([askubuntu.com](https://askubuntu.com/questions/1405124/install-ubuntu-desktop-22-04-arm64-on-macos-apple-silicon-m1-pro-max-in-parall), not recommended)
  - "server" just means that the downloaded operating system doesn't have a desktop environment/GUI
  - you don't have to use the Ubuntu LTS version, but it will make life easier, as updates are provided for a longer time, and many tutorials are oriented towards LTS versions
  - on Apple Silicon, you need files intended for ARM architecture, x86 installers won't work (unless you use UTM "Emulation" instead of "Virtualization", which is much slower)
- Create a new virtual machine (VM) and run the Ubuntu installer as shown in the YouTube video
  - during the installation, you are presented with some scary-sounding options, but remember that the installation happens only within the VM, so you can always repeat it if something doesn't work; the default settings are fine ([ubuntu.com](https://ubuntu.com/server/docs/install/step-by-step))
- At 9:40 in the video, he uses the program SSH (the command `ssh username@ip-address`) to log in to the VM without the UTM GUI, just via the command line. This has the same effect as opening a terminal in the VM, and entering commands there. You can try this, even if a GUI (interacting with the VM via the UTM window) is probably more familiar for you
  - Note that you cannot run graphical applications via SSH without an additional option `-X`, which enables [X11 forwarding](https://unix.stackexchange.com/questions/12755/how-to-forward-x-over-ssh-to-run-graphics-applications-remotely), also see [here](https://unix.stackexchange.com/questions/566/how-does-ssh-x-function); if you want to run graphical applications, simply do it directly in the UTM window, not via SSH
- The next step is to install system updates via `sudo apt update && sudo apt upgrade`, this is explained in detail in the [VirtualBox tutorial](install_linux_in_virtualbox.md)
- Installing the `qemu-guest-agent` and `spice-vdagent` packages is explained in the [UTM docs](https://docs.getutm.app/guest-support/linux/); this is the equivalent of VirtualBox guest additions
  - the QEMU guest agent is a program intended to run in the background in VMs that use the QEMU hypervisor ([qemu-project.gitlab.io](https://qemu-project.gitlab.io/qemu/interop/qemu-ga.html))
  - the SPICE agent is another helper program (technical details: [spice-space.org](https://www.spice-space.org/index.html), [manpages.ubuntu.com](https://manpages.ubuntu.com/manpages/lunar/man1/spice-vdagent.1.html))
- Apart from the GNOME desktop (installed via the package `ubuntu-desktop`), there are other desktop environments like Xfce ([howtogeek.com](https://www.howtogeek.com/193129/how-to-install-and-use-another-desktop-environment-on-linux/)), this is a matter of taste
- Set up a shared folder according to the instructions in [docs.getutm.app](https://docs.getutm.app/guest-support/linux/#virtfs)
- Note that during startup of your VM you may briefly see some log messages ([askubuntu.com](https://askubuntu.com/questions/982632/what-are-the-messages-i-see-during-the-startup-shutdown-process-of-ubuntu)) and possibly even some error messages, this is part of the normal boot process
- If you get a warning about low disk space, inspect the disk usage in the [disk usage analyzer](https://help.gnome.org/users/baobab/stable/); did you select an appropriate disk size when configuring the VM in UTM?

### Problems?

- Try to search for the respective issue
  - on GitHub ([UTM issues](https://github.com/utmapp/UTM/issues), [UTM discussions](https://github.com/utmapp/UTM/discussions/))
  - on Reddit (via Google using `site:reddit.com`, [techlicious.com](https://www.techlicious.com/tip/google-search-tips-everone-should-know/))
  - on Google
- Display resolution: in case of problems, try to set another resolution in the VM settings, e.g. 1440x900
- If the VM freezes regularly, try changing the "Emulated Display Card" in the VM Display settings, e.g. to virtio-ramfb ([forums.macrumors.com](https://forums.macrumors.com/threads/utm-virtualisation-of-ubuntu-20-04-randomly-freezes-on-apple-silicon-m2.2388950/))

### Additional links

- Ubuntu server tutorials/installation:
  - [ubuntu.com](https://ubuntu.com/server/docs/tutorials)
- Blogs:
  - [sachin-the-learner.hashnode.dev](https://sachin-the-learner.hashnode.dev/install-ubuntu-using-utm-on-mac)
  - [medium.com](https://medium.com/@lizrice/linux-vms-on-an-m1-based-mac-with-vscode-and-utm-d73e7cb06133)

### Additional notes for hackers

- The Ubuntu installer sets up an LVM partitioning scheme, here are some more details:
  - [ubuntu.com](https://ubuntu.com/server/docs/install/storage)
  - [digitalocean.com](https://www.digitalocean.com/community/tutorials/an-introduction-to-lvm-concepts-terminology-and-operations) - introduction to LVM concepts
  - [discourse.ubuntu.com](https://discourse.ubuntu.com/t/how-is-the-size-of-the-lvm-container-decided/24608)
- In some cases, you will need to change the VM settings in UTM
  - For example, if you use a VPN on your host machine, you may need to change the network mode to "Emulated VLAN" to be able to connect to the internet from within the VM ([UTM docs](https://docs.getutm.app/settings-qemu/devices/network/network/), [GitHub](https://github.com/utmapp/UTM/issues/3238))
- Ubuntu is not the only Linux distro that can be run on UTM ([docs.getutm.app](https://docs.getutm.app/guides/guides/))
- UTM can also run Windows VMs, see e.g. [eshop.macsales.com](https://eshop.macsales.com/blog/72081-utm-virtual-machine-on-m1-mac/) (07/2021)

## Installation in VMware Fusion

- VMware Fusion Pro: [blogs.vmware.com](https://blogs.vmware.com/teamfusion/2024/05/fusion-pro-now-available-free-for-personal-use.html), [knowledge.broadcom.com](https://knowledge.broadcom.com/external/article/368667/download-and-license-information-for-vmw.html) (also see [reddit](https://www.reddit.com/r/vmware/comments/1cry8ej/comment/l426xtq/))
- Recommended YouTube walkthrough for installing Ubuntu in the virtual machine: "How to install Ubuntu on Macbook M1 or M2 Using VMWare Fusion" by Murphy Tsai, 05/2023 ([YouTube](https://www.youtube.com/watch?v=4dFy-4pw8NA))
- [Companion guide](https://community.broadcom.com/vmware-cloud-foundation/discussion/version-28-of-the-fusion-companion-guide-is-now-available): v28 at the time of writing; you need only the "Ubuntu" section from the guide
- [Forum](https://community.broadcom.com/communities/communityhomeblogs?CommunityKey=0c3a2021-5113-4ad1-af9e-018f5da40bc0)

## Installation of Anaconda

- For installing Anaconda in the Linux VM, download the `Linux-aarch64` installer (it has a filename like `Anaconda3-202x.xx-Linux-aarch64.sh` on [anaconda.com](https://www.anaconda.com/download#download))
- The installation instructions are found in the official documentation, on [docs.anaconda.com](https://docs.anaconda.com/anaconda/install/)); read them carefully and follow them step by step
  - If some of the software packages listed in the "Prerequisites" section ([docs.anaconda.com](https://docs.anaconda.com/anaconda/install/linux/)) can't be installed (e.g. because the package is not found), install only those packages for which it's possible
- In case of problems, you can always install Anaconda directly on macOS, just make sure to use the right installer ("Apple silicon")
 
