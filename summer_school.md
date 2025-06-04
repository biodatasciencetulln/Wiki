<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>Information about summer school</H1>

- TOC
  {:toc}

## Overview

Welcome to the **Bio Data Science summer school**! This session is all about setting up your personal bioinformatics toolkit – a powerful digital workspace that you'll use throughout your master's curriculum.

We'll begin by installing **Ubuntu** or its derivative **Xubuntu**, both user-friendly versions of Linux, inside a virtual machine. Think of a virtual machine like a computer within your computer; it lets you run Linux and all its programs without altering your main operating system (OS).

Once Ubuntu is set up, we'll equip it with essential software:

- **Anaconda**: A collection of popular tools and packages for data science, including the versatile Python programming language.
- **Jupyter**: This tool lets you create interactive "notebooks" directly in your web browser. These notebooks combine Python code, its output, and explanatory text, making them perfect for many applications.
- **Visual Studio Code**: A popular and highly customizable development environment where you can write, run, and debug code in Python and many other languages.

Finally, we'll dive into the Linux shell. While it might sound technical, it's simply a program that acts as an interface to the OS. It takes commands from the keyboard (**command-line interface**) and gives them to the OS to perform. Knowing the shell is fundamental for efficient biological data analyses. Mastering these basics will give you a significant advantage in your bioinformatics journey!

The sessions will be held online, via Microsoft Teams (alternatively Zoom). Please have the following available:

- Fachhochschule login (username and password)
- Suitable laptop (Windows, macOS or Linux)
- Stable internet connection
- Headset
- Microsoft Teams and Zoom
- Required software (listed below)

