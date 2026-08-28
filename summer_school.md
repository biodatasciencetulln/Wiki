<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>Information about summer school</H1>

* TOC
{:toc}

## Overview

Welcome to the **Bio Data Science summer school**! This session is all about setting up your personal bioinformatics toolkit – a powerful digital workspace that you'll use throughout your master's curriculum.

We'll begin by setting up a **Linux environment** on your laptop. Linux is the operating system (OS) that essentially all bioinformatics software is written for, and the one running on the FH compute servers you'll use later. How you get there depends on your computer:

- On **Windows**, we use the [Windows Subsystem for Linux](install_linux_in_wsl.md) (WSL), which lets you run a real Linux environment, such as Ubuntu, directly on Windows using a lightweight built-in virtual machine. The default Linux distribution is Ubuntu, others are also [available](https://learn.microsoft.com/en-us/windows/wsl/basic-commands). It installs with a single command and integrates tightly with your Windows desktop and editor.
- On a **Mac with Apple silicon**, we use a virtual machine — a computer within your computer — via [UTM or VMware Fusion](install_linux_on_apple_silicon.md).
- If you prefer a full Linux desktop in a window, or WSL is unavailable on your machine, [VirtualBox](install_linux_in_virtualbox.md) remains a good alternative.

Once Ubuntu is running, we'll equip it with essential software:

- **Miniforge**: A minimal installer for `conda`, the package and environment manager we use to install Python and scientific software. Nearly all bioinformatics tools are distributed this way, via the conda-forge and bioconda channels.
- **Jupyter**: This tool lets you create interactive "notebooks" directly in your web browser. These notebooks combine Python code, its output, and explanatory text, making them perfect for many applications.
- **Visual Studio Code**: A popular and highly customizable development environment where you can write, run, and debug code in Python and many other languages.

Then we'll dive into the Linux shell. This is simply a program that acts as an interface to the OS. It takes commands from the keyboard (**command-line interface**) and gives them to the OS to perform. Knowing the shell is fundamental for efficient biological data analyses.

The shell is where we'll spend most of our time, and there will be plenty of hands-on exercises. It's the tool you'll use for most courses of the curriculum, so it's worth getting comfortable with it now.

The sessions will be held online, via Microsoft Teams (alternatively Zoom). Please have the following available:

- Fachhochschule login (username and password)
- Suitable laptop (Windows, macOS or Linux)
- Stable internet connection
- Headset
- Microsoft Teams and Zoom
- Required software (listed below)

The setup step may seem daunting at first, but there are detailed tutorials to guide you (linked above), and it's a one-time investment that you'll benefit from for the rest of the curriculum.

### Plan for each session

1. **"Vorbereitungen für den Studienbeginn – Installation notwendiger Programme"**: Setting up your Linux environment (WSL on Windows, a VM on Apple silicon), installing Miniforge and VS Code. First steps in the terminal.
2. **"Freiwillige Übungseinheit – Installation notwendiger Programme"**: Questions and problems regarding the setup, Miniforge, and VS Code. Bring whatever didn't work.
3. **"Linux I"**: Linux basics, important computer terms, essential shell commands, navigating the file system.
4. **"Linux II"**: Package manager, Linux file hierarchy, variables, environment. Practical exercises.

## Preparation for the summer school

Please do as much of this as you can before the first session, so that we can spend our time together on the parts that actually need discussion.

### Everyone

- Create an account on [GitHub](https://github.com/). Use a professional-looking username; you may well end up linking to it in a CV. We won't be using Git in the summer school — you'll learn version control properly in the "Best Practices" course in the second semester — but the account is useful for browsing and downloading course materials in the meantime.
- Make a **full backup of your computer** before making any modifications.
- Nothing to download in advance for Miniforge — we install it from the command line inside Linux during the session.

### Windows

- Check that you're on Windows 10 version 2004 (build 19041) or later, or Windows 11: press <kbd>Win</kbd> + <kbd>R</kbd>, type `winver`, press Enter.
- Check that virtualization is enabled: Task Manager (<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Esc</kbd>) → Performance → CPU → look for "Virtualization: Enabled".
- Install [Visual Studio Code](https://code.visualstudio.com/Download) for Windows.
- Note that you do **not** need to download an Ubuntu ISO for WSL — it downloads Ubuntu itself during the installation. Full instructions: [Install Ubuntu in WSL](install_linux_in_wsl.md).

**Backup plan.** WSL works on the large majority of machines, but occasionally it can't be enabled — an older Windows build, a locked-down laptop, or virtualization switched off in the firmware. So that nobody loses a session to this, please also prepare the VirtualBox route in advance:

- Install [VirtualBox](https://www.virtualbox.org/).
- Download the ISO file of the latest [Xubuntu](https://xubuntu.org/download/) LTS release, currently 26.04 — the 64-bit PC ([AMD64](https://en.wikipedia.org/wiki/X86-64)) desktop image. You can download via torrent or from a nearby mirror.
  - Optionally, verify the integrity of the downloaded file as explained on [ubuntu.com](https://ubuntu.com/tutorials/how-to-verify-ubuntu).

For now, we will use VirtualBox as a fallback option; for installation instructions, see the [VirtualBox tutorial](install_linux_in_virtualbox.md). You don't have to use it later if WSL works well for you. Generally, installing VirtualBox does not interfere with WSL. However, once WSL is installed, VirtualBox runs on top of the Windows hypervisor and is therefore somewhat slower than it would be on its own.

### macOS (Apple silicon)

Apple silicon computers (MacBooks from 2020 onwards, with M1 chips or later) use a different processor architecture than previous Intel-based Macs. This [ARM-based](https://en.wikipedia.org/wiki/Apple_silicon) CPU architecture is also known as AArch64 or ARM64, and represents a significant [shift](https://www.quora.com/How-is-the-Apple-MacBook-M1-capable-of-beating-every-x86-chip-I-taught-ARM-was-weaker-than-x86). Software installers for this architecture usually have `arm64` or `aarch64` in their filenames.

- Install UTM and/or VMware Fusion according to the instructions in the [tutorial](install_linux_on_apple_silicon.md).
- Download the **Ubuntu Desktop ISO for ARM** — the latest LTS release, currently 26.04 LTS — from [ubuntu.com](https://ubuntu.com/download/desktop). Be sure to pick the **ARM 64-bit** (arm64) image, not the Intel/AMD one.
- Install [Visual Studio Code](https://code.visualstudio.com/Download) for macOS (Apple silicon build).

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

- **A working Linux environment**, via WSL or a virtual machine, giving you a fully functional Ubuntu system.
  - This allows you to easily install, modify, and test software without any risk or changes to your main OS.
  - If it breaks (becomes unresponsive, or you install something that ruins it), you can restore it from a backup, or simply wipe it and start over. WSL users: `wsl --export` and `wsl --import`; VM users: see the backup sections of the respective tutorials. Knowing you can always start over is what makes it safe to experiment — and experimenting is how you learn.
- **An installation of Miniforge**, giving you the `conda` package and environment manager, and a working environment containing Python and Jupyter.
  - You'll also understand *why* we use environments: if one breaks, you delete and recreate it instead of repairing your whole system.
- **An installation of Visual Studio Code**, connected to your Linux environment, so that you edit code in a comfortable graphical editor while it runs in Linux.
- **The ability to run Jupyter** and open "notebooks" (`.ipynb` files) in JupyterLab in the browser, or directly in VS Code.
  - Notebook documents (or "notebooks") are text files containing both computer code (e.g., Python) and text. They are human-readable documents containing text and results (figures, tables, etc.), but also executable code that can be run to perform data analysis. Jupyter enables editing and running notebooks via a web browser. It can be run locally without internet access, or on a remote server and accessed through the internet. Jupyter also includes a text file editor and a built-in terminal.
  - You can also try JupyterLab online (on a remote server somewhere in the internet), including a very short tour: [jupyter.org/try](https://jupyter.org/try) → click "JupyterLab".
- **Working knowledge of the Linux shell**: navigating the file system, inspecting and manipulating text files, installing software with the package manager, and understanding variables and the environment. This is the main goal, and the one that pays off soonest.

## What is a server, anyway?

Later, you will also get an account on a shared Linux server, and for some jobs it is the better tool.

A server is a computer you use over the network instead of sitting in front of it. The plain way in is `ssh`: you get a shell, and from there it behaves like the Linux machine on your desk — same commands, same files, no windows. Servers often also run browser-based interfaces such as JupyterLab or RStudio Server, which give you an editor and a notebook or console on the same machine. (If you are wondering why it's called RStudio Server: The word "server" refers not only to a physical computer, but also to software running in the background that "client" software connects to; in this case, the client is your browser.) Both of these interfaces include a terminal, so the shell is never far away; the browser interfaces are just a convenience layer. The server stays on whether you are logged in or not, so a job you start on Friday is still running on Monday.

The reason bioinformatics leans on servers is the data amount. A sequencing run produces files in the tens or hundreds of gigabytes; a genome assembly or a large alignment can want much more memory than a laptop has installed, and will fail otherwise. A server has the RAM, the cores, the disk, and a copy of the reference data everyone in the group would otherwise download separately. Several people use it at once, which is also why you share it politely.

### Why set up a local environment when there is a server?

It's still very convenient to have a development environment on your own machine, for several reasons.

**You are allowed to break it.** On a shared machine you are a guest: no root, no system packages, no reboots. On your own VM you can install anything, misconfigure it, and reinstall from scratch in half an hour. Breaking things and repairing them is a large part of how you find out how something actually works.

**Admin rights change your perspective.** Permissions, package management, mounting filesystems – these are abstract concepts until you are the person responsible for them.

**It keeps working when the network does not.** Trains, conference wifi, maintenance windows, a VPN certificate that expires the morning of a deadline — none of these stop you if the work is on your own machine.

**You keep it.** Your server account ends with the curriculum. The environment on your laptop does not, and neither does the knowledge of how you built it – next time it'll be easy for you to set it up, if you need it.

**The loop is shorter.** Writing a script and running it against a small test file is quicker when the file, the editor and the interpreter are on the same machine.

On the other hand, the server is the right place for data that does not fit on a laptop, for jobs that run for hours, for anything needing a lot of memory or many cores, and for shared reference datasets you should not be copying around. The realistic workflow is both: develop and debug locally against a small subset, then run the full analysis remotely.
