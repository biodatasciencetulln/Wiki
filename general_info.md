<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">

<H1 style="color:dimgray">Introductory information, resources and recommendations</H1>

FH Tulln, Bio Data Science  

## Laptop specifications

A portable laptop is required for a number of courses.

- CPU: Intel Core i3/i5/i7 or equivalent AMD processor; Atom, Celeron, or similar processors (mostly used in netbooks) are too slow
- Memory: at least 8 GB RAM
- Storage: SSD highly recommended, at least 256 GB
- Operating system: Windows, MacOS or Linux
- GPU: irrelevant
- Screen size: Whatever works for you (at least 13 inches is recommended)
- Overall system performance: You can assess it based on the startup time of a program like Firefox. Ideally, it should take no more than 3-4 seconds.

## Virtual machine

**Note:** Please make a full backup of your data/operating system before any modifications to your computer.

A virtual machine provides a convenient way of working with other operating systems (OS) than the one currently installed on your computer. [This video](https://www.youtube.com/watch?v=yIVXjl4SwVo) briefly explains what an OS and what a virtual machine is. (If you are interested in more details, [this video](https://www.youtube.com/watch?v=26QPDBe-NB8&) gives a condensed overview of the history and basic functionality of computer OSes.) Briefly, a virtual machine is a simulated computer (where you can install an OS, called "guest") that runs on your actual computer (with the host OS). It is a great way to learn and experiment with Linux and programming, because you can install it under Windows or MacOS start/close it as any other program. (There are some more [advantages](https://www.makeuseof.com/tag/reasons-start-using-virtual-machine/).) The virtual machine is saved as a file (or folder) on your hard drive and can be easily copied, duplicated, backed up etc. You can play with it and modify it in any way you like, and if it is broken beyond repair, you can simply restore it from an earlier backup by copying the corresponding folder back into place. 

We will use Virtualbox ([download page](https://www.virtualbox.org/wiki/Downloads)), which is a free program available for all OSes, and allows e.g. to run a Linux OS on Windows. Linux comes in different flavors (called distrubitions), with Ubuntu being the most popular one. I suggest to use the latest Xubuntu (current release 20.04, [download page](https://xubuntu.org/download/)), which is Ubuntu with a more lightweight and responsive desktop environment (called Xfce, therefore **X**ubuntu). [This video](https://www.youtube.com/watch?v=sB_5fqiysi4) shows how to download and install Ubuntu in Virtualbox; the process is equivalent for Xubuntu. (You might run into some problems, e.g. the option `Ubuntu (64 bit)` might not be available, because you need to activate VT-x/AMD-v in the host PC [BIOS](https://www.youtube.com/watch?v=SlzwMKcCoMI) first, as explained on the [virtualbox forum](https://forums.virtualbox.org/viewtopic.php?f=1&t=62339) or on [superuser.com](https://superuser.com/questions/1241956/virtualbox-only-allowing-32-bit-os). Also, after installing and booting your new OS, you will need to install the [guest additions](https://www.itzgeek.com/post/how-to-install-virtualbox-guest-additions-on-ubuntu-20-04/), essentially a collection of Virtualbox-related drivers, for a fully functional virtual machine.)

Note that Windows also provides a built-in [Windows Subsystem for Linux](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux), that allows to run the Linux command line and some utilities directly on Windows. This also works via a type of virtual machine, and can be useful in some cases. However, a fully fledged virtual machine is more convenient for us.

## Linux and Bash

[Linux](https://en.wikipedia.org/wiki/Linux) is a free OS, which is stable yet highly customizeable, actively developed, and offers a huge selection of free software development tools. A lot of good scientific software is written only for Linux - e.g. almost all short read aligners, assemblers, and many more. Some advantages are:

* Software can be installed in an automated way using a package manager (similar to an app store)
* Software can be installed by the user without administrator priviledges and easily configured in different ways (this is much harder in Windows)
* Linux is very safe, malware is rare

Linux includes the [shell](http://linuxcommand.org/lc3_lts0010.php), a command-line interpreter/scripting language that can execute built-in shell commands, Linux utilities and programs. It is a powerful and versatile tool, and very useful e.g. for working with text files, which is a frequent situation in biological data analysis. The shell allows to easily build pipelines using built-in and other tools, e.g. for sorting/cutting/restructuring text files and feeding the result into other programs. It is one of the most important tools for bio data science, and you should try to get comfortable with it early on.

Several shell programs are available, but most Linux distributions come with the [Bash shell](https://en.wikipedia.org/wiki/Bash_(Unix_shell)). A [terminal emulator](https://dev.to/nestedsoftware/comment/4a33) is a program that opens a window and lets you interact with the shell. Different flavors of Ubuntu use different terminals, e.g. Xubuntu uses the [Xfce 4 terminal emulator](https://superuser.com/a/269252). [Here](https://docs.xubuntu.org/current/user/C/command-line.html) is how to open Bash on Xubuntu, and a listing of some important commands. [This video](https://www.youtube.com/watch?v=V_gODEnrxI0) gives a brief Xubuntu tour.

Some recommended Bash introductory tutorials/resources:

- YouTube: ["Linux Tutorial - Basic Command Line"](https://www.youtube.com/watch?v=cBokz0LTizk)
- YouTube: ["Beginner's Guide to the Bash Terminal"](https://www.youtube.com/watch?v=oxuRxtrO2Ag)
- [linuxcommand.org](http://linuxcommand.org/)
- [swcarpentry.github.io](https://swcarpentry.github.io/shell-novice/)

Hint: If you find a useful Youtube channel, you might want to subscribe and/or check out their other videos.

Books:

- B. Ward: "How Linux Works" ([Amazon](https://www.amazon.de/How-Linux-Works-Brian-Ward/dp/1718500408))
- W. Shotts: "The Linux Command Line: A Complete Introduction" ([Amazon](https://www.amazon.de/Linux-Command-Line-2nd-Introduction/dp/1593279523/))


## Python

It's not very important which resource for learning Python you pick, as most of them present very similar content (the basics of the Python programming language) in different forms. It's only important that the way in which the information is presented makes sense to you. Pick a resource that works well for you and stick to if possible. You can also talk to your fellow students to exchange experiences and recommendations.

### Development environment

A development environment are programs and tools that you use for writing, testing and debugging code. You can use a text editor for that, but [integrated development environments](https://www.codecademy.com/articles/what-is-an-ide) provide many features that will make your life easier and (hopefully) improve your code. You can install the programs listed below in the virtual machine, or (for testing) on your regular OS. 

One great way to learn Python is to simply run it online. There are several good resources for that, e.g.

- [Google Colab](https://colab.research.google.com) — Jupyter notebook in the cloud (via Google drive), with real-time collaboration ([short YouTube intro](https://www.youtube.com/watch?v=inN8seMm7UI))
- [Repl.it](https://repl.it/languages/python3) — A browser-based IDE, that supports over 50 programming languages, including Python

To run Python locally, the most convenient way is to use a *Python distribution* like [Anaconda](https://en.wikipedia.org/wiki/Anaconda_(Python_distribution)), which includes not only the Python interpreter but also a number of useful libraries and programs, including the development environments Jupyter, Spyder and VS Code (and others, like RStudio for R development). You can e.g. try Jupyter and Spyder, which are both great environments.

Hint: If you use [Spyder](https://www.spyder-ide.org/), a good place to start is the `Spyder tutorial`, accessible via `Help` → `Spyder tutorial`.

### Books/tutorials

- ["A Byte of Python"](https://python.swaroopch.com/) (free ebook)
- ["Think Python: How to Think Like a Computer Scientist"](https://greenteapress.com/wp/think-python-2e/) (free ebook)
  - ["How to Think Like a Computer Scientist: Interactive Edition"](https://runestone.academy/runestone/books/published/thinkcspy/index.html) (interactive edition)
- E. Freeman: "Head First Learn to Code: A Brain-Friendly Guide" ([Amazon](https://www.amazon.de/Head-First-Learn-Code-Brain-Friendly/dp/1491958863/), very beginner-friendly, if you like the book's approach)
- E. Matthes: "Python Crash Course: A Hands-On, Project-Based Introduction to Programming" ([Amazon](https://www.amazon.de/Python-Crash-Course-Eric-Matthes/dp/1593279280/))
- L. Ramalho: "Fluent Python: Clear, Concise, and Effective Programming", ([Amazon](https://www.amazon.de/Fluent-Python-Concise-Effective-Programming-ebook/dp/B0131L3PW4/))
- B. Slatkin: "Effective Python: 59 Specific Ways to Write Better Python" ([Amazon](https://www.amazon.de/Effective-Python-Specific-Software-Development-ebook/dp/B00TKGY0GU/); advanced, not beginner-friendly)
- [Official Python tutorial](https://docs.python.org/3/tutorial/)

### Videos/YouTube channels

- ["Python Tutorial for Absolute Beginners #1 - What Are Variables?" (CS Dojo)](https://www.youtube.com/watch?v=Z1Yd7upQsXY)
- ... many others ...

### Online platforms and other resources

- [python-guide.org: useful links](https://docs.python-guide.org/intro/learning/)
- [learnpython.org](https://www.learnpython.org/)
- [codecademy.com](https://www.codecademy.com/learn/learn-python-3) and similar interactive learning resources
- [**The Carpentries**](https://carpentries.org/):
  - [Software Carpentry](https://software-carpentry.org/)
  - [Data Carpentry](https://datacarpentry.org/)
  
Hint: Problem-oriented tutorials (that solve little tasks rather than just presenting information) are usually more fun and provide better understanding.
