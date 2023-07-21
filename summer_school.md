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

## Preparation for the summer school

### Required software

- Install [VirtualBox](https://www.virtualbox.org/) (for Intel CPUs; for Apple M1 chips or later, see [below](#apple-silicon))
- Download the ISO file of the latest [Xubuntu](https://xubuntu.org/) LTS release (currently 22.04); the ISO can be downloaded via a torrent file or directly from a nearby mirror, e.g. [this one](http://ftp.uni-kl.de/pub/linux/ubuntu-dvd/xubuntu/releases/22.04/release/) → 64-bit PC ([AMD64](https://en.wikipedia.org/wiki/X86-64)) desktop image (filename `xubuntu-22.04-desktop-amd64.iso`)
  - If you want (this is purely optional), you can verify the integrity of the downloaded file as explained on [ubuntu.com](https://ubuntu.com/tutorials/how-to-verify-ubuntu) or [pctipp.ch](https://www.pctipp.ch/praxis/windows-10/windows-10-sha256-hash-bordmitteln-pruefen-2507915.html)
- Download the Anaconda installer for Linux-x86 from [anaconda.com](https://www.anaconda.com/download#downloads); the downloaded file should have a filename like `Anaconda3-202x.xx-Linux-x86_64.sh`
- Download the Visual Studio Code installer for Debian, Ubuntu ([code.visualstudio.com](https://code.visualstudio.com/Download))
- Create an account on [GitHub](https://github.com/)

#### Apple silicon

Apple silicon computers (Macbooks since 2020, with M1 chip or later) have a different underlying processor architecture, and there are some differences regarding the used software. Such [ARM-based CPUs](https://www.quora.com/How-is-the-Apple-MacBook-M1-capable-of-beating-every-x86-chip-I-taught-ARM-was-weaker-than-x86) are referred to as "AArch64" or "ARM64". The transition of established workflows to ARM-based processors is still ongoing, and you might encounter some problems, however there should be no major difficulties anymore.

- VirtualBox is not available for Apple silicon; instead, install [VMware Fusion Player](https://www.vmware.com/go/getfusionplayer) or [UTM](https://mac.getutm.app/) (a commercial alternative is also available, [Parallels Desktop](https://www.parallels.com/eu/); also see [here](https://biodatasciencetulln.github.io/Wiki/install_linux_in_virtualbox.html))
- Download the ISO file of the latest [Ubuntu Server](https://ubuntu.com/download/server/arm) LTS release (currently 22.04) (also see the section on Ubuntu installation in the latest VMware Fusion [companion guide](https://communities.vmware.com/t5/VMware-Fusion-Discussions/Announcing-The-Unofficial-Fusion-13-for-Apple-Silicon-Companion/td-p/2939909/page/2), v19 at the time of writing)
- For installing Anaconda ([docs.anaconda.com](https://docs.anaconda.com/anaconda/install/)) in the Linux VM, download `Linux-aarch64` installer (it has a filename like `Anaconda3-202x.xx-Linux-aarch64.sh` on [anaconda.com](https://www.anaconda.com/download#downloads))
  - In case of problems, you can always install Anaconda directly on macOS ([anaconda.com](https://www.anaconda.com/blog/new-release-anaconda-distribution-now-supporting-m1))

### Additional background information

Watch these videos as preparation:

- "What is a Virtual Machine (VM)? In 3 minutes - Virtual Machine Tutorial for Beginners" ([YouTube](https://www.youtube.com/watch?v=yIVXjl4SwVo))
- "Virtual Machines explained in 15 Mins" by TechWorld with Nana, 2021 ([YouTube](https://www.youtube.com/watch?v=mQP0wqNT_DI))
- "Bash in 100 Seconds" by Fireship, 2021 ([YouTube](https://www.youtube.com/watch?v=I4EWvMFj37g)), which is a *very* short intro to Bash scripting (Bash is the name of the most popular Linux shell); you will recognize these concepts later in your lectures
  - Note the command `which $SHELL` (and the output, `/usr/bin/bash` in the video); by the way, did you notice that the `$` sign is also used later, when he talks about variables (`echo $GREET`)? Hmm, let's see if there is a pattern...
  - Note that he mentions the file `.bashrc` for customization
  - Note that the command `echo` (it simply prints something, e.g. `echo Hi there!` prints `Hi there!`) has the same effect no matter whether it's used interactively in the shell, or in a shell script; shell scripts simply execute commands line by line
  - Note that he mentions **variables**, which are just placeholders for data/information that you want to use later in your script/program
  - Note that he mentions **arguments**, which is data/information that you want to pass to the script/program; for example, if the script does some data analysis on files in a directory, you want to be able to quickly tell it which directory it should work on; this is not the same as **interactive input**, which is rarely required
  - Note that in the end he is talking about **processes** rather than scripts

## Summer school goals

By the end of our summer school sessions, you should have:

- A functional Linux operating system, where you can easily install/modify/test anything without worrying that you may break something on your computer
  - If the VM breaks (e.g. it becomes unresponsive or doesn't boot anymore, which is rare), you should be able to restore it to its previous state within minutes (see [here](https://biodatasciencetulln.github.io/Wiki/install_linux_in_virtualbox.html) for more information on backup)
- An installation of Anaconda, which is a collection of software including Python, the program `conda` and many other packages like Jupyter and others
- An installation of Visual Studio Code
- The knowledge how to run Jupyter and open notebooks (`.ipynb` files) in JupyterLab in the browser
- Some experience of working with the Linux shell
