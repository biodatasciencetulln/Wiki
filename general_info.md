<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>General information, resources and recommendations</H1>

* TOC
{:toc}

## Biological background

A solid biological background is indispensible for all courses of the curriculum. This general textbook provides a comprehensive overview and can be used for studying and as a reference:

- Urry et al.: "Campbell Biology" ([amazon.com](https://www.amazon.com/Campbell-Biology-11th-Lisa-Urry/dp/0134093410), [pearson-studium.de](https://www.pearson-studium.de/campbell-biologie_3.html))

## Laptop specifications

A portable laptop is required for a number of courses. Minimum specifications:

- CPU: Intel Core i3/i5/i7 or equivalent AMD processor; Atom, Celeron, or similar processors (mostly used in netbooks) are too slow
- Memory: 8 GB RAM
- Storage: SSD highly recommended, at least 256 GB
- Operating system: Windows, macOS or Linux
- GPU: irrelevant
- Screen size: Whatever works for you (at least 13 inches is recommended)
- Overall system performance: You can assess it based on the startup time of a program like Firefox. Ideally, it should take no more than 3-4 seconds.

## Virtual machine

**Note:** Please make a full backup of your computer before making any modifications.

Virtual machines (VMs) allow you to run an operating system (OS) in an app window on your desktop that behaves like a full, separate computer. This virtual computer, the "guest", has its own emulated CPU, memory, network interface and storage, and you can install an OS on it just as you would on a real, physical machine. [This short video](https://www.youtube.com/watch?v=yIVXjl4SwVo) explains the basic terms. The [advantages](https://www.makeuseof.com/tag/reasons-start-using-virtual-machine/) are that you can try different OSes, run software your main OS can't, and try out apps in a safe, isolated environment. It's a great way to learn and experiment with an OS like Linux, because you can install it on Windows or macOS and run it like any other software. VMs are saved as folders with some files on your hard drive and can be copied, backed up and removed like any other folders. You can play with a VM and modify it as you like, and if it's broken beyond repair, you can quickly restore it from an earlier backup. Many people use VMs for their work on a regular basis. (By the way, do you know what an OS does? [This nice video](https://www.youtube.com/watch?v=26QPDBe-NB8&) approaches its basic functionality from a historical perspective.)

We will use [VirtualBox](https://www.virtualbox.org/wiki/Downloads), which is free software available for most OSes, and allows to run e.g. a Linux VM on Windows. Linux comes in different flavors (called [distributions](https://www.howtogeek.com/132624/htg-explains-whats-a-linux-distro-and-how-are-they-different/)), with Ubuntu being the most popular one. I suggest to use the latest [Xubuntu](https://xubuntu.org/download/), which is Ubuntu with the lightweight and responsive desktop environment Xfce instead of GNOME, therefore **X**ubuntu. [This video](https://www.youtube.com/watch?v=sB_5fqiysi4) walks you through the installation of Ubuntu in VirtualBox; the process is equivalent for Xubuntu. You might run into some problems, e.g. the option `Ubuntu (64 bit)` might not be available, because you need to activate VT-x/AMD-v in the host BIOS/UEFI first, as explained e.g. [here](https://superuser.com/questions/1241956/virtualbox-only-allowing-32-bit-os). Also, after installing and booting the guest OS, you will need to install the [guest additions](https://www.itzgeek.com/post/how-to-install-virtualbox-guest-additions-on-ubuntu-20-04/), a set of VirtualBox-related drivers and software, for a fully functional VM. [Click here for detailed instructions.](install_linux_in_virtualbox.md)

Note that Windows 10 now includes a built-in [Windows Subsystem for Linux](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux), that allows to run the Linux shell and command-line tools directly on Windows. This also works via a type of VM, and can sometimes be useful. However, a fully fledged VM is more convenient for us.

## Linux and Bash

[Linux](https://en.wikipedia.org/wiki/Linux) is a free OS, which is stable yet highly customizable, actively developed, and offers a huge selection of free software development tools. A lot of scientific software is written only for Linux - e.g. almost all short read aligners, assemblers, and many more. Some advantages are:

* Linux is completely free and open-source and widely used
* Linux is very safe, malware is rare
* Software can be installed in an automated way using a package manager (similar to an app store)
* Software can be installed by the user without administrator privileges and easily configured in different ways (this is much harder in Windows)

Linux includes [the shell](http://linuxcommand.org/lc3_lts0010.php), a command-line interpreter/scripting language that can execute built-in shell commands, Linux utilities and programs. It is a powerful and versatile tool and very useful e.g. for working with text files, which is common in biological data analysis. The shell allows to easily build pipelines using different commands and utilities, e.g. for sorting/cutting/restructuring text files and feeding the result into other commands/utilities/programs. It is one of the most important tools in bio data science, and you should get comfortable with it early on.

Several shell programs exist. The most popular is [the Bash shell](http://linuxcommand.org/lc3_lts0010.php), it is default on most or all Linux distributions. A [terminal emulator](https://dev.to/nestedsoftware/comment/4a33) is a program that opens a window and lets you interact with the Bash shell. Different Ubuntu flavors use different terminals, e.g. Xubuntu has the Xfce 4 terminal emulator. [Here](https://docs.xubuntu.org/current/user/C/command-line.html) is how to open the terminal on Xubuntu, and a listing of some important commands.

Some recommended Bash introductory tutorials/resources:

- YouTube: ["Linux Tutorial - Basic Command Line"](https://www.youtube.com/watch?v=cBokz0LTizk)
- YouTube: ["Beginner's Guide to the Bash Terminal"](https://www.youtube.com/watch?v=oxuRxtrO2Ag)
- [linuxcommand.org](http://linuxcommand.org/)
- [swcarpentry.github.io](https://swcarpentry.github.io/shell-novice/)

Hint: If you find a useful YouTube channel, you might want to subscribe and/or check out their other videos.

Books:

- B. Ward: "How Linux Works" ([Amazon](https://www.amazon.de/How-Linux-Works-Brian-Ward/dp/1718500408))
- W. Shotts: "The Linux Command Line: A Complete Introduction" ([Amazon](https://www.amazon.de/Linux-Command-Line-2nd-Introduction/dp/1593279523/))


## Python

It's not very important which resource for learning Python you pick, as most of them present similar content (the basics of the Python programming language) in different ways. It's only important that the way in which the information is presented makes sense to you. Pick a resource that works well for you and stick to it if possible. You can also talk to your fellow students and exchange experiences and recommendations.

### Development environment

A development environment comprises programs and tools that you use for writing, testing and debugging code. You could use a simple text editor, but [integrated development environments (IDEs)](https://www.codecademy.com/articles/what-is-an-ide) provide many features that will make your life easier and your code better. 

**Online IDEs.** One great way to learn Python is to simply run it online. There are several good resources, e.g.

- [Google Colab](https://colab.research.google.com) — Jupyter notebook in the cloud (via Google drive), with real-time collaboration ([short YouTube intro](https://www.youtube.com/watch?v=inN8seMm7UI))
- [Repl.it](https://repl.it/languages/python3) — A browser-based IDE, that supports over 50 programming languages, including Python

**Local IDEs.** One way to install and run Python locally is via the *Python distribution* [Anaconda](https://stackoverflow.com/a/42096429) ([download page](https://www.anaconda.com/products/individual), [installation instructions](https://docs.anaconda.com/anaconda/install/)). You can install it in the VM, or (for testing, if you don't have a VM yet) on the host OS. Anaconda includes not only the Python interpreter but also many additional libraries and tools for data science, including the IDEs Jupyter, Spyder, VS Code and others, accessible via the [Anaconda navigator](https://docs.anaconda.com/anaconda/navigator/). All three are great IDEs with somewhat different strengths and main focus. Roll the dice and pick one to start with.

- [Spyder](https://www.spyder-ide.org/): Very learning-friendly IDE. A good place to start is the Spyder tutorial, `Help` → `Spyder tutorial`; also check out [this introductory video](https://www.youtube.com/watch?v=zYNRqVimU3Q)
- [Jupyter](https://en.wikipedia.org/wiki/Project_Jupyter): Great for presenting, storytelling and exploratory data analysis; not necessarily the best for learning to code or longer scripts. [Introductory video](https://www.youtube.com/watch?v=HW29067qVWk)
- [VS Code](https://en.wikipedia.org/wiki/Visual_Studio_Code): Very nice IDE, but not necessarily the best for complete beginners; if you want to try it, start [here](https://www.digitalocean.com/community/tutorials/getting-started-with-python-in-visual-studio-code) and continue [here](https://realpython.com/python-development-visual-studio-code/), [here](https://code.visualstudio.com/docs/python/python-tutorial) or [here](https://code.visualstudio.com/docs/getstarted/introvideos)

### Books/tutorials

- [w3schools.com Python tutorial](https://www.w3schools.com/python/) - interactive tutorial, for complete beginners
- ["A Byte of Python"](https://python.swaroopch.com/) - free beginner-friendly ebook; doesn't go too deep, but covers the basics
- E. Freeman: "Head First Learn to Code: A Brain-Friendly Guide" ([Amazon](https://www.amazon.de/Head-First-Learn-Code-Brain-Friendly/dp/1491958863/)) - very beginner-friendly, if you like the approach of the book series
- ["Think Python: How to Think Like a Computer Scientist"](https://greenteapress.com/wp/think-python-2e/) - free and very nice ebook, maybe not great for complete beginners; you'll learn a lot if you can work your way through it
  - ["How to Think Like a Computer Scientist: Interactive Edition"](https://runestone.academy/runestone/books/published/thinkcspy/index.html) - interactive edition
- E. Matthes: "Python Crash Course: A Hands-On, Project-Based Introduction to Programming" ([Amazon](https://www.amazon.de/Python-Crash-Course-Eric-Matthes/dp/1593279280/)) - practical introduction for complete beginners, with exercises
  - The author provides a collection of online resources, including some nice [cheat sheets](https://ehmatthes.github.io/pcc_2e/cheat_sheets/cheat_sheets/)
- A. Sweigart: "Automate the Boring Stuff with Python: Practical Programming for Total Beginners" ([Amazon](https://www.amazon.de/Al-Sweigart/dp/1593279922/)) - practically oriented introduction for beginners (ranges from beginners to somewhat advanced content)
- [Official Python tutorial](https://docs.python.org/3/tutorial/) - good reference for topics you already know, to refresh your memory or to go deeper

Hints: Practically oriented tutorials that solve little problems rather than just presenting information, are usually more fun and provide a better understanding of the material. When writing code based on some code template, do not copy-paste it, but re-type it yourself. This improves the learning result. 

**Advanced.**
- L. Ramalho: "Fluent Python: Clear, Concise, and Effective Programming", ([Amazon](https://www.amazon.de/Fluent-Python-Concise-Effective-Programming-ebook/dp/B0131L3PW4/)) - discussion of Python-specific language features, for Python programmers who want to improve their skills (not for complete beginners)
- B. Slatkin: "Effective Python: 59 Specific Ways to Write Better Python" ([Amazon](https://www.amazon.de/Effective-Python-Specific-Software-Development-ebook/dp/B00TKGY0GU/)) -  learn to write efficient and "Pythonic" code (advanced)

### Videos/YouTube channels

- ["Python Tutorial for Absolute Beginners #1 - What Are Variables?" (CS Dojo channel)](https://www.youtube.com/watch?v=Z1Yd7upQsXY)
- ["Python Tutorial for Beginners 1: Install and Setup for Mac and Windows" (Corey Schafer channel)](https://www.youtube.com/watch?v=YYXdXT2l-Gg&list=PL-osiE80TeTt2d9bfVyTiXJA-UTHn6WwU)

### Online platforms and other resources

- [python-guide.org: useful links](https://docs.python-guide.org/intro/learning/)
- [learnpython.org](https://www.learnpython.org/)
- [codecademy.com](https://www.codecademy.com/learn/learn-python-3), and similar interactive learning resources
- [The Carpentries](https://carpentries.org/):
  - [Software Carpentry](https://software-carpentry.org/)
  - [Data Carpentry](https://datacarpentry.org/)
- [Rosalind](http://rosalind.info/problems/locations/) - a platform for learning bioinformatics and programming through problem solving
  
### Staying updated

Connecting with other people from whom you can learn is both fun and helps staying updated. Here are some ideas:

- Twitter: look [here](https://www.youtube.com/watch?v=1hhuFrBNoLg) and maybe [here](https://www.youtube.com/watch?v=3471Vg3GaPI) 
- Reddit: look [here](https://analyticsindiamag.com/10-data-science-subreddits-every-tech-enthusiast-should-follow/)
- Podcasts: look [here](https://dbader.org/blog/ultimate-list-of-python-podcasts)
- Forums: [Stackoverflow](https://stackoverflow.com/), no way around it
