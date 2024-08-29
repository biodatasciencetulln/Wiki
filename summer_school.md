<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>Information about summer school</H1>

- TOC
{:toc}

## Overview

In the Bio Data Science summer school, we will set up a working environment useful for multiple courses of the curriculum. We will install Ubuntu (a Linux distribution) in a virtual machine, which allows to easily use the Linux operating system and any Linux program. In the virtual machine, we will install several required programs, like Anaconda (a bundle of software packages for data science, including Python), Jupyter (it lets you create and run documents, so-called "notebooks", with Python code/outputs/additional text, via the browser) and Visual Studio Code (another popular development environment for Python and other programming languages). We will also start learning the basics of the Linux shell, which is a necessary prerequisite for all kinds of biological data analysis.

The sessions will be held online, via Microsoft Teams (alternatively Zoom). Please have the following available:

- Fachhochschule login (username and password)
- Adequate laptop (Windows, macOS or Linux)
- Internet connection
- Headset
- Microsoft Teams and Zoom
- Required software (listed below)

The first part (setting up the virtual machine) is very detailed and quite technical. This is challenging at the beginning, but it's a one-time setup, and you'll get used to working with it very soon.

## Preparation for the summer school

### Required software

- Install [VirtualBox](https://www.virtualbox.org/) (for Intel CPUs; for Apple M1 chips or later, see [below](#apple-silicon))
- Download the ISO file of the latest [Xubuntu](https://xubuntu.org/) LTS release (currently 24.04); the ISO can be downloaded via a torrent file or directly from a nearby mirror, e.g. [this one](http://ftp.uni-kl.de/pub/linux/ubuntu-dvd/xubuntu/releases/24.04/release/) → 64-bit PC ([AMD64](https://en.wikipedia.org/wiki/X86-64)) desktop image (filename `xubuntu-24.04-desktop-amd64.iso`)
  - If you want (this is purely optional), you can verify the integrity of the downloaded file as explained on [ubuntu.com](https://ubuntu.com/tutorials/how-to-verify-ubuntu) or [pctipp.ch](https://www.pctipp.ch/praxis/windows-10/windows-10-sha256-hash-bordmitteln-pruefen-2507915.html)
- Download the Anaconda installer for Linux-x86 from [anaconda.com](https://www.anaconda.com/download#download); the downloaded file should have a filename like `Anaconda3-202x.xx-Linux-x86_64.sh`
- Download the Visual Studio Code installer for Debian, Ubuntu ([code.visualstudio.com](https://code.visualstudio.com/Download))
- Create an account on [GitHub](https://github.com/)

#### Apple silicon

Apple silicon computers (Macbooks since 2020, with M1 chip or later) have a different underlying processor architecture, and there are some differences regarding the used software. Such [ARM-based CPUs](https://www.quora.com/How-is-the-Apple-MacBook-M1-capable-of-beating-every-x86-chip-I-taught-ARM-was-weaker-than-x86) are referred to as "AArch64" or "ARM64". The transition of established workflows to ARM-based processors is still ongoing, and you might encounter occasional problems, but there should be no major difficulties anymore.

- **VirtualBox is not available** for Apple silicon; alternatives are:
  - [VMware Fusion Pro](https://knowledge.broadcom.com/external/article/368667/download-and-license-information-for-vmw.html) (in case of problems see [reddit](https://www.reddit.com/r/vmware/comments/1cry8ej/comment/l426xtq/)): free for personal use; see [companion guide](https://community.broadcom.com/vmware-cloud-foundation/discussion/version-28-of-the-fusion-companion-guide-is-now-available) (v28 at the time of writing; you need only the "Ubuntu" section from the guide), [YouTube tutorial](https://www.youtube.com/watch?v=4dFy-4pw8NA), [forum](https://community.broadcom.com/communities/communityhomeblogs?CommunityKey=0c3a2021-5113-4ad1-af9e-018f5da40bc0)
  - [UTM](https://mac.getutm.app/): open source ([GitHub](https://github.com/utmapp/UTM/)); see the official [documentation](https://docs.getutm.app/basics/basics/) and especially the [Ubuntu guide](https://docs.getutm.app/guides/ubuntu/) and my [short installation guide](install_linux_in_UTM.md)
  - UTM and VMware Fusion Pro both work well; you can also try out both, and stick to the one that works best for you
  - a commercial alternative is [Parallels Desktop](https://www.parallels.com/products/desktop/), which is popular, but requires a paid license
  - note that my tutorial for [installing Linux in VirtualBox](https://biodatasciencetulln.github.io/Wiki/install_linux_in_virtualbox.html) is mostly oriented towards VirtualBox, even though it also contains universally useful information
- Canonical does not provide an official Ubuntu Desktop release for platforms other than x86_64 and Raspberry Pi. The best approach to set up Ubuntu Desktop on ARM is to install Ubuntu Server for ARM and convert it to an Ubuntu Desktop by installing additional software (the desktop environment). This is the preferred way for both UTM and VMware Fusion. You will need the ISO file of the latest [Ubuntu Server](https://ubuntu.com/download/server/arm) LTS release (currently 24.04).
- For installing Anaconda ([docs.anaconda.com](https://docs.anaconda.com/anaconda/install/)) in the Linux VM, download the `Linux-aarch64` installer (it has a filename like `Anaconda3-202x.xx-Linux-aarch64.sh` on [anaconda.com](https://www.anaconda.com/download#download))
  - In case of problems, you can always install Anaconda directly on macOS, just make sure to use the right installer ("Apple silicon")

### Additional background information

Watch these videos as preparation:

- "What is a Virtual Machine (VM)? In 3 minutes - Virtual Machine Tutorial for Beginners" ([YouTube](https://www.youtube.com/watch?v=yIVXjl4SwVo))
- "Virtual Machines explained in 15 Mins" by TechWorld with Nana, 2021 ([YouTube](https://www.youtube.com/watch?v=mQP0wqNT_DI))
- "Bash in 100 Seconds" by Fireship, 2021 ([YouTube](https://www.youtube.com/watch?v=I4EWvMFj37g)), which is a *very* short intro to Bash scripting (Bash is the name of the most popular Linux shell); you will recognize these concepts later in your lectures
  - Note the command `which $SHELL` (and the output, `/usr/bin/bash` in the video); by the way, did you notice that the `$` sign is also used later, when he talks about variables (`echo $GREET`)? Hmm, let's see if there is a pattern...
  - Note that he says "It's like any other application that lives in the binaries directory". Apparently there is a "binaries" directory (maybe it's the `bin` in `/usr/bin/bash`?) where applications, i.e. programs, live
  - Note that he mentions the file `.bashrc` for customization
  - Note that commands like `echo` (which simply prints something, e.g. `echo Hi there!` prints `Hi there!`) can be used interactively in the shell or non-interactively in a **shell script**; shell scripts simply execute commands line by line
  - Note that he mentions **variables**, which are placeholders for data/information that you want to use later in your script/program
  - Note that he mentions **arguments**, which is data/information that you want to pass to a script/program from the command line (e.g. if the script does some data analysis on files in a directory, and you want to tell it which directory it should work on); this is not the same as **interactive input**, which is rarely required
  - Note that you can create loops (repeating instructions) and conditional logic in Bash (and also in other programming languages)
  - Note that in the end he mentions **processes** (as opposed to scripts/programs); programs are code written by developers, while processes represent the actual execution of programs in memory (if you execute a program multiple times in parallel, you have multiple processes)

## Summer school goals

By the end of our summer school sessions, you should have:

- A virtual machine with Xubuntu or Ubuntu, i.e. a fully functional Linux operating system
  - This allows to easily install/modify/test anything without worrying that you break your computer
  - If the VM breaks (e.g. it becomes unresponsive or doesn't boot anymore), you can restore it to its previous state within minutes from a backup (see [here](https://biodatasciencetulln.github.io/Wiki/install_linux_in_virtualbox.html) for information on backups)
- An installation of Anaconda, which is a collection of software including Python, the program `conda` and many other software packages like Jupyter and others
- An installation of the code editor Visual Studio Code
- The knowledge how to run Jupyter and open "notebooks" (`.ipynb` files) in JupyterLab in the browser
  - Notebook documents (or "notebooks") are text files, which contain both computer code (e.g. Python) and text. They are both human-readable documents containing text and results (figures, tables, etc.) as well as executable documents which can be run to perform data analysis. Jupyter allows editing and running notebooks via a web browser. It can be executed on a local desktop requiring no internet access, or on a remote server and accessed through the internet. Jupyter also allows to edit text files and provides a built-in terminal.
  - You can also try JupyterLab online (on a remote server somewhere on the internet), including a very short tour of JupyterLab: https://jupyter.org/try -> click "JupyterLab"
- Basic knowledge of the Linux shell
