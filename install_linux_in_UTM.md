# Ubuntu virtualization via UTM on Apple silicon

## Links and instructions

- UTM docs:
  - [docs.getutm.app](https://docs.getutm.app/guides/ubuntu/)
  - [mac.getutm.app/gallery/ubuntu](https://mac.getutm.app/gallery/ubuntu-20-04)
- Ubuntu server tutorials/installation:
  - [ubuntu.com](https://ubuntu.com/server/docs/tutorials)
- Blogs:
  - [sachin-the-learner.hashnode.dev](https://sachin-the-learner.hashnode.dev/install-ubuntu-using-utm-on-mac)
  - [medium.com](https://medium.com/@lizrice/linux-vms-on-an-m1-based-mac-with-vscode-and-utm-d73e7cb06133)
  - [eshop.macsales.com](https://eshop.macsales.com/blog/72081-utm-virtual-machine-on-m1-mac/)

## Installation

A very nice walkthrough through the complete installation process is given in the video "Install a Linux VM in UTM | Get Into Linux | MacOS" by TatOG Tech, 2023 ([YouTube](https://www.youtube.com/watch?v=FS-HJTM6Oec)). Additional notes:

- If you have enough space on your computer, leave the drive size at 64 GB (default setting)
- The "shared directory" is a macOS directory that the VM will be able to access; you can also add it later
- For Ubuntu, currently it's recommended to install Ubuntu Server ([ubuntu.com](https://ubuntu.com/download/server/arm)) and add the GUI (desktop environment) in the next step, rather than directly installing Ubuntu Desktop ([askubuntu.com](https://askubuntu.com/questions/1405124/install-ubuntu-desktop-22-04-arm64-on-macos-apple-silicon-m1-pro-max-in-parall), not recommended)
  - "server" just means that the downloaded operating system doesn't have a desktop environment/GUI
  - you don't have to use the Ubuntu LTS version, but it will make life easier, as updates are provided for a longer time, and many tutorials are oriented towards LTS versions
  - on Apple Silicon, you need files intended for ARM architecture, x86 installers won't work (unless you use "Emulation" instead of "Virtualization", which is much slower)
- Create a new virtual machine (VM) and run the Ubuntu installer like described in the YouTube video
  - During the installation, you are presented with some scary-sounding options, but the defaults are fine ([ubuntu.com](https://ubuntu.com/server/docs/install/step-by-step))
- At 9:40 in the video, he is using the program SSH (the command is `ssh username@ip-address`) to log in to the VM without the UTM GUI, just via the command line; you should absolutely try this, even though a GUI (interacting with the VM via the UTM window) will probably be more familiar
- The next step is to install system updates via `sudo apt update && sudo apt upgrade`, this is explained in detail in the [VirtualBox tutorial](install_linux_in_virtualbox.md)
- Installing the `quemu-guest-agent` and `spice-vdagennt` packages is explained in the [UTM docs](https://docs.getutm.app/guest-support/linux/)
  - the Qemu guest agent is a program intended to run in the background in VMs that use the QEMU hypervisor ([qemu-project.gitlab.io](https://qemu-project.gitlab.io/qemu/interop/qemu-ga.html))
  - the SPICE agent is another helper program (technical details: [spice-space.org](https://www.spice-space.org/index.html), [manpages.ubuntu.com](https://manpages.ubuntu.com/manpages/lunar/man1/spice-vdagent.1.html))
- Apart from the GNOME desktop (installed via the package `ubuntu-desktop`), there are alternatives like Xfce or Cinnamon ([computingforgeeks.com](https://computingforgeeks.com/how-to-install-cinnamon-desktop-environment-on-debian/)), this is a matter of taste
- Set up a shared folder according to instructions in [docs.getutm.app](https://docs.getutm.app/guest-support/linux/#virtfs)

## Problems?

- Try to search for the respective issue:
  - on GitHub ([UTM issues](https://github.com/utmapp/UTM/issues), [UTM discussions](https://github.com/utmapp/UTM/discussions/))
  - on Reddit (via Google using `site:reddit.com`, [techlicious.com](https://www.techlicious.com/tip/google-search-tips-everone-should-know/))
  - on Google
- Resolution: in case of problems, try another resolution, e.g. 1440x900

## Additional notes for hackers

- Ubuntu is not the only Linux distribution that can be run on UTM ([docs.getutm.app](https://docs.getutm.app/guides/guides/))
- The Ubuntu installer sets up an LVM partitioning scheme, here are some more details:
  - [ubuntu.com](https://ubuntu.com/server/docs/install/storage)
  - [digitalocean.com](https://www.digitalocean.com/community/tutorials/an-introduction-to-lvm-concepts-terminology-and-operations) - introduction to LVM concepts
  - [discourse.ubuntu.com](https://discourse.ubuntu.com/t/how-is-the-size-of-the-lvm-container-decided/24608)
