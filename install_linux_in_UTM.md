<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>Ubuntu virtualization via UTM on Apple silicon</H1>

**Note**: Please make a full backup of your computer before making any modifications.

## Installation

A nice walkthrough through the complete installation process is given in the video "Install a Linux VM in UTM \| Get Into Linux \| MacOS" by TatOG Tech, 2023 ([YouTube](https://www.youtube.com/watch?v=FS-HJTM6Oec)). Additional notes:

- If you have a large enough hard drive, you can leave the virtual drive size at 64 GB (default setting)
- The "shared directory" is a macOS directory that the VM will be able to access; you can also add it later
- For Ubuntu, currently it's recommended to install Ubuntu Server ([ubuntu.com](https://ubuntu.com/download/server/arm)) and add the GUI ("graphical user interface", i.e. the desktop environment) in the next step, rather than directly installing Ubuntu Desktop ([askubuntu.com](https://askubuntu.com/questions/1405124/install-ubuntu-desktop-22-04-arm64-on-macos-apple-silicon-m1-pro-max-in-parall), not recommended)
  - "server" just means that the downloaded operating system doesn't have a desktop environment/GUI
  - you don't have to use the Ubuntu LTS version, but it will make life easier, as updates are provided for a longer time, and many tutorials are oriented towards LTS versions
  - on Apple Silicon, you need files intended for ARM architecture, x86 installers won't work (unless you use UTM "Emulation" instead of "Virtualization", which is much slower)
- Create a new virtual machine (VM) and run the Ubuntu installer as shown in the YouTube video
  - during the installation, you are presented with some scary-sounding options, but remember that the installation happens only within the VM, so you can always repeat it if something doesn't work; the default settings are fine ([ubuntu.com](https://ubuntu.com/server/docs/install/step-by-step))
- At 9:40 in the video, he uses the program SSH (the command `ssh username@ip-address`) to log in to the VM without the UTM GUI, just via the command line. This has the same effect as opening a terminal in the VM, and entering commands there. You can try this, even if a GUI (interacting with the VM via the UTM window) is probably more familiar for you
- The next step is to install system updates via `sudo apt update && sudo apt upgrade`, this is explained in detail in the [VirtualBox tutorial](install_linux_in_virtualbox.md)
- Installing the `qemu-guest-agent` and `spice-vdagent` packages is explained in the [UTM docs](https://docs.getutm.app/guest-support/linux/); this is the equivalent of VirtualBox guest additions
  - the QEMU guest agent is a program intended to run in the background in VMs that use the QEMU hypervisor ([qemu-project.gitlab.io](https://qemu-project.gitlab.io/qemu/interop/qemu-ga.html))
  - the SPICE agent is another helper program (technical details: [spice-space.org](https://www.spice-space.org/index.html), [manpages.ubuntu.com](https://manpages.ubuntu.com/manpages/lunar/man1/spice-vdagent.1.html))
- Apart from the GNOME desktop (installed via the package `ubuntu-desktop`), there are other desktop environments like Xfce ([howtogeek.com](https://www.howtogeek.com/193129/how-to-install-and-use-another-desktop-environment-on-linux/)), this is a matter of taste
- Set up a shared folder according to the instructions in [docs.getutm.app](https://docs.getutm.app/guest-support/linux/#virtfs)
- Note that during startup of your VM you may briefly see some log messages ([askubuntu.com](https://askubuntu.com/questions/982632/what-are-the-messages-i-see-during-the-startup-shutdown-process-of-ubuntu)) and possibly even some error messages, this is part of the normal boot process
- If you get a message about not enough free space, inspect the disk usage in the [disk usage analyzer](https://help.gnome.org/users/baobab/stable/); did you select an appropriate disk size when configuring the VM in UTM?

## Problems?

- Try to search for the respective issue
  - on GitHub ([UTM issues](https://github.com/utmapp/UTM/issues), [UTM discussions](https://github.com/utmapp/UTM/discussions/))
  - on Reddit (via Google using `site:reddit.com`, [techlicious.com](https://www.techlicious.com/tip/google-search-tips-everone-should-know/))
  - on Google
- Display resolution: in case of problems, try to set another resolution in the VM settings, e.g. 1440x900
- If the VM freezes regularly, try changing the "Emulated Display Card" in the VM Display settings, e.g. to virtio-ramfb ([forums.macrumors.com](https://forums.macrumors.com/threads/utm-virtualisation-of-ubuntu-20-04-randomly-freezes-on-apple-silicon-m2.2388950/))

## Additional links

- UTM docs:
  - [docs.getutm.app](https://docs.getutm.app/guides/ubuntu/)
  - [mac.getutm.app gallery](https://mac.getutm.app/gallery/ubuntu-20-04)
- Ubuntu server tutorials/installation:
  - [ubuntu.com](https://ubuntu.com/server/docs/tutorials)
- Blogs:
  - [sachin-the-learner.hashnode.dev](https://sachin-the-learner.hashnode.dev/install-ubuntu-using-utm-on-mac)
  - [medium.com](https://medium.com/@lizrice/linux-vms-on-an-m1-based-mac-with-vscode-and-utm-d73e7cb06133)

## Additional notes for hackers

- The Ubuntu installer sets up an LVM partitioning scheme, here are some more details:
  - [ubuntu.com](https://ubuntu.com/server/docs/install/storage)
  - [digitalocean.com](https://www.digitalocean.com/community/tutorials/an-introduction-to-lvm-concepts-terminology-and-operations) - introduction to LVM concepts
  - [discourse.ubuntu.com](https://discourse.ubuntu.com/t/how-is-the-size-of-the-lvm-container-decided/24608)
- In some cases, you will need to change the VM settings it UTM
  - for example, if you use a VPN on your host machine, you may need to change the network mode to "Emulated VLAN" to be able to connect to the internet from within the VM ([UTM docs](https://docs.getutm.app/settings-qemu/devices/network/network/), [GitHub](https://github.com/utmapp/UTM/issues/3238))
- Ubuntu is not the only Linux distro that can be run on UTM ([docs.getutm.app](https://docs.getutm.app/guides/guides/))
- UTM can also run Windows VMs, see e.g. [eshop.macsales.com](https://eshop.macsales.com/blog/72081-utm-virtual-machine-on-m1-mac/) (07/2021)
