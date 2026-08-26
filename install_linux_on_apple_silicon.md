<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>Ubuntu virtualization on Apple silicon</H1>

* TOC
{:toc}

For Apple Silicon computers (which have an ARM-based CPU architecture), you need software that is specifically written for this architecture. Such installers usually include **arm64** or **aarch64** in their file names. Not all software packages are available for all CPU architectures. While VirtualBox recently added support for Apple Silicon, it's still in its early days and not widely adopted yet. We'll use more well-established solutions.

**Note**: Please make a full backup of your computer before making any modifications.

## Which virtualization software?

**Use [UTM](https://mac.getutm.app/).** It is free and open-source, needs no user account to download, and runs ARM Linux natively on your ARM Mac. UTM is a frontend for the open-source [QEMU](https://en.wikipedia.org/wiki/QEMU) virtualization software, which is known for its **broad OS compatibility**.

Two alternatives (which you usually don't need):

- [VMware Fusion](https://en.wikipedia.org/wiki/VMware_Fusion) is also [free](https://blogs.vmware.com/cloud-foundation/2025/03/10/vmware-fusion-workstation-going-free-new-resources/) for private, educational and commercial use. It was developed **specifically for macOS** by [VMware](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion), now owned by [Broadcom](https://en.wikipedia.org/wiki/Broadcom). It is a mature and capable product, but involves more friction — starting with the fact that the download requires a Broadcom account, and there are some quirks to work around (see [below](#alternative-vmware-fusion)). Its real strength is Windows guests. Keep it in mind as a fallback if UTM gives you trouble.
- [Parallels Desktop](https://www.parallels.com/products/desktop/) is a popular commercial alternative, but requires a paid license. You don't need it, unless you have a specific application for which the free options are not suitable.

Install UTM according to [docs.getutm.app](https://docs.getutm.app/installation/macos/). (Additional links: [GitHub](https://github.com/utmapp/UTM/).) Note that UTM is also sold on the Mac App Store; that version is identical, and paying for it is simply a way of supporting the developers.

Note that my tutorial for [installing Linux in VirtualBox](https://biodatasciencetulln.github.io/Wiki/install_linux_in_virtualbox.html) includes important Ubuntu-specific information applicable to users of other virtualization platforms like UTM or VMware.

## Host, hypervisor, guest: who does what?

Remember this mental model, which will save you some confusion later:

- The **host** is your Mac, running macOS.
- The **hypervisor** is the virtualization application (UTM, or VMware Fusion). It is a normal macOS app that creates and runs the virtual machine.
- The **guest** is Ubuntu, running inside the VM.

All three handle input, display and files, and each has its own settings. When something behaves strangely, the first question to ask is always **which of the three is responsible**.

Keyboard behavior is the classic example. A key press travels host → hypervisor → guest, and any layer can intercept it. If a keyboard shortcut doesn't reach Ubuntu, macOS may be capturing it, or the hypervisor may have its own mapping for it. And the **keyboard layout inside Ubuntu** (German vs. US, for instance) is something else entirely, managed by the guest OS, with neither macOS nor the hypervisor involved. Three different places to look, three different fixes.

The same logic applies to shared folders (the host offers a directory, the hypervisor exposes it, the guest must mount it), to the clipboard, and to screen resolution.

## Installation of Ubuntu in UTM

- Official [documentation](https://docs.getutm.app/basics/basics/), especially the [Ubuntu guide](https://docs.getutm.app/guides/ubuntu/)
- Recommended YouTube walkthrough: "How to Install Ubuntu 26.04 LTS on Mac (M Series) \| Run Ubuntu on Apple Silicon Using UTM" by ProgrammingKnowledge, 05/2026 ([YouTube](https://www.youtube.com/watch?v=QZH1pZrqn7c))
  - Also see "How to Install Ubuntu on Mac (M1, M2, M3, M4) // Run Ubuntu on Apple Silicon Using UTM (NEW)" by Ksk Royal, 08/2025 ([YouTube](https://www.youtube.com/watch?v=_JDg69TrOao))

Canonical now provides a **native Ubuntu Desktop ISO for ARM** ([ubuntu.com](https://ubuntu.com/download/desktop)), so you can simply install Ubuntu Desktop directly. Download the ISO file of the latest LTS release, currently **Ubuntu 26.04 LTS** ("Resolute Raccoon"), for the **ARM 64-bit architecture** (arm64).

- Generally, you don't have to use the Ubuntu LTS (Long-Term Support) version, but the [extended support](https://ubuntu.com/about/release-cycle) is convenient, and many tutorials are oriented towards LTS versions.
- **Historical note:** older tutorials, YouTube videos and blog posts describe a workaround that was necessary for Ubuntu releases before 24.10, when no ARM desktop ISO existed: install **Ubuntu Server** for ARM and then convert it to a desktop system by installing a desktop environment with `sudo apt install ubuntu-desktop`. You **no longer need to do this**. If you follow one of the older guides, skip that conversion step — everything else still applies.

Installation notes:

- You can leave the **virtual drive size** at 64 GB (default setting), or increase it to ~80 GB (recommended).
- The "**shared directory**" is a macOS directory that the VM will be able to access; you can also add it later.
- Remember that on Apple Silicon, you need software intended for ARM architecture; x86 installers won't work, unless you use UTM "Emulation" instead of "Virtualization", which is much slower.
- Create a new virtual machine (VM) and run the **Ubuntu installer** as shown in the YouTube video.
- Remember that the installation happens only within the VM, so you can always repeat it if something doesn't work. The default settings are usually fine ([ubuntu.com](https://ubuntu.com/desktop/docs/en/latest/tutorial/install-ubuntu-desktop/)).
- The next step is to **install system updates** via `sudo apt update && sudo apt upgrade`; this is explained in detail in the [VirtualBox tutorial](install_linux_in_virtualbox.md).
- Install the `qemu-guest-agent` and `spice-vdagent` packages as explained in the [UTM docs](https://docs.getutm.app/guest-support/linux/) to improve the guest support; this is the equivalent of VirtualBox **guest additions**.
  - The QEMU guest agent is a program intended to run in the background in VMs that use the QEMU hypervisor ([qemu-project.gitlab.io](https://qemu-project.gitlab.io/qemu/interop/qemu-ga.html)).
  - The SPICE agent is another helper program (technical details: [spice-space.org](https://www.spice-space.org/index.html), [manpages.ubuntu.com](https://manpages.ubuntu.com/manpages/lunar/man1/spice-vdagent.1.html)).
- The Ubuntu Desktop ISO ships the GNOME desktop. Other desktop environments like Xfce exist ([howtogeek.com](https://www.howtogeek.com/193129/how-to-install-and-use-another-desktop-environment-on-linux/)) and can be added later via `sudo apt install xubuntu-desktop`. This is a matter of taste; GNOME is fine for our purposes.
- Set up a shared folder according to the instructions in [docs.getutm.app](https://docs.getutm.app/guest-support/linux/#virtfs).
- Note that during startup of your VM you may briefly see some log messages ([askubuntu.com](https://askubuntu.com/questions/982632/what-are-the-messages-i-see-during-the-startup-shutdown-process-of-ubuntu)) and possibly even some error messages; this is part of the normal boot process.
- If you get a warning about low disk space, inspect the disk usage in the [disk usage analyzer](https://help.gnome.org/users/baobab/stable/); did you select an appropriate disk size when configuring the VM in UTM?
- After setting up the VM, you can [make a backup](https://github.com/utmapp/UTM/discussions/5234) of the VM. It's good practice to perform backups in regular intervals, so that you can quickly revert to the last working version if required.

A note on the desktop: the GNOME philosophy differs from more traditional desktops like XFCE. It focuses on minimalism and touchscreen-friendliness, whereas XFCE and other traditional desktops prefer a conventional, menu-driven interface akin to older Windows versions, offering extensive customization and a lighter resource footprint. Especially on GNOME, [keyboard shortcuts](https://help.gnome.org/gnome-help/shell-keyboard-shortcuts.html) can significantly boost your productivity. For instance, [Super](https://help.gnome.org/gnome-help/keyboard-key-super.html) (Command key) opens the activities overview, and Super + Tab allows to quickly switch between open windows.

Ubuntu has additional useful settings. For example, you can visit [extensions.gnome.org](https://extensions.gnome.org/) to learn more about GNOME extensions, and install e.g. a system monitor like [this one](https://extensions.gnome.org/extension/6807/system-monitor/).

Hint: If the given explanations are too brief or technical, or a command doesn't work as expected, you can discuss them with an LLM like Gemini, Claude or ChatGPT. However, these tools sometimes give wrong or imprecise information. The authoritative source is still the technical documentation.

### Problems?

- Try searching for the respective issue
  - on GitHub ([UTM issues](https://github.com/utmapp/UTM/issues), [UTM discussions](https://github.com/utmapp/UTM/discussions/))
  - on Reddit (via Google: simply add `reddit` to your search query, or `site:reddit.com`, see [techlicious.com](https://www.techlicious.com/tip/google-search-tips-everone-should-know/))
  - on Google
- Display resolution: in case of problems, try to set another resolution in the VM settings, e.g. 1440x900
- If the VM freezes regularly, try changing the "Emulated Display Card" in the VM Display settings, e.g. to virtio-ramfb ([forums.macrumors.com](https://forums.macrumors.com/threads/utm-virtualisation-of-ubuntu-20-04-randomly-freezes-on-apple-silicon-m2.2388950/))
- If the VM remains unusable after trying the above, switching to [VMware Fusion](#alternative-vmware-fusion) is a legitimate fallback.

### Additional links

- **Ubuntu Desktop documentation**: [documentation.ubuntu.com](https://documentation.ubuntu.com/desktop/), and the **Ubuntu Server** tutorial and How-to guides: [ubuntu.com](https://documentation.ubuntu.com/server/tutorial/)
- Blogs:
  - [sachin-the-learner.hashnode.dev](https://sachin-the-learner.hashnode.dev/install-ubuntu-using-utm-on-mac)
  - [medium.com](https://medium.com/@lizrice/linux-vms-on-an-m1-based-mac-with-vscode-and-utm-d73e7cb06133)

### Additional notes for hackers

- The Ubuntu installer sets up an "LVM partitioning scheme". More information:
  - [ubuntu.com](https://ubuntu.com/server/docs/install/storage)
  - [digitalocean.com](https://www.digitalocean.com/community/tutorials/an-introduction-to-lvm-concepts-terminology-and-operations) - introduction to LVM concepts
  - [discourse.ubuntu.com](https://discourse.ubuntu.com/t/how-is-the-size-of-the-lvm-container-decided/24608)
  - [askubuntu.com](https://askubuntu.com/questions/1269493/how-to-make-lv-use-all-disk-space-in-pv)
- In some cases, you will need to change the **VM settings in UTM**
  - For example, if you use a VPN on your host machine, you may need to change the network mode to "Emulated VLAN" to be able to connect to the internet from within the VM ([UTM docs](https://docs.getutm.app/settings-qemu/devices/network/network/), [GitHub](https://github.com/utmapp/UTM/issues/3238))
- Ubuntu is not the only Linux distro that can be run on UTM ([docs.getutm.app](https://docs.getutm.app/guides/guides/))
- UTM can also run Windows VMs, see e.g. [eshop.macsales.com](https://eshop.macsales.com/blog/72081-utm-virtual-machine-on-m1-mac/) (07/2021)

## Alternative: VMware Fusion

You only need this section if UTM doesn't work out for you. Everything above about Ubuntu itself — the ARM desktop ISO, updates, the desktop environment, Miniforge — applies here too.

### Installation

Install VMware Fusion (version 26H1 at the time of writing) according to [knowledge.broadcom.com](https://knowledge.broadcom.com/external/article/368667/download-and-license-information-for-vmw.html). The download requires creating a [Broadcom account](https://www.reddit.com/r/vmware/comments/1kolpgb/how_to_download_vmware_fusion_free/), and the process is not entirely self-explanatory. (Additional links: [Broadcom forum](https://community.broadcom.com/communities/communityhomeblogs?CommunityKey=0c3a2021-5113-4ad1-af9e-018f5da40bc0).)

### Installation of Ubuntu in VMware Fusion

- YouTube walkthroughs:
  - "How to Install VMware Fusion on Mac (Step-by-Step) (2026)" by ProgrammingKnowledge, 07/2026 ([YouTube](https://www.youtube.com/watch?v=0Hp-5ZYJI6A)) and "How to Install Ubuntu 26.04 LTS on VMware Fusion for Mac (2026)" by ProgrammingKnowledge, 07/2026 ([YouTube](https://www.youtube.com/watch?v=BKGYltyrk_8))
  - "Complete Beginner's Guide to Installing Ubuntu on Mac with VMware Fusion Pro" by Tech Troublemaker, 03/2025 ([YouTube](https://www.youtube.com/watch?v=zCozkZ269fk))
  - You can customize the resolution as explained in [this video](https://youtu.be/kDosGTdwqO0?t=610)
- The [community](https://community.broadcom.com/vmware-cloud-foundation/viewdocument/the-unofficial-fusion-for-apple-sil) has a "Fusion 13 for Apple Silicon **Companion Guide**" (v34 at the time of writing) – an unofficial user-contributed document that provides tips and techniques for setting up and running virtual machines with VMware Fusion 13 on Apple Silicon Macs. It was required to modify a fresh Ubuntu installation using the commands from the "Ubuntu" section in the guide – such as installing `ubuntu-desktop` or `ubuntu-desktop-minimal` on top of Ubuntu Server to install the GNOME Desktop. This step is **no longer necessary** if you use the ARM Ubuntu Desktop ISO, which already includes GNOME.
  - Apart from GNOME, you could also install `xubuntu-desktop`, which installs the XFCE desktop (and thus, effectively, Xubuntu). However, setting a high resolution didn't work for me in Xubuntu; after setting the "scaling" option to 200%, the screen remained black. Therefore, this is currently not recommended. You will often encounter different sorts of problems like this, especially in non-standard configurations – be mindful about this and don't let it discourage you.
- To improve the integration between host and guest (copy-paste functionality, resolution, etc.), install these packages ([knowledge.broadcom.com](https://knowledge.broadcom.com/external/article?legacyId=2073803), [GitHub](https://github.com/vmware/open-vm-tools)): `sudo apt update; sudo apt install open-vm-tools open-vm-tools-desktop`
- After setting up the VM, you can **make a backup** of the VM as explained in the [best practices](https://knowledge.broadcom.com/external/article/303386/#:~:text=There%20is%20no,back%20it%20up.) for virtual machine backup (programs and data) in VMware Fusion. For instructions how to locate the VM file for backup, see [here](https://knowledge.broadcom.com/external/article/344570/locating-the-virtual-machine-bundle-in-v.html).
  - It's good practice to backup the VM in regular time intervals, so that you can quickly revert to the last working version if needed.

### Problems and solutions

Below are examples of problems I encountered with VMware Fusion, and how they were solved. Most of them are instances of the [host / hypervisor / guest](#host-hypervisor-guest-who-does-what) question above: figure out which layer is responsible, and the fix usually follows.

- After the installation of the OS, one keyboard key didn't work.
  - Solution: Debugging together with Claude showed that deactivating the checkbox "Enable Mac OS Host Keyboard Shortcuts" ([techdocs.broadcom.com](https://techdocs.broadcom.com/us/en/vmware-cis/desktop-hypervisors/fusion-pro/13-0/using-vmware-fusion/configuring-vmware-fusion/setting-fusion-preferences/enable-or-disable-mac-os-shortcuts-on-the-keyboard-and-mouse-preference-pane.html)) fixed the problem. This option allows the host system to intercept key presses before they reach the guest OS. In case of other key mapping problems, see [this thread](https://community.broadcom.com/vmware-cloud-foundation/discussion/dead-keys-on-host-system-prevent-vmware-guest-from-receiving-keystrokes-at-all). If you want to use the same key bindings in the VM as on the host, you can add additional key mappings, e.g. <kbd>⌘</kbd> → <kbd>Ctrl</kbd>, and <kbd>⌘</kbd> + <kbd>Tab</kbd> → <kbd>Alt</kbd> + <kbd>Tab</kbd>, as explained [here](https://community.broadcom.com/vmware-cloud-foundation/discussion/dead-keys-on-host-system-prevent-vmware-guest-from-receiving-keystrokes-at-all#:~:text=Command%2DTab%20%C2%A0%2D%3E%20Alt,removes%20windows%20key). One possible (untested) alternative is a project like [toshy](https://github.com/RedBearAK/toshy).
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

## Installation of Miniforge (conda)

[Miniforge](https://github.com/conda-forge/miniforge) is a minimal installer for **conda**, the package and environment manager we use throughout the curriculum. It is preconfigured to use the [conda-forge](https://conda-forge.org/) channel, which — together with [bioconda](https://bioconda.github.io/) — is where essentially all bioinformatics software is published. We deliberately don't use the larger **Anaconda** distribution: its `defaults` channel is no longer recommended for bioinformatics (bioconda dropped it in 2024), and its terms of service require a paid license in companies with 200 or more employees.

Install it **inside the Linux VM**, using the `aarch64` (ARM) installer:

```bash
cd ~
wget https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-aarch64.sh
bash Miniforge3-Linux-aarch64.sh
```

This download link always points at the newest release, so there is no version number to keep up to date. Remember that on Apple silicon you need the `aarch64` build; an `x86_64` installer will not run.

Follow the prompts: accept the license, accept the default install location, and answer "yes" when asked whether to run `conda init`. Close and reopen your terminal; your prompt should then begin with `(base)`.

Then create a separate environment for your work, rather than installing into `base`:

```bash
conda create -n bds python jupyterlab numpy pandas matplotlib scikit-learn biopython
conda activate bds
```

- If you ever break the environment, you can simply delete and recreate it (`conda env remove -n bds`) without reinstalling conda.
- In case of problems, you can also install Miniforge directly on the host system; be sure to use the macOS `arm64` installer ([conda-forge.org/download](https://conda-forge.org/download/)).
- More information: [Miniforge on GitHub](https://github.com/conda-forge/miniforge), [conda-forge docs](https://conda-forge.org/docs/user/introduction/)
