<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>Install Ubuntu in WSL (Windows)</H1>

* TOC
{:toc}

This is now the **recommended way to get a Linux environment on Windows**. (As a fallback option, also follow the [VirtualBox tutorial](install_linux_in_virtualbox.md) to install a full virtual machine.) If you use a Mac with Apple silicon, follow the [Apple silicon tutorial](install_linux_on_apple_silicon.md) instead.

**Note**: Please make a full backup of your computer before making any modifications.

## What is WSL, and why do we use it?

The [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/) (WSL) is a feature built into Windows 10 and 11 that runs a real Linux system alongside Windows. WSL 2, the current version, runs an actual [Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel) in a lightweight, tightly integrated virtual machine that Windows manages for you.

The important point for us: what you get is **a real Ubuntu system**. The same `apt` package manager, the same `sudo`, the same file hierarchy, the same Bash shell as on a regular Linux OS. Everything you will learn about the shell applies unchanged.

Compared to a full virtual machine in VirtualBox, WSL:

- installs with **a single command**, with no ISO download, no installer to click through, and no [guest additions](install_linux_in_virtualbox.md) to configure afterwards
- **shares memory and disk dynamically** with Windows, instead of reserving a fixed amount up front
- integrates with **Visual Studio Code** so that you can edit files in your familiar Windows editor while all code runs in Linux (this is the main practical advantage, see [below](#visual-studio-code))
- starts in about a second, rather than booting an operating system

What you *don't* get is a Linux desktop environment (no Xfce, no GNOME, no wallpaper). You only get a terminal. This is perfectly fine: it is also how you will work on the FH compute servers, where there is no desktop either.

Additional videos:

- "WSL Explained: Run Linux on Windows + Docker Like a Pro" by Techies Lounge 01/2026 ([YouTube](https://www.youtube.com/watch?v=wcXiZcpW5Gg))
- "What Is The Windows Subsystem for Linux (WSL) For?!" by Michael Horn, 06/2025 ([YouTube](https://www.youtube.com/watch?v=EAROgwvOV4s)) – examples of use cases

## Requirements

- Windows 10 version 2004 (build 19041) or later, or Windows 11. Check with <kbd>Win</kbd> + <kbd>R</kbd> → type `winver` → Enter.
- **Virtualization enabled** in your BIOS/UEFI. On most laptops this is already the case. You can check in the Task Manager (<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Esc</kbd>) → Performance → CPU → "Virtualization: Enabled". If it says Disabled, you need to enable it in your BIOS/UEFI setup, as explained e.g. [here](https://support.microsoft.com/en-us/windows/experience/enable-virtualization-on-windows).
- Administrator rights for the initial installation (a single command). If this is a managed company laptop and you don't have them, contact IT.
- About 20 GB of free disk space to start with; this grows as you install software.

## Installation

Some possibly helpful YouTube videos:

- "Install Windows Subsystem for Linux - WSL2 and Linux Ubuntu in Windows 11" by Aleksandar Haber PhD, 01/2025 ([YouTube](https://www.youtube.com/watch?v=1XuoUlaIEFo))
- "Running Linux on Windows with WSL 2" by Programming with Dr. Hayes, 01/2022 ([YouTube](https://www.youtube.com/watch?v=qPMsV1DSGJY)) – for additional details

Open **PowerShell as administrator** (right-click the Start button → "Terminal (Admin)" or "Windows PowerShell (Admin)") and run:

```powershell
wsl --install
```

This one command enables the required Windows features, downloads the Linux kernel, sets WSL 2 as the default, and installs Ubuntu ([learn.microsoft.com](https://learn.microsoft.com/en-us/windows/wsl/install)). **Restart your computer** when prompted.

You may have to run the command twice: the first run installs WSL itself, the second one downloads and installs Ubuntu. If WSL is installed afterwards but Ubuntu is still missing, see [Troubleshooting](#troubleshooting) below.

After the restart, open Ubuntu from the Start menu (just type "Ubuntu"). On first launch it unpacks itself and then asks you to create a **username** and **password**:

- These are your *Linux* username and password. They have nothing to do with your Windows login or your FH account.
- Use a simple lowercase username without spaces, e.g. your first name.
- **While typing the password, nothing appears on screen** — no dots, no asterisks. This is normal ("blind typing") and is standard behavior on Linux. Type it and press Enter.
- This account is the Linux administrator: it can run `sudo` ("super user do") to execute commands with administrative privileges.

If you forget the password later, you can reset it: in PowerShell run `wsl -u root`, then `passwd <username>`.

Now update the system's software packages — do this regularly, Windows will not do it for you:

```bash
sudo apt update && sudo apt upgrade
```

`apt update` refreshes the list of available packages, and `apt upgrade` actually installs the newer versions. You will be asked for your Linux password. See [Ubuntu basics](ubuntu_basics.md) for what these commands do in more detail.

### Check that everything worked

In PowerShell:

```powershell
wsl --list --verbose
```

You should see your Ubuntu distribution with `VERSION` set to `2`. (WSL 1 is an older, slower implementation without a real Linux kernel; you don't want it.)

### Install Windows Terminal

[Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/) is a much better terminal application than the default console window: tabs, split panes, proper Unicode support, sensible copy-paste, and configurable fonts and colors. On Windows 11 it is already installed; otherwise get it from the Microsoft Store. Your Ubuntu installation appears automatically as a profile in it.

You can set Ubuntu as the [default startup profile](https://learn.microsoft.com/en-us/windows/terminal/customize-settings/startup) so that a new terminal window opens directly in Linux.

## Where to put your files

**You now have two file systems**:

- the **Linux** file system, where your Linux home directory `/home/<username>` lives (`~` is a shorthand for it)
- the **Windows** file system, your usual `C:\`, which WSL makes visible inside Linux under `/mnt/c/`

You can access files across the boundary, but doing so is substantially **slower**, because every file operation has to cross between the two systems. Programs that watch files for changes (like Jupyter or VS Code) may also misbehave.

The rule is simple:

> **Keep your course files and projects in your Linux home directory** (`~/`, i.e. `/home/<username>/`). **Do not** work in `/mnt/c/Users/...`.

So: `~/bio-data-science/project1` — good. `/mnt/c/Users/YourName/Documents/project1` — bad.

Some practical consequences:

- To open your current Linux directory in the Windows File Explorer, run `explorer.exe .` (note the dot at the end). You can drag files in and out of that window, or pin it to Quick Access.
- In the File Explorer address bar, your Linux files are also reachable at `\\wsl.localhost\Ubuntu\home\<username>`. (You may also see the older form `\\wsl$\Ubuntu\...`, which still works, but only while the distribution is already running — `wsl.localhost` starts it for you.)
- Downloading a file with your Windows browser puts it in `C:\Users\...\Downloads`, i.e. on the Windows side. Move it into your Linux home before working on it, e.g. `mv /mnt/c/Users/YourName/Downloads/data.csv ~/`.
- Alternatively, download directly inside Linux with `wget <url>` or `curl -O <url>`, which puts the file where you want it in the first place.

## Visual Studio Code

VS Code is a very popular code editor / development environment. It runs as a normal Windows application, but with the [WSL extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) it starts a small server inside Linux and does all the actual work there. The editor, your extensions, the integrated terminal, the Python interpreter, the debugger — all of it operates inside Ubuntu, while the window itself is a native Windows window.

1. Install [Visual Studio Code](https://code.visualstudio.com/Download) **on Windows** (not inside Linux — do not use `apt` for this).
2. During installation, leave "Add to PATH" enabled.
3. Install the [WSL extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) in VS Code.
4. In your Ubuntu terminal, navigate to a project directory and run `code .` (again, note the dot, which means "the current directory").

The first time, this downloads the VS Code server into Linux; afterwards it is instant. The [bottom-left corner](https://code.visualstudio.com/docs/remote/wsl) of the window shows a green indicator reading `WSL: Ubuntu`, which tells you that you are connected to Linux.

Note that extensions are installed either on the Windows side or the Linux side. Language-related extensions (Python, Jupyter) belong on the Linux side; VS Code will usually prompt you and offer an "Install in WSL" button.

Also see:
- [learn.microsoft.com](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-vscode)
- [VS Code WSL tutorial](https://code.visualstudio.com/docs/remote/wsl-tutorial)

## Install Miniforge (conda)

With Linux in place, install **conda**, the package and environment manager we use throughout the curriculum. The instructions are the same for every platform and live on their own page: [Install Miniforge (conda)](install_conda.md).

- Install it **inside WSL**, using the `x86_64` installer — not the Windows version of Miniforge, and not both.
- Your environment will be called `bioinf`; the rest of this page assumes it is active.

## Run Jupyter

Start JupyterLab from your Linux terminal, with your environment active:

```bash
conda activate bioinf
cd ~
jupyter lab
```

WSL forwards network ports to Windows automatically, so the link printed in the terminal (something like `http://localhost:8888/lab?token=...`) simply opens in your normal Windows browser. In many cases the browser opens by itself; if it doesn't, <kbd>Ctrl</kbd>-click the link or copy it into the address bar.

Press <kbd>Ctrl</kbd> + <kbd>C</kbd> twice in the terminal to shut the server down when you are finished.

Alternatively, you can open `.ipynb` notebook files directly in VS Code, which has built-in Jupyter support.

## Back up your Linux system

Just like a VirtualBox snapshot, WSL lets you save the complete state of your Linux installation and restore it later. Do this once your environment is set up and working, and then from time to time.

To save (from PowerShell):

```powershell
wsl --export Ubuntu D:\backups\ubuntu-backup-2026-09-01.tar
```

Choose a location with enough free space; the file will be several GB. Including the date in the filename makes it easy to keep several versions.

To restore into a fresh distribution:

```powershell
wsl --import UbuntuRestored D:\wsl\UbuntuRestored D:\backups\ubuntu-backup-2026-09-01.tar
wsl -d UbuntuRestored
```

**Important:** an imported distribution logs you in as **root**, not as your normal user. Imported distributions have no launcher, so WSL has nowhere to record a default user ([learn.microsoft.com](https://learn.microsoft.com/en-us/windows/wsl/basic-commands#change-the-default-user-for-a-distribution)). Working as root is a bad habit and makes it easy to damage the system by accident, so fix it by creating the file `/etc/wsl.conf` inside Linux:

```ini
[user]
default=<your-username>
```

You can create it with `sudo nano /etc/wsl.conf`. Then run `wsl --terminate UbuntuRestored` in PowerShell and start the distribution again; you should now land as your normal user (check with `whoami`).

It's easiest to create this file *before* you export, so every future backup already carries it.

To start over completely, `wsl --unregister Ubuntu` deletes the distribution **and everything in it**, after which `wsl --install -d Ubuntu` gives you a clean system. This is the WSL equivalent of reinstalling the VM — useful when you have broken something beyond repair, and a good reason not to be afraid of experimenting.

Command reference: [learn.microsoft.com](https://learn.microsoft.com/en-us/windows/wsl/basic-commands)

## Useful commands

Run these in **PowerShell**, not inside Linux:

| Command | Meaning |
| --- | --- |
| `wsl` | Enter your default Linux distribution |
| `wsl --status` | View your general WSL configuration |
| `wsl --list --verbose` | List installed distributions and their WSL version |
| `wsl --shutdown` | Stop all distributions (the standard fix when something misbehaves) |
| `wsl --update` | Update the WSL platform itself |
| `wsl --export <distro> <file.tar>` | Back up a distribution |
| `wsl --unregister <distro>` | Delete a distribution and all its data |

And inside **Linux**:

| Command | Meaning |
| --- | --- |
| `explorer.exe .` | Open the current directory in the Windows File Explorer |
| `code .` | Open the current directory in VS Code |
| `cd ~` | Go to your Linux home directory |
| `sudo apt update && sudo apt upgrade` | Update installed software |

## Troubleshooting

**"Please enable the Virtual Machine Platform Windows feature"** or an error mentioning virtualization
: Virtualization is disabled in your BIOS/UEFI. Reboot into the firmware settings and enable it (it is called VT-x, Intel Virtualization Technology, AMD-V, or SVM Mode, depending on the manufacturer).
: If virtualization is already enabled there, the Windows feature itself may be switched off instead — see the next entry.

**WSL was installed, but Ubuntu was not**
: Two Windows features have to be switched on. Press <kbd>Win</kbd>+<kbd>R</kbd>, type `optionalfeatures` and press <kbd>Enter</kbd> to open "Turn Windows features on or off" ("Windows-Features aktivieren oder deaktivieren"). Tick *Virtual Machine Platform* ("Plattform für virtuelle Computer") and *Windows Subsystem for Linux* ("Windows-Subsystem für Linux"), confirm, and reboot. Then run `wsl --install` again.

**Everything feels slow**
: Almost always this means you are working in `/mnt/c/...` instead of your Linux home directory. Run `pwd` to check where you are; if the path starts with `/mnt/`, move your files (see [above](#where-to-put-your-files)).
: The second common cause is antivirus software scanning the WSL virtual disk. Add an exclusion for it in Windows Security → Virus & threat protection → Manage settings → Exclusions — see [Finding the WSL virtual disk](#finding-the-wsl-virtual-disk) below for how to locate the file.

**WSL hangs, or a distribution won't start**
: Run `wsl --shutdown` in PowerShell and start it again. This resolves a surprising share of problems.

**`code .` doesn't work**
: Make sure VS Code was installed on Windows with the "Add to PATH" option, and that you have restarted your terminal since installing it.

**The disk keeps growing and doesn't shrink**
: The virtual disk grows on demand but does not automatically shrink when you delete files. This is normal, and usually not worth worrying about.
: If you do need the space back, see [learn.microsoft.com](https://learn.microsoft.com/en-us/windows/wsl/disk-space) for how to compact it. There is also a setting that lets WSL reclaim space automatically, `wsl --manage Ubuntu --set-sparse true` (requires WSL 2.0.5+ and Windows 11 23H2). Note that Microsoft has disabled this by default at times over concerns about data corruption, so **make a backup with `wsl --export` before enabling it**, and don't turn it on unless you actually need it.

**VirtualBox stopped working after installing WSL**
: WSL 2 uses Hyper-V, which does not coexist well with VirtualBox. Older VirtualBox versions may refuse to start 64-bit VMs or become very slow. Use one or the other; if you need both, update VirtualBox to the latest version, which handles this considerably better.

### Finding the WSL virtual disk

All your Linux files live inside a single file called `ext4.vhdx`. Where Windows keeps it depends on how WSL was installed, so rather than guessing, ask Windows directly — run this in PowerShell ([learn.microsoft.com](https://learn.microsoft.com/en-us/windows/wsl/disk-space#how-to-locate-the-vhdx-file-and-disk-path-for-your-linux-distribution)):

```powershell
(Get-ChildItem -Path HKCU:\Software\Microsoft\Windows\CurrentVersion\Lxss | Where-Object { $_.GetValue("DistributionName") -eq 'Ubuntu' }).GetValue("BasePath") + "\ext4.vhdx"
```

Typically the result is somewhere under `%LOCALAPPDATA%\Packages\CanonicalGroupLimited.Ubuntu...\LocalState\`, or under `%LOCALAPPDATA%\wsl\` for newer installations. If you are adding an antivirus exclusion, exclude the folder containing this file.

Do not move, edit or open this file with Windows tools — that is a reliable way to corrupt your Linux installation. To get at your Linux files, use `\\wsl.localhost\Ubuntu\` or `explorer.exe .` instead.

For anything else, search the [WSL issue tracker](https://github.com/microsoft/WSL/issues) or the [troubleshooting guide](https://learn.microsoft.com/en-us/windows/wsl/troubleshooting).

Hint: If an explanation here is too brief or technical, or a command doesn't behave as expected, you can discuss it with an LLM like Claude, Gemini or ChatGPT. However, these tools sometimes give wrong or imprecise information — the authoritative source is still the technical documentation.

## Where to go from here

- Get comfortable with the shell: [linuxcommand.org](http://linuxcommand.org/), [swcarpentry.github.io](https://swcarpentry.github.io/shell-novice/)
- The [general information](general_info.md) page lists further books, tutorials and videos
- **[Ubuntu basics](ubuntu_basics.md)** covers the shell, the file system, and package management with `apt` — all of it applies to WSL
