<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>Ubuntu basics</H1>

* TOC
{:toc}

This page applies to **every platform**. However you got your Linux environment — [WSL](install_linux_in_wsl.md), [a VM on Apple silicon](install_linux_on_apple_silicon.md), or [VirtualBox](install_linux_in_virtualbox.md) — the shell, the file system and package management work the same way. A few items apply only if you have a full Linux **desktop**; those are marked.

Each section ends with optional *further reading*. You don't need any of it to follow the instructions — come back to it when you're curious or stuck.

## Open a terminal

- **WSL** (Windows): open Windows Terminal, or run `wsl` in PowerShell. There is no desktop here — the terminal *is* your Linux environment.
- **Xubuntu in VirtualBox** (Xfce desktop): Application menu → Accessories → Terminal emulator.
- **Ubuntu in UTM or VMware Fusion** (GNOME desktop): press <kbd>Super</kbd> (the Command key on a Mac) to open the activities overview, then type `terminal`.

On both desktops, <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>T</kbd> also opens a terminal directly.

It's called a terminal "emulator" because it emulates the physical terminals that were once the only way to talk to a computer.

*Further reading: [Ubuntu command line for beginners](https://ubuntu.com/desktop/docs/en/latest/tutorial/the-linux-command-line-for-beginners/) · [GNOME keyboard shortcuts](https://help.gnome.org/gnome-help/shell-keyboard-shortcuts.html)*

## Run and stop commands

- **Start programs/run commands**: type the program/command in the terminal and hit <kbd>Enter</kbd>
- **Abort a program/command** running in the terminal: press **<kbd>Ctrl</kbd>+<kbd>C</kbd>** (this key combination sends the "SIGINT" (interrupt) signal to a running process)

To stop a program that isn't attached to your terminal, use `pkill <name>` (e.g. `pkill firefox`); this works everywhere, including WSL. Only use if absolutely necessary, as it loses unsaved work.

> **Desktop only**: on Xubuntu/Xfce you can enter `xkill` + <kbd>Enter</kbd> and then click a non-responsive *graphical* application to kill it.

Different desktop environments use different "display server protocols", i.e. different ways to draw windows on the screen. You can check in the terminal using the command `echo $XDG_SESSION_TYPE`, which prints `wayland` or `x11` (on WSL it prints nothing, because there is no desktop and thus no display server). Note that `xkill` is an X11 tool, so it does not work for applications running natively under Wayland, which recent GNOME versions use by default — there, use the System Monitor, or `pkill`.

A handful of shell shortcuts are worth learning straight away. These work in any terminal, on any platform:

| Shortcut | What it does |
| --- | --- |
| <kbd>Tab</kbd> | Complete the command or filename you started typing |
| <kbd>Ctrl</kbd>+<kbd>C</kbd> | Abort the running command |
| <kbd>Ctrl</kbd>+<kbd>D</kbd> | End input / close the shell |
| <kbd>Ctrl</kbd>+<kbd>L</kbd> | Clear the screen |
| <kbd>Ctrl</kbd>+<kbd>A</kbd> / <kbd>Ctrl</kbd>+<kbd>E</kbd> | Jump to start / end of the line |
| <kbd>Ctrl</kbd>+<kbd>U</kbd> | Delete everything left of the cursor |

## Command history

The Bash shell stores the history of commands you run.

- Use the arrow keys <kbd>&uarr;</kbd>/<kbd>&darr;</kbd> to repeat previously typed commands: e.g. enter `ls` + <kbd>Enter</kbd> → _list_ the contents of the current directory; now press <kbd>&uarr;</kbd> to bring up the previously entered command
- **Search** for previously entered commands using **<kbd>Ctrl</kbd>+<kbd>R</kbd>**: Press this shortcut and start typing to search your bash history for a command
- View the **complete history** using the command `history`

## The file system

The Linux **file system** has a single hierarchical directory structure. The top directory is `/`, called the **root directory** (or simply root). All files and folders are part of this hierarchy. Devices like disks, external memory devices and network resources (e.g. shared folders) are also part of the hierarchy.

The three commands you need first are `pwd` (where am I?), `cd` (go somewhere) and `ls` (what's here?).

*Further reading: [navigating the file system](https://linuxcommand.org/lc3_lts0020.php) · [how the Linux file system is organized](https://linuxcommand.org/lc3_lts0040.php) · [YouTube](https://www.youtube.com/watch?v=HbgzrKJvDRw)*

### File permissions

Every Linux file and directory has read/write/execute permissions for the **file owner**, the **group**, and **other users** — nine permissions in total. `ls -l` shows them. This matters as soon as you share a directory with collaborators, or wonder why you get "Permission denied".

*Further reading: [file permissions explained](https://linuxcommand.org/lc3_lts0090.php)*

## Read the output

When you interact with the terminal, you should always **read the output/error messages**, even if you don't immediately understand everything they say. You might be used from Windows that you just click "Cancel" or "Continue" to make the messages go away. Messages on Linux are usually more informative and tell you what's happening and if a problem occurred.

E.g., if you run a command, and a message says `Building modules...`, then it's building modules, and you have to wait. If it says `Successfully installed`, then the package was successfully installed. If it says `Failed to fetch http://some/web/url`, then the resource couldn't be fetched, maybe because the URL was invalid or there was no internet connection. If the command didn't complete successfully, try to search for the respective error message, which can help to find a solution.

## Update the system

After a fresh install, it's good practice to update the OS, to ensure that it's fully up to date. You can do this by using the built-in update/software management mechanism. (Unlike some other distributions, Ubuntu provides only well-tested software packages via this mechanism, which rarely lead to problems. Instead, updates can for example provide the latest drivers that better support recent hardware.)

Open a terminal, type `sudo apt update && sudo apt upgrade` (copy-pasting probably won't work yet) + <kbd>Enter</kbd>. It should ask you for your password. Type the password (it's invisible) + <kbd>Enter</kbd>. After an additional confirmation step, the command will update all installed software (packages) to their latest versions.

- `sudo` (_superuser do_) grants root privileges and is required for all system-relevant tasks
- `apt` is the command that manages installing/removing/updating most software on Ubuntu and Debian, which Ubuntu is based on
- `update` and `upgrade` are **arguments** that modify the command behavior (tell the command what to do):
  - The subcommand `apt update` updates the list of available packages and their versions in the configured sources (repositories)
  - `apt upgrade` uses this information to fetch and install packages that have new versions
- `&&` is an **operator** that connects commands; it executes the second command only if the first one completed successfully. You can also execute `apt update` and `apt upgrade` on two separate lines

After `apt` is finished (the command prompt returns and you can enter new commands), restart Linux. On a desktop VM, run `sudo reboot` (or use the desktop's log-out/restart menu); on WSL, run `wsl --shutdown` in PowerShell and then start your distribution again. Upon restart, there should be no apparent changes. To make sure that you have the latest software versions, you can repeat the command `sudo apt update && sudo apt upgrade`; this time, `apt` should tell you that there is nothing to update.

### Installing software

Install software with `sudo apt install <package>`, e.g. `sudo apt install htop`. Some tutorials use `apt-get` instead of `apt`; the differences are marginal.

Apart from `apt`, Ubuntu increasingly uses a second package management system, **Snap**. Some applications like Firefox or Chromium are only available as snap packages. Snaps update automatically, or manually with `snap refresh`.

For **scientific software**, you will usually use neither of these, but conda — see [Install Miniforge (conda)](install_conda.md).

*Further reading: [what Snap is](https://snapcraft.io/about) · [managing snap updates](https://snapcraft.io/docs/managing-updates)*

## Keep an eye on the system state

Keeping track of the system state — processor load, RAM usage, swap usage, network usage and disk usage — helps to diagnose problems. For example, if RAM and swap space are filled up, the system will freeze.

In the terminal, `htop` (install with `sudo apt install htop`) gives you a live overview on any platform, and `df -h` shows disk usage.

On a desktop you can also keep a permanent readout in view, which is worth doing:

- **Xubuntu/Xfce**: add the [system load monitor](https://docs.xfce.org/panel-plugins/xfce4-systemload-plugin/start) to the [Xfce panel](https://docs.xfce.org/xfce/xfce4-panel/start), by right-clicking on the panel and selecting `Panel` → `Add New Items`.
- **Ubuntu/GNOME**: install a [system monitor extension](https://extensions.gnome.org/extension/6807/system-monitor/) from [extensions.gnome.org](https://extensions.gnome.org/).

**WSL**: `htop` and `df -h` work as described above, but they only show the Linux side of things. Windows sees your entire Linux environment as a *single* process, called `Vmmem` (or `vmmemWSL` on newer builds), in the Task Manager (<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Esc</kbd>). The two views answer different questions: use the Task Manager to see what Linux is costing Windows overall, and `htop` inside Linux to see *which* program is responsible.

WSL claims memory dynamically as it needs it, and does not always hand it back to Windows promptly. If it takes too much, you can set an upper limit in a [`.wslconfig` file](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#example-wslconfig-file). Also note that `df -h` reports usage inside the Linux virtual disk, which grows on demand but does not shrink by itself — see [Troubleshooting](install_linux_in_wsl.md#troubleshooting) on the WSL page.

*Further reading: [GNOME disk usage analyzer](https://help.gnome.org/users/baobab/stable/)*

## Where to go from here

This section *is* a list of links — pick one, don't read them all.

**Learn the command line.** Even though some tasks like software installation can be done via GUIs, they are just frontends to command-line tools like `apt`, and it's preferable to use the original thing. Linux GUIs can also be buggy, because neither users nor developers like them very much.

- Start here: [Software Carpentry's shell lesson](https://swcarpentry.github.io/shell-novice/) (thorough, aimed at researchers)
- Prefer video? [Introduction to Linux and the command line](https://www.youtube.com/watch?v=oxuRxtrO2Ag)
- Prefer a book-length treatment? [linuxcommand.org](https://linuxcommand.org/)
- Prefer learning by doing? [an interactive course](https://linuxsurvival.com/), or [Bandit, a hacking game](https://overthewire.org/wargames/bandit/)
- Keep a **cheat sheet**: [devhints.io](https://devhints.io/bash) to start with — but a text file of your own commands will serve you better than either
- Look up a command: `man ls` for the full manual, or the friendlier [TLDR pages](https://tldr.inbrowser.app/) for examples (try `ls`)

**Other things worth doing:**

- Learn a non-GUI text editor — [nano](https://www.howtogeek.com/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/) is enough to start, [vim](https://www.youtube.com/watch?v=ggSyF1SVFr4) if you're ambitious. You will need one on the compute servers.
- Install conda: [Install Miniforge (conda)](install_conda.md)
- Browse the [general information](general_info.md) page for further books, tutorials and videos

AI tools like Claude, ChatGPT or Gemini are useful for discussing Linux and command-line questions. As always with LLMs, don't take the results for granted, especially for non-trivial questions — always double-check them.