The initial step, setting up the virtual machine, can be somewhat technical (refer to the [detailed tutorial](https://biodatasciencetulln.github.io/Wiki/install_linux_in_virtualbox.html)). This is challenging at first, but it's a one-time setup, and you'll quickly get used to it.

### Plan for each session

1. "Vorbereitungen für den Studienbeginn - Installation notwendiger Programme": Setting up a virtual machine with Xubuntu (or Ubuntu), installation of Anaconda
2. "Freiwillige Übungseinheit - Installation notwendiger Programme": Questions/problems regarding virtual machine and Anaconda
3. "Linux": Linux basics, important computer terms, essential shell comands
4. "Linux": Package manager, Linux file hierarchy, variables, environment

## Preparation for the summer school

### Required software

- Install [VirtualBox](https://www.virtualbox.org/) (for Intel CPUs; for Apple M1 chips or later, see [below](#apple-silicon)).
- Download the ISO file of the latest [Xubuntu](https://xubuntu.org/) LTS release, currently 24.04 (pick the latest minor version, e.g. 24.04.02). You can download the ISO via a torrent file or directly from a nearby mirror, such as [this one](http://ftp.uni-kl.de/pub/linux/ubuntu-dvd/xubuntu/releases/24.04/release/) → 64-bit PC ([AMD64](https://en.wikipedia.org/wiki/X86-64)) desktop image (filename `xubuntu-24.04-desktop-amd64.iso`).
  - Optionally, you can verify the integrity of the downloaded file as explained on [ubuntu.com](https://ubuntu.com/tutorials/how-to-verify-ubuntu) or [pctipp.ch](https://www.pctipp.ch/praxis/windows-10/windows-10-sha256-hash-bordmitteln-pruefen-2507915.html).
- Download the Anaconda installer for Linux-x86 from [anaconda.com](https://www.anaconda.com/download#download); the downloaded file should have a filename like `Anaconda3-202x.xx-Linux-x86_64.sh`
- Download the Visual Studio Code installer for Debian, Ubuntu ([code.visualstudio.com](https://code.visualstudio.com/Download)).
- Create an account on [GitHub](https://github.com/).

#### Apple silicon

Apple silicon computers (Macbooks since 2020, with M1 chip or later) have a different underlying processor architecture, leading to some software differences. These [ARM-based CPUs](https://www.quora.com/How-is-the-Apple-MacBook-M1-capable-of-beating-every-x86-chip-I-taught-ARM-was-weaker-than-x86) are also known as "AArch64" or "ARM64". The transition of established workflows to ARM-based processors is still ongoing, and you might encounter occasional problems, but no significant difficulties.

VirtualBox supports Apple silicon since [version 7.1](https://blogs.oracle.com/virtualization/post/oracle-virtualbox-710). This is a relatively recent development, and it's currently recommended to stick to alternatives described in my [short installation guide for Apple silicon](install_linux_on_apple_silicon). As preparation:

- Install [UTM](https://docs.getutm.app/installation/macos/) and [VMware Fusion Pro](https://knowledge.broadcom.com/external/article/368667/download-and-license-information-for-vmw.html) (in case of installation problems, see [reddit](https://www.reddit.com/r/vmware/comments/1cry8ej/comment/l426xtq/)).
    - You can install VMware Fusion Pro by creating a Broadcom account and downloading "VMware Fusion Pro for Personal Use". Alternatively, you can install the [Homebrew](https://brew.sh/) package manager (also see [mac.install.guide](https://mac.install.guide/homebrew/3)), and use it to install and update other programs. For example, the command `brew install --cask utm` installs UTM ([formulae.brew.sh](https://formulae.brew.sh/cask/utm)), and the command `brew install --cask vmware-fusion` installs VMware Fusion ([formulae.brew.sh](https://formulae.brew.sh/cask/vmware-fusion)). If you have never worked with a package manager before, it's easier to perform the installations manually, without using Homebrew.
- Download the ISO file of the latest [Ubuntu Server](https://ubuntu.com/download/server/arm) LTS release (currently 24.04).
- Download the Anaconda installer for Linux-aarch64 from [anaconda.com](https://www.anaconda.com/download#download). The downloaded file should have a filename like `Anaconda3-202x.xx-Linux-aarch64.sh`

### Additional background information

Watch these videos as preparation:

- "What is a Virtual Machine (VM)? In 3 minutes - Virtual Machine Tutorial for Beginners" ([YouTube](https://www.youtube.com/watch?v=yIVXjl4SwVo))
- "Virtual Machines explained in 15 Mins" by TechWorld with Nana, 2021 ([YouTube](https://www.youtube.com/watch?v=mQP0wqNT_DI))
- "Bash in 100 Seconds" by Fireship, 2021 ([YouTube](https://www.youtube.com/watch?v=I4EWvMFj37g)), which is a _very_ short introduction to Bash scripting (Bash is the name of the most popular Linux shell). You'll recognize these concepts later in your lectures.
  - Note the command `which $SHELL` (and the output, `/usr/bin/bash` in the video). Did you notice that the `$` sign is also used later, when he talks about variables (`echo $GREET`)? There's a pattern here...
  - He says: "It's like any other application that lives in the binaries directory". Apparently there is a "binaries" directory (maybe it's the `bin` in `/usr/bin/bash`?) where applications, i.e. programs, live.
  - He mentions the file `.bashrc` for customization.
  - Commands like `echo` (which simply prints something, e.g. `echo Hi there!` prints `Hi there!`) can be used interactively in the shell or non-interactively in a **shell script**. Shell scripts simply execute commands line by line.
  - He mentions **variables**, which are placeholders for data/information that you want to use later in your script/program.
  - He mentions **arguments**, which is data/information that you want to pass to a script/program from the command line (e.g. specifying a directory for data analysis). This is not the same as **interactive input**, which is rarely required.
  - You can create loops (repeating instructions) and conditional logic in Bash (and other programming languages).
  - In the end he mentions **processes** (as opposed to scripts/programs). Programs are code written by developers, while processes represent the actual execution of programs in memory. If you execute a program multiple times in parallel, you get multiple processes.

## Summer school goals

By the end of our summer school sessions, you should have:

- A virtual machine with Xubuntu or Ubuntu, providing a fully functional Linux OS.
  - This allows you to easily install, modify, and test software without any risk or changes to your main OS.
  - If the VM malfunctions (e.g., becomes unresponsive or fails to boot), you can quickly restore it to a previous state from a backup (see [here](https://biodatasciencetulln.github.io/Wiki/install_linux_in_virtualbox.html) for information on backups).
- An installation of Anaconda, which is a software collection including Python, the `conda` program, and many software packages like Jupyter.
- An installation of the Visual Studio Code editor.
- The ability to run Jupyter and open "notebooks" (`.ipynb` files) in JupyterLab in the browser.
  - Notebook documents (or "notebooks") are text files containing both computer code (e.g., Python) and text. They are human-readable documents containing text and results (figures, tables, etc.), but also executable code that can be run to perform data analysis. Jupyter enables editing and running notebooks via a web browser. It can be run locally without internet access, or on a remote server and accessed through the internet. Jupyter also includes a text file editor and a built-in terminal.
  - You can also try JupyterLab online (on a remote server somewhere in the internet), including a very short tour: [jupyter.org/try](https://jupyter.org/try) → click "JupyterLab".
- Basic knowledge of the Linux shell.
