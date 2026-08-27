<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>Install Miniforge (conda)</H1>

* TOC
{:toc}

Once you have a working Linux environment — [WSL](install_linux_in_wsl.md), [a VM on Apple silicon](install_linux_on_apple_silicon.md), or [VirtualBox](install_linux_in_virtualbox.md) — come back here to install conda. The only difference between platforms is which installer file you download.

## What is Miniforge, and why not Anaconda?

[Miniforge](https://github.com/conda-forge/miniforge) is a minimal installer for **conda**, the package and environment manager we use throughout the curriculum. It comes preconfigured for the [conda-forge](https://conda-forge.org/) channel, which — together with the [bioconda](https://bioconda.github.io/) channel — is where essentially all the bioinformatics software you'll need is published.

You may have heard of **Anaconda** instead. Anaconda is a much larger distribution that bundles conda together with hundreds of preinstalled packages. We don't use it, for two reasons:

- Its `defaults` channel is [no longer recommended](https://bioconda.github.io/) for bioinformatics work — bioconda dropped support for it in 2024, and [conda-forge](https://conda-forge.org/docs/user/transitioning_from_defaults/) and [Bioconda](https://bioconda.github.io/faqs.html#what-s-the-difference-between-anaconda-conda-miniconda-mamba-mambaforge-micromamba) both recommend Miniforge.
- Anaconda's terms of service have changed several times and have at times required a paid license for larger organizations, which has led to considerable confusion. Miniforge avoids the question entirely.

Miniforge is also a fraction of the size. Anything Anaconda preinstalls can be added to an environment on demand, and building small per-project environments is better practice anyway.

## Install it inside Linux

Install Miniforge **inside your Linux environment** — not the Windows or macOS version, and not both. Mixing a host installation with a Linux one is a common source of confusing errors later.

Pick the installer that matches your setup:

| Your setup | Installer |
| --- | --- |
| WSL on Windows | `Miniforge3-Linux-x86_64.sh` |
| VirtualBox (Windows or Intel Mac) | `Miniforge3-Linux-x86_64.sh` |
| UTM or VMware Fusion on Apple silicon | `Miniforge3-Linux-aarch64.sh` |

If you're unsure, run `uname -m` inside Linux: it prints `x86_64` or `aarch64`.

```bash
cd ~
wget https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh
bash Miniforge3-Linux-x86_64.sh
```

On Apple silicon, substitute `aarch64` for `x86_64` in both lines. An `x86_64` installer will not run on an ARM guest.

This download link always points at the newest release, so there is no version number to keep up to date.

Follow the prompts: read (or page through with <kbd>Space</kbd>) and accept the license, accept the default install location, and answer "yes" when asked whether to run `conda init`. Then close and reopen your terminal. Your prompt should now begin with `(base)`, showing that the conda base environment is active.

### Check that everything worked

```bash
conda --version
python --version
which python
```

`which python` should print a path inside your Miniforge directory (e.g. `/home/<username>/miniforge3/bin/python`), not `/usr/bin/python`. This tells you which Python you are actually running — a distinction that will matter later.

## Create your working environment

Don't install packages into `base`. Instead, create a separate **environment** for your work. An environment is simply a self-contained directory where software is installed. If you ever break it, you can simply delete it and recreate it, without touching your conda installation. To create a new `bioinf` environment and install several software packages, starting with Python:

```bash
conda create -n bioinf python jupyterlab numpy pandas matplotlib scikit-learn biopython
conda activate bioinf  # activate new environment
```

Your prompt changes from `(base)` to `(bioinf)` to show which environment is active. You need to run `conda activate bioinf` in each new terminal; we'll make this automatic later.

The name `bioinf` is arbitrary in principle — but please keep it, as later course instructions may refer to it by name.

To start over (just for demonstration purposes), remove the environment and create it again:

```bash
conda env remove -n bioinf
# Recreate as shown above, using the `conda create` command
```

## Notes and further reading

- **On Apple silicon**, if you run into problems inside the VM, you can also install Miniforge directly on the macOS host; be sure to use the macOS `arm64` installer ([conda-forge.org/download](https://conda-forge.org/download/)).
- [Miniforge on GitHub](https://github.com/conda-forge/miniforge)
- [conda-forge documentation](https://conda-forge.org/docs/user/introduction/)
- [conda cheat sheet](https://docs.conda.io/projects/conda/en/latest/user-guide/cheatsheet.html)
