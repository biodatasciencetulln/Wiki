<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>General information, resources and recommendations</H1>

* TOC
{:toc}

## Biological background

A solid biological background is indispensible for all courses of the curriculum. This general textbook provides a comprehensive overview and can be used for studying and as a reference:

- Urry et al.: "Campbell Biology" ([amazon.com](https://www.amazon.com/Campbell-Biology-11th-Lisa-Urry/dp/0134093410), [pearson.de](https://www.pearson.de/campbell-biologie-9783868943665))

## Laptop specifications

A portable laptop is required for a number of courses. Minimum specifications:

- CPU: Intel Core i5 or equivalent (e.g. AMD Ryzen 5)
    - Atom, Celeron, and similar low-end processors are too slow
- Memory: 16 GB RAM (8 is possible, but may slow down your computer)
- Storage: ≥100 GB free space (SSD recommended)
- Operating system: Windows, macOS or Linux
- GPU: irrelevant
- Screen size: Whatever works for you (≥13 inches recommended)
- Overall system performance can be assessed based on the startup time of a program like Firefox. Ideally, it should take no more than 2-3 seconds

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

Several shell programs exist. The [Bash shell](http://linuxcommand.org/lc3_lts0010.php) is the most popular shell and the default on most or all Linux distributions. A [terminal emulator](https://dev.to/nestedsoftware/comment/4a33) is a program that opens a window and lets you interact with the Bash shell. Different Ubuntu flavors use different terminals, e.g. Xubuntu has the Xfce 4 terminal emulator. [Here](https://docs.xubuntu.org/current/user/C/command-line.html) is how to open the terminal on Xubuntu, and a listing of some important commands.

Some recommended Bash introductory tutorials/resources:

- YouTube: ["Linux Tutorial - Basic Command Line"](https://www.youtube.com/watch?v=cBokz0LTizk)
- YouTube: ["Beginner's Guide to the Bash Terminal"](https://www.youtube.com/watch?v=oxuRxtrO2Ag)
- [linuxcommand.org](http://linuxcommand.org/)
- [swcarpentry.github.io](https://swcarpentry.github.io/shell-novice/)

Hint: If you find a useful YouTube channel, you might want to subscribe and/or check out their other videos.

Books:

- B. Ward: "How Linux Works" ([Amazon](https://www.amazon.de/How-Linux-Works-Brian-Ward/dp/1718500408))
- W. Shotts: "The Linux Command Line: A Complete Introduction" ([Amazon](https://www.amazon.de/Linux-Command-Line-2nd-Introduction/dp/1593279523/), [ebook](http://linuxcommand.org/tlcl.php))


## Python

Together with R and Bash, Python is an essential part of the modern bioinformatics and data science toolkit ([reddit](https://www.reddit.com/r/bioinformatics/comments/lez284/the_real_question_r_vs_python/)). It's not very important which resource for learning Python you pick, as most of them present similar content (the basics of the Python programming language) in different ways. It's only important that the way in which the information is presented makes sense to you. Pick a resource that works well for you and stick to it if possible. You can also talk to your fellow students and exchange experiences and recommendations.

### Development environment

A development environment comprises programs and tools that you use for writing, testing and debugging code. You could use a simple text editor, but [integrated development environments (IDEs)](https://www.codecademy.com/articles/what-is-an-ide) provide many features that will make your life easier and your code better. 

**Online IDEs.** One great way to learn Python is to simply run it online. There are several good resources, e.g.

- [Replit](https://replit.com/languages/python3) — Browser-based IDE that supports many programming languages, including Python; has real-time collaboration
- [Google Colab](https://colab.research.google.com) — Jupyter notebooks in the cloud (via Google drive) ([YouTube intro](https://www.youtube.com/watch?v=inN8seMm7UI))
- [Deepnote](https://docs.deepnote.com/deepnote-crash-course-videos) — Data science notebooks in the cloud

**Local IDEs.** One way to install and run Python locally is via the *Python distribution* [Anaconda](https://stackoverflow.com/a/42096429) ([download page](https://www.anaconda.com/products/individual), [installation instructions](https://docs.anaconda.com/anaconda/install/)). You can install it in the VM, or (for testing, if you don't have a VM yet) on the host OS. Anaconda includes not only the Python interpreter but also many additional libraries and tools for data science, including the IDEs Jupyter, Spyder, VS Code and others, accessible via the [Anaconda navigator](https://docs.anaconda.com/anaconda/navigator/). All three are great IDEs with somewhat different strengths and main focus. Roll the dice and pick one to start with.

- [Spyder](https://www.spyder-ide.org/): Very learning-friendly IDE. A good place to start is the Spyder tutorial, `Help` → `Spyder tutorial`; also check out [this introductory video](https://www.youtube.com/watch?v=zYNRqVimU3Q)
- [Jupyter](https://en.wikipedia.org/wiki/Project_Jupyter): Great for presenting, storytelling and exploratory data analysis; not necessarily the best for learning to code or longer scripts. [Introductory video](https://www.youtube.com/watch?v=HW29067qVWk)
- [VS Code](https://en.wikipedia.org/wiki/Visual_Studio_Code): Popular code editor with many plugins, but not necessarily the best for complete beginners; if you want to try it, start [here](https://www.digitalocean.com/community/tutorials/getting-started-with-python-in-visual-studio-code) and continue [here](https://realpython.com/python-development-visual-studio-code/), [here](https://code.visualstudio.com/docs/python/python-tutorial) or [here](https://code.visualstudio.com/docs/getstarted/introvideos)

### Books/tutorials

- [w3schools.com Python tutorial](https://www.w3schools.com/python/) - interactive tutorial, for complete beginners
- ["A Byte of Python"](https://python.swaroopch.com/) - free beginner-friendly ebook; doesn't go too deep, but covers the basics
- ["Python for Everybody"](https://www.py4e.com/html3/) and [interactive edition](https://books.trinket.io/pfe/index.html), also see [here](https://runestone.academy/runestone/books/published/py4e-int/index.html) - free beginner-friendly ebook
- E. Freeman: "Head First Learn to Code: A Brain-Friendly Guide" ([Amazon](https://www.amazon.de/Head-First-Learn-Code-Brain-Friendly/dp/1491958863/)) - very beginner-friendly, if you like the approach of the book series
- ["Think Python: How to Think Like a Computer Scientist"](https://greenteapress.com/wp/think-python-2e/) - free and very nice ebook, maybe not great for complete beginners; you'll learn a lot if you work your way through it
  - ["How to Think Like a Computer Scientist: Interactive Edition"](https://runestone.academy/runestone/books/published/thinkcspy/index.html) - interactive edition
- E. Matthes: "Python Crash Course: A Hands-On, Project-Based Introduction to Programming" ([Amazon](https://www.amazon.de/Python-Crash-Course-Eric-Matthes/dp/1593279280/)) - practical introduction for complete beginners, with exercises
  - The author provides a collection of online resources, including some nice [cheat sheets](https://ehmatthes.github.io/pcc_2e/cheat_sheets/cheat_sheets/)
- A. Sweigart: "Automate the Boring Stuff with Python: Practical Programming for Total Beginners" ([Amazon](https://www.amazon.de/Al-Sweigart/dp/1593279922/), [online book](https://automatetheboringstuff.com)) - practically oriented introduction for beginners (ranges from beginners to somewhat advanced content)
- D. Amos et al.: "Python Basics: A Practical Introduction to Python 3", 4th edition ([Amazon](https://www.amazon.com/Python-Basics-Practical-Introduction/dp/1775093328/))
- [Official Python tutorial](https://docs.python.org/3/tutorial/) - good reference for topics you already know, to refresh your memory or to go deeper

Hints: Practically oriented tutorials that solve little problems rather than just presenting information, are usually more fun and provide a better understanding of the material. When writing code based on some code template, do not copy-paste it, but re-type it yourself. This improves the learning result. 

**Advanced.**

- L. Ramalho: "Fluent Python: Clear, Concise, and Effective Programming", ([Amazon](https://www.amazon.de/Fluent-Python-Concise-Effective-Programming-ebook/dp/B0131L3PW4/)) - discussion of Python-specific language features, for Python programmers who want to improve their skills (advanced)
- B. Slatkin: "Effective Python: 59 Specific Ways to Write Better Python" ([Amazon](https://www.amazon.de/Effective-Python-Specific-Software-Development-ebook/dp/B00TKGY0GU/)) - learn to write efficient and "Pythonic" code (advanced)

### Videos/YouTube channels

- ["Python Tutorial for Beginners 1: Install and Setup for Mac and Windows" (Corey Schafer channel)](https://www.youtube.com/watch?v=YYXdXT2l-Gg&list=PL-osiE80TeTt2d9bfVyTiXJA-UTHn6WwU)
- ["Learn Python - Full Course for Beginners [Tutorial]" (freeCodeCamp.org channel)](https://www.youtube.com/watch?v=rfscVS0vtbw)
- ["Python Tutorial for Absolute Beginners #1 - What Are Variables?" (CS Dojo channel)](https://www.youtube.com/watch?v=Z1Yd7upQsXY)
- ["Introduction to Python 3 Programming Tutorial" (sentdex channel)](https://www.youtube.com/watch?v=eXBD2bB9-RA&list=PLQVvvaa0QuDeAams7fkdcwOGBpGdHpXln)
- ["Top Youtube channels to learn Python" (towardsdatascience.com)](https://towardsdatascience.com/top-13-youtube-channels-to-learn-python-524442aaab2f)

### Online platforms and other resources

- [Rosalind](http://rosalind.info/problems/locations/) - a platform for learning bioinformatics and programming through problem solving
- [edabit.com](https://edabit.com/challenges/python3) and other programming challenge websites
- [Reddit r/learnpython: useful links](https://www.reddit.com/r/learnpython/wiki/index)
- [freecodecamp.org: useful links](https://www.freecodecamp.org/news/best-python-tutorial/)
- [python-guide.org: useful links](https://docs.python-guide.org/intro/learning/)
- [codecademy.com](https://www.codecademy.com/learn/learn-python-3) and other interactive learning platforms
- [https://www.pythonforbiologists.org/](https://www.pythonforbiologists.org/) -
  videos and code for learning Python basics through genomics examples
  

### Staying updated

Connecting with other people from whom you can learn is both fun and helps staying updated. Here are some ideas:

- Reddit: r/Python, r/learnpython, r/bioinformatics, and see [here](https://analyticsindiamag.com/10-data-science-subreddits-every-tech-enthusiast-should-follow/)
- Twitter: see [here](https://www.youtube.com/watch?v=1hhuFrBNoLg) and [here](https://www.youtube.com/watch?v=3471Vg3GaPI) 
- Podcasts: see [here](https://dbader.org/blog/ultimate-list-of-python-podcasts)
- Blogs: see [here](https://blog.feedspot.com/python_blogs/)
- Forums: [Stackoverflow](https://stackoverflow.com/)

### After the course is before the course

So, you successfully completed your introductory Python courses. You learned the syntax and most keywords, you can write functions and classes, and you can use standard library and third-party modules. Congratulations, that's a great start, and hopefully the beginning of a beautiful friendship. To let the friendship carry on, it's a good idea to continue to educate yourself. This is what **every programmer** does - to gain practice, learn new skills, follow the quickly changing programming landscape, improve their chances on the market, and also because it's fun. It doesn't matter how exactly you do this: Books, tutorials, blogs, courses, YouTube channels (e.g. [YouTube](https://www.youtube.com/user/schafer5), [YouTube](https://www.youtube.com/c/rebelCoderBio/playlists), [realpython.com](https://realpython.com/python-youtube-channels/)), Python conference presentations (PyCon, PyData, etc., e.g. [YouTube](https://www.youtube.com/results?search_query=pycon+hettinger), [YouTube](https://www.youtube.com/watch?v=OSGv2VnC0go), [YouTube: Pandas](https://www.youtube.com/watch?v=5JnMutdy6Fw)), programming challenges ([reddit](https://www.reddit.com/r/learnpython/comments/av5c3o/so_where_can_i_find_python_coding_challenges_for/), [reddit](https://www.reddit.com/r/learnpython/comments/7330vy/is_there_a_website_that_gives_you_practice_python/), [medium.com](https://medium.com/coderbyte/the-best-coding-challenge-websites-in-2020-2e39f71cf488), [r/dailyprogrammer](https://www.reddit.com/r/dailyprogrammer/wiki/index); try e.g. [codewars.com](https://www.codewars.com/)) are all great options. If a book is difficult to understand and not fun to read, it may be poorly written or it may be too early for you to read it - then put it away and try again in 1-2 years. You can pay special attention at libraries that are popular in bioinformatics and data science ([reddit](https://www.reddit.com/r/learnpython/comments/gk517f/data_analysis_resources_for_python/), [medium.com](https://medium.com/javarevisited/6-best-python-books-for-data-science-and-machine-learning-in-2021-2f41d9fbf8be), [jakevdp.github.io](https://jakevdp.github.io/PythonDataScienceHandbook/), [YouTube](https://www.youtube.com/watch?v=ZyhVh-qRZPA&list=PL-osiE80TeTsWmV9i9c58mdDCSskIFdDS)), but don't limit yourself there. It's also worthwhile to connect with other people and hear their experiences ([stackexchange.com](https://softwareengineering.stackexchange.com/questions/44177/what-is-the-single-most-effective-thing-you-did-to-improve-your-programming-skil)). A good place for this is Reddit, where you can find links to many useful resources ([reddit](https://www.reddit.com/r/Python/comments/i0m2sy/i_know_python_basics_what_next/), [reddit](https://www.reddit.com/r/learnpython/comments/cf71a7/automate_the_boring_stuff_next_steps/), [learnbyexample.github.io](https://learnbyexample.github.io/python-intermediate/)), and learn about the projects of other people. One frequent recommendation is to start a small project yourself ([reddit](https://www.reddit.com/r/learnpython/comments/9i6ps9/what_took_your_python_skills_to_the_next_level/)), however it can be hard to pick one ([reddit](https://www.reddit.com/r/learnpython/comments/m42l42/so_i_want_to_learn_python_but_no_personal_project/)). So, it may be a good idea to read a book in the meantime, watch some YouTube videos and check out a programming challenge website, while following the subreddits and looking out for interesting projects to contribute, or for ideas to start with your own.
You can also look for internships in academic groups that are using Python for their work. It may be (still) hard for you to tackle a complex project by yourself, just be honest about this and talk with your supervisor. Maybe there are small tasks that you can do, or maybe you can participate in a collaborative project, and help e.g. with testing or writing documentation. You can also participate in open-source projects, maybe one that you discovered on Reddit, or something else. One exciting project worth checking out is the Biopython library, [biopython.org](https://biopython.org/wiki/Contributing).

