<img src="https://tulln.fhwn.ac.at/assets/svg/fhwn-logo-tulln.svg">
<p style="color:darkgray;">FHWN, Biotech Campus Tulln</p>

<H1>General information, resources and recommendations</H1>

- TOC
{:toc}

## Quickstart: Python

If you want to know what programming is and if it's right for you, watch an introductory tutorial like "Python Project Tutorial - Your First Python Project" by freeCodeCamp.org, 2020 ([YouTube](https://www.youtube.com/watch?v=_ZqAVck-WeM)) or ask one of the frontier LLMs ("Give me simple examples of programming in Python"). For more info, read on.

## Biological background

A solid biological background is indispensible for all courses of the curriculum. This general textbook provides a comprehensive overview and can be used for studying and as a reference:

- Urry et al.: "Campbell Biology" ([pearson.com](https://www.pearson.com/en-us/subject-catalog/p/campbells-biology/P200000014184/9780135455890), [pearson.de](https://www.pearson.de/campbell))

## Laptop specifications

A portable laptop is required for a number of courses. Data-intensive computations and heavy simulations are meant to run on dedicated FH hardware rather than on your laptop, so your laptop primarily needs to handle code editing, web research, multitasking, and remote connections. Minimum specifications:

- CPU: Intel Core i5 / AMD Ryzen 5 or higher
  - Apple Silicon Macs (M-series chips) are also excellent
  - Avoid slow low-end processors; if you are unsure whether a specific chip qualifies, look it up on a processor benchmark site like [notebookcheck.com](https://www.notebookcheck.com/Mobile-Prozessoren-Benchmarkliste.1809.0.html) or [cpubenchmark.net](https://www.cpubenchmark.net/)
- Memory: ≥16 GB RAM recommended; this ensures smooth performance when running a Linux environment, an IDE (like VS Code or RStudio), a web browser with dozens of research tabs, and connection software simultaneously. 8 GB can work if you use WSL, which shares memory with Windows dynamically rather than reserving a fixed amount, but you will feel the difference.
- Storage: ≥200 GB of free disk space (SSD) at the start of the curriculum; most current laptops ship with at least 512 GB SSDs
- GPU: not required for any course; if you want headroom for local AI model experimentation on your own time, consider a MacBook (Apple Silicon's unified memory works well for this) or a discrete NVIDIA GPU with ≥8 GB VRAM (but a dGPU adds weight, cost, and reduces battery life)
- Display & portability: ≥13 inches; a lightweight ultrabook is recommended
- Operating system: Windows 11, macOS, or Linux
- Tip: Prioritize well-established business lines (e.g., Lenovo ThinkPad, Dell Latitude, Apple MacBook) over cheap consumer special offers; you can check independent reviews on [notebookcheck.net](https://www.notebookcheck.net/Laptop-Buying-Guide-Tool.13212.0.html), e.g. [budget office laptops](https://www.notebookcheck.net/Notebookcheck-s-Top-10-Budget-Office-Business-Notebooks.98853.0.html)

Note: benchmarks describe a laptop's optimal performance. Real-world responsiveness can diverge significantly due to a bloated system, malware, aggressive antivirus, slow SSDs, or poor thermal design. A useful informal check: after a normal startup, opening common applications and switching between them should feel immediate, not laggy. If your existing laptop already feels slow in daily use, that is reason enough to reinstall the OS or replace the laptop, even if the specifications look acceptable on paper.

## Linux environment

**Note:** Please make a full backup of your computer before making any modifications.

Some courses of the curriculum require a Linux operating system. You do not need to give up Windows or macOS for this: Linux runs alongside your usual system, either tightly integrated with it (WSL on Windows) or as a **virtual machine**. Virtual machines (VMs) allow you to run an operating system (OS) in an app window on your desktop that behaves like a full, separate computer. This virtual computer, the "guest", has its own emulated CPU, memory, network interface and storage, and you can install an OS on it just as you would on a real, physical machine. [This short video](https://www.youtube.com/watch?v=yIVXjl4SwVo) explains the basic terms. The [advantages](https://www.makeuseof.com/tag/reasons-start-using-virtual-machine/) are that you can try different OSes, run software your main OS can't, and try out apps in a safe, isolated environment. It's a great way to learn and experiment with an OS like Linux, because you can install it on Windows or macOS and run it like any other software. VMs are saved as folders with some files on your hard drive and can be copied, backed up and removed like any other folders. You can play with a VM and modify it as you like, and if it's broken beyond repair, you can quickly restore it from an earlier backup. Many people use VMs for their work on a regular basis. (By the way, do you know what an OS does? [This nice video](https://www.youtube.com/watch?v=26QPDBe-NB8&) approaches its basic functionality from a historical perspective.)

WSL works differently: instead of a window containing a desktop, you get a Linux terminal integrated into Windows, running on a lightweight VM that Windows manages for you. It is faster to set up and lighter on resources, at the cost of not having a Linux desktop.

Linux comes in different flavors (called [distributions](https://www.howtogeek.com/132624/htg-explains-whats-a-linux-distro-and-how-are-they-different/)), with Ubuntu being the most popular one; that's what we use. Which route is right for you depends on your computer.

### Which option should I use?

- **Windows: use WSL** ([detailed instructions](install_linux_in_wsl.md)). Windows 10 and 11 include the built-in [Windows Subsystem for Linux](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux) (also see [ubuntu.com](https://ubuntu.com/desktop/wsl)), which runs a real Ubuntu system — the same `apt`, the same `sudo`, the same Bash — in a lightweight VM managed by Windows itself. It installs with a single command, needs no ISO and no guest additions, shares memory and disk with Windows dynamically instead of reserving them up front, and integrates with Visual Studio Code so that you edit in a familiar Windows window while all code runs in Linux. What it does not give you is a Linux *desktop*, you only get a terminal – this is fine, as it matches how you will work on the FH compute servers.
- **macOS with Apple silicon: use UTM or VMware Fusion** ([detailed instructions](install_linux_on_apple_silicon.md)). WSL is Windows-only, so on a Mac you run a real VM.
- **VirtualBox** ([detailed instructions](install_linux_in_virtualbox.md)) is still a good choice if you want a full Linux desktop. One important [caveat](https://forums.virtualbox.org/viewtopic.php?t=112113) is that Windows 11 enables its own hypervisor, Hyper-V, by default for security features; if you have installed WSL it is enabled in any case. VirtualBox must then run on top of it and falls back to a [slower mode](https://learn.microsoft.com/en-us/troubleshoot/windows-client/application-management/virtualization-apps-not-work-with-hyper-v). Hyper-V can be switched off, but doing so disables some [security features](https://learn.microsoft.com/en-us/windows/security/hardware-security/enable-virtualization-based-protection-of-code-integrity), and is not generally recommended.

### Notes on the VirtualBox route

If you go the VirtualBox way, I suggest the latest [Xubuntu](https://xubuntu.org/download/) LTS, which is Ubuntu with the lightweight and responsive desktop environment Xfce instead of GNOME, therefore **X**ubuntu. [This video](https://www.youtube.com/watch?v=sB_5fqiysi4) walks you through the installation of Ubuntu in VirtualBox; the process is equivalent for Xubuntu. You might run into some problems, e.g. the option `Ubuntu (64 bit)` might not be available, because you need to activate VT-x/AMD-v in the host BIOS/UEFI first, as explained e.g. [here](https://superuser.com/questions/1241956/virtualbox-only-allowing-32-bit-os). Also, after installing and booting the guest OS, you will need to install the "guest additions", a set of VirtualBox-related drivers and software, for a fully functional VM. [Click here for detailed instructions.](install_linux_in_virtualbox.md)

## Linux and Bash

[Linux](https://en.wikipedia.org/wiki/Linux) is a free OS, which is stable yet highly customizable, actively developed, and offers a huge selection of free software development tools. A lot of scientific software is written only for Linux - e.g. almost all short read aligners, assemblers, and many more. Some advantages are:

- Linux is completely free and open-source and widely used
- Linux is very safe, malware is rare
- Software can be installed in an automated way using a package manager (similar to an app store)
- Software can be installed by the user without administrator privileges and easily configured in different ways (this is much harder in Windows)

Linux includes [the shell](http://linuxcommand.org/lc3_lts0010.php), a command-line interpreter/scripting language that can execute built-in shell commands, Linux utilities and programs. It is a powerful and versatile tool and very useful e.g. for working with text files, which is common in biological data analysis. The shell allows to easily build pipelines using different commands and utilities, e.g. for sorting/cutting/restructuring text files and feeding the result into other commands/utilities/programs. It is one of the most important tools in bio data science, and you should get comfortable with it early on.

Several shell programs exist. The [Bash shell](http://linuxcommand.org/lc3_lts0010.php) is the most popular shell and the default on most or all Linux distributions. A [terminal emulator](https://dev.to/nestedsoftware/comment/4a33) is a program that opens a window and lets you interact with the Bash shell. Different Ubuntu flavors use different terminal emulators as default, e.g. Xubuntu has the [Xfce terminal](https://docs.xfce.org/apps/terminal/start).

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

Together with R and Bash, Python is an essential part of the modern bioinformatics and data science toolkit. While Bash is an integral part of Linux and is therefore [inevitable](https://www.reddit.com/r/bioinformatics/comments/e5qj7b/whats_the_advantage_of_bash_on_bioinformatics/), and R is useful for statistical modeling and visualization, Python is a general-purpose language that is applied in a wide range of applications, including data science, machine learning, software and web development, automation, "and generally getting stuff done" ([YouTube](https://www.youtube.com/watch?v=zyh2HU1efo4), [reddit](https://www.reddit.com/r/bioinformatics/comments/lez284/the_real_question_r_vs_python/)).

It's not very important which resource for learning Python you pick, as most of them present similar contents in different ways. However, it's important that the way in which the information is presented makes sense to you, so that you can enjoy the learning experience and are motivated to continue. Pick a resource that works well for you and stick to it if possible. You can also talk to your fellow students and exchange experiences and recommendations.

### Development environment

A development environment comprises programs and tools that you use for writing, testing and debugging code. You could use a simple text editor, but [integrated development environments (IDEs)](https://www.codecademy.com/articles/what-is-an-ide) provide many features that will make your life easier and your code better. 

**Online IDEs.** One great way to learn Python is to simply run it online. There are many good resources, e.g.

- [Google Colab](https://colab.research.google.com) — Jupyter notebooks in the cloud (via Google Drive), very popular
- [Try Jupyter / JupyterLite](https://jupyter.org/try-jupyter/lab/) — a full JupyterLab in the browser, with no account and no server; NumPy, pandas and matplotlib are included, and files live only in browser storage
- [PythonAnywhere](https://www.pythonanywhere.com/) — a Linux console with Python in the browser; the free tier is quite limited
- [GitHub Codespaces](https://github.com/features/codespaces) — a real Linux container with VS Code in the browser, with a monthly free allowance for personal accounts
- [molab](https://molab.marimo.io/) — free cloud notebooks in the [marimo](https://marimo.io/) format; the [gallery](https://molab.marimo.io/notebooks) shows examples
- Without an account: [onlinegdb.com](https://www.onlinegdb.com/online_python_compiler) (also does Bash)
- [Python Tutor](https://pythontutor.com/) — steps through your code and visualizes variables, references and the call stack

**Local IDEs.** To install and run Python locally, we use [Miniforge](https://github.com/conda-forge/miniforge), a minimal installer for the **conda** package and environment manager, preconfigured for the [conda-forge](https://conda-forge.org/) channel. You install it in your Linux environment (see the setup tutorials above), and then create an environment containing Python plus whichever libraries and tools you need.

Note: you may encounter the larger [Anaconda](https://stackoverflow.com/a/42096429) distribution in other tutorials, which bundles conda with many preinstalled packages and the [Anaconda Navigator](https://docs.anaconda.com/anaconda/navigator/). However, its terms of service have changed several times, requiring a paid license in some cases. Beyond that confusion, there is little reason to use it: anything Anaconda preinstalls can be added to a conda environment on demand and building minimal per-project environments is better practice anyway. The licensing limitations don't affect conda itself or the conda-forge channel – only Anaconda's distribution and its own package repository (the "defaults" channel), which Miniforge does not use.

All three IDEs listed below are popular for Python code development, and have somewhat different strengths and focus:

- [Jupyter](https://en.wikipedia.org/wiki/Project_Jupyter): Great for presenting, storytelling and exploratory data analysis; not necessarily the best for learning to code or longer scripts. [Introductory video](https://www.youtube.com/watch?v=HW29067qVWk)
- [VS Code](https://en.wikipedia.org/wiki/Visual_Studio_Code): Popular code editor with many plugins, but not necessarily the best for complete beginners; if you want to try it, start [here](https://www.digitalocean.com/community/tutorials/getting-started-with-python-in-visual-studio-code) and continue [here](https://realpython.com/python-development-visual-studio-code/), [here](https://code.visualstudio.com/docs/python/python-tutorial) or [here](https://code.visualstudio.com/docs/getstarted/introvideos)
- [Spyder](https://www.spyder-ide.org/): Very learning-friendly IDE. A good place to start is the Spyder tutorial, `Help` → `Spyder tutorial`; also check out [this introductory video](https://www.youtube.com/watch?v=zYNRqVimU3Q)

### Books/tutorials

- [w3schools.com Python tutorial](https://www.w3schools.com/python/) – useful as a reference, with interactive examples
- ["A Byte of Python"](https://python.swaroopch.com/) – free beginner-friendly ebook; doesn't go too deep, but covers the basics
- [programming-26.mooc.fi](https://programming-26.mooc.fi/part-1) – free online course/tutorial, ranges from basic to complex topics
- ["Python for Everybody"](https://www.py4e.com/html3/) and [interactive edition](https://books.trinket.io/pfe/index.html), also see [here](https://runestone.academy/runestone/books/published/py4e-int/index.html) – free beginner-friendly ebook
- E. Freeman: "Head First Learn to Code: A Brain-Friendly Guide" ([Amazon](https://www.amazon.de/Head-First-Learn-Code-Brain-Friendly/dp/1491958863/)); P. Barry: "Head First Python" ([oreilly.com](https://www.oreilly.com/library/view/head-first-python/9781491919521/)) – very beginner-friendly, if you like the approach of the book series
- ["Think Python: How to Think Like a Computer Scientist"](https://greenteapress.com/wp/think-python-3rd-edition/) – free and very nice ebook; you'll learn a lot if you work your way through it
- E. Matthes: "Python Crash Course: A Hands-On, Project-Based Introduction to Programming", 3rd edition ([nostarch.com](https://nostarch.com/python-crash-course-3rd-edition)) – practical introduction for complete beginners, with exercises
  - The author provides a collection of online resources, including some nice [cheat sheets](https://ehmatthes.github.io/pcc_3e/cheat_sheets/)
- A. Sweigart: "Automate the Boring Stuff with Python: Practical Programming for Total Beginners" ([Amazon](https://www.amazon.de/Al-Sweigart/dp/1593279922/), [online book](https://automatetheboringstuff.com)) – practically oriented introduction for Python (ranges from beginners to somewhat advanced content); more excellent free Python books from this author can be found at [inventwithpython.com](https://inventwithpython.com/)
- D. Amos et al.: "Python Basics: A Practical Introduction to Python 3", 4th edition ([Amazon](https://www.amazon.com/Python-Basics-Practical-Introduction/dp/1775093328/))
- [Official Python tutorial](https://docs.python.org/3/tutorial/) – good reference for topics you already know, to refresh your memory or to go deeper

Hints: Practically oriented tutorials that solve little problems rather than just presenting information, are usually more fun and provide a better understanding of the material. When writing code based on some code template, do not copy-paste it, but re-type it yourself. This improves the learning result. 

**Advanced.**

- L. Ramalho: "Fluent Python: Clear, Concise, and Effective Programming", ([fluentpython.com](https://www.fluentpython.com/)) – discussion of Python-specific language features, for Python programmers who want to improve their skills (advanced)
- B. Slatkin: "Effective Python: 125 Specific Ways to Write Better Python", 3rd edition ([effectivepython.com](https://effectivepython.com/)) – learn to write efficient and "Pythonic" code (advanced)

### Videos/YouTube channels

- ["Python Tutorial for Beginners 1: Install and Setup for Mac and Windows" (Corey Schafer channel)](https://www.youtube.com/watch?v=YYXdXT2l-Gg&list=PL-osiE80TeTt2d9bfVyTiXJA-UTHn6WwU)
- ["Learn Python - Full Course for Beginners [Tutorial]" (freeCodeCamp.org channel)](https://www.youtube.com/watch?v=rfscVS0vtbw)
- ["Python Tutorial for Absolute Beginners #1 - What Are Variables?" (CS Dojo channel)](https://www.youtube.com/watch?v=Z1Yd7upQsXY)
- ["Introduction to Python 3 Programming Tutorial" (sentdex channel)](https://www.youtube.com/watch?v=eXBD2bB9-RA&list=PLQVvvaa0QuDeAams7fkdcwOGBpGdHpXln)
- ["Data Professor" channel](https://www.youtube.com/c/DataProfessor/videos)
- Reddit discussions, e.g. "What is your favorite Python-related YouTube channel?" ([reddit](https://www.reddit.com/r/learnpython/comments/1cyeyp8/what_is_your_favorite_pythonrelated_youtube/)) and "What is the best video series to learn python on youtube?" ([reddit](https://www.reddit.com/r/learnpython/comments/18vnu9i/what_is_the_best_video_series_to_learn_python_on/))

### Online platforms and other resources

- [Rosalind](http://rosalind.info/problems/locations/) – a platform for learning bioinformatics and programming through problem solving
- [codewars.com](https://www.codewars.com/), [exercism.org](https://exercism.org/tracks/python), [checkio.org](https://py.checkio.org/), [practicepython.org](https://www.practicepython.org/), or other programming challenge websites
- [Reddit r/learnpython: useful links](https://www.reddit.com/r/learnpython/wiki/index), [r/learnpython: more links](https://www.reddit.com/r/learnpython/comments/tvkfih/is_codeacademy_free_worth_it_to_learn_basic_python/)
- [freecodecamp.org: useful links](https://www.freecodecamp.org/news/best-python-tutorial/)
- [python-guide.org: useful links](https://docs.python-guide.org/intro/learning/)
- [software-carpentry.org](https://software-carpentry.org/lessons/index.html) – a collection of tutorials for research computing
- [pythonforbiologists.org](https://www.pythonforbiologists.org/) – videos and code for learning Python basics through genomics examples
- Apps like [Sololearn](https://play.google.com/store/apps/details?id=com.sololearn&gl=at) or others

### Staying updated

Connecting with other people from whom you can learn is both fun and helps staying updated. Here are some ideas:

- Reddit: r/Python, r/learnpython, r/bioinformatics, and see [here](https://analyticsindiamag.com/10-data-science-subreddits-every-tech-enthusiast-should-follow/)
- X (formerly Twitter): still one of the fastest sources for tech and especially AI news, where a lot breaks first. Curated accounts do the filtering for you, e.g. [@kimmonismus](https://x.com/kimmonismus) for AI. Be aware that the signal-to-noise ratio depends entirely on whom you follow.
- [Bluesky](https://bsky.app/): where much of the academic and bioinformatics community moved after 2023; better for research discussion and for following individual scientists than for breaking news.
- Podcasts: see [here](https://dbader.org/blog/ultimate-list-of-python-podcasts)
- Blogs: see [here](https://blog.feedspot.com/python_blogs/)
- Forums: [Stackoverflow](https://stackoverflow.com/) and other [Stackexchange](https://stackexchange.com/sites#) forums

### After the course is before the course

So, you successfully completed your introductory Python courses. You learned the syntax and most keywords, you can write functions and classes, and you can use standard library and third-party modules. (You can always look at one of the many introductory tutorials as a refresher, just install the [returnyoutubedislike](https://www.returnyoutubedislike.com/) addon to help you choose one.) Congratulations, that's a great start, and hopefully the beginning of a beautiful friendship. To let the friendship carry on, it's a good idea to continue to educate yourself. This is what **every programmer** does - to gain practice, learn new skills, follow the quickly changing programming landscape, improve their chances on the market, and also because it's fun. It doesn't matter how exactly you do this: Books, tutorials, blogs, courses, YouTube channels (e.g. [YouTube](https://www.youtube.com/user/schafer5), [YouTube](https://www.youtube.com/c/rebelCoderBio/playlists), [realpython.com](https://realpython.com/python-youtube-channels/)), Python conference presentations (PyCon, PyData, etc., e.g. [YouTube](https://www.youtube.com/results?search_query=pycon+hettinger), [YouTube](https://www.youtube.com/watch?v=OSGv2VnC0go), [YouTube: Pandas](https://www.youtube.com/watch?v=5JnMutdy6Fw)), programming challenges ([reddit](https://www.reddit.com/r/learnpython/comments/av5c3o/so_where_can_i_find_python_coding_challenges_for/), [reddit](https://www.reddit.com/r/learnpython/comments/7330vy/is_there_a_website_that_gives_you_practice_python/), [medium.com](https://medium.com/coderbyte/the-best-coding-challenge-websites-in-2020-2e39f71cf488), [r/dailyprogrammer](https://www.reddit.com/r/dailyprogrammer/wiki/index); try e.g. [codewars.com](https://www.codewars.com/)) are all great options. If a book is difficult to understand and not fun to read, it may be poorly written or it may be too early for you to read it - then put it away and try again in 1-2 years. You can pay special attention at libraries that are popular in bioinformatics and data science ([reddit](https://www.reddit.com/r/learnpython/comments/gk517f/data_analysis_resources_for_python/), [medium.com](https://medium.com/javarevisited/6-best-python-books-for-data-science-and-machine-learning-in-2021-2f41d9fbf8be), [jakevdp.github.io](https://jakevdp.github.io/PythonDataScienceHandbook/), [YouTube](https://www.youtube.com/watch?v=ZyhVh-qRZPA&list=PL-osiE80TeTsWmV9i9c58mdDCSskIFdDS)), but don't limit yourself there. It's also worthwhile to connect with other people and hear their experiences ([stackexchange.com](https://softwareengineering.stackexchange.com/questions/44177/what-is-the-single-most-effective-thing-you-did-to-improve-your-programming-skil)). A good place for this is Reddit, where you can find links to many useful resources ([reddit](https://www.reddit.com/r/Python/comments/i0m2sy/i_know_python_basics_what_next/), [reddit](https://www.reddit.com/r/learnpython/comments/cf71a7/automate_the_boring_stuff_next_steps/), [learnbyexample.github.io](https://learnbyexample.github.io/python-intermediate/)), and learn about the projects of other people. One frequent recommendation is to start a small project yourself ([reddit](https://www.reddit.com/r/learnpython/comments/9i6ps9/what_took_your_python_skills_to_the_next_level/), [inventwithpython.com](https://inventwithpython.com/bigbookpython/)), however it can be hard to pick one ([reddit](https://www.reddit.com/r/learnpython/comments/m42l42/so_i_want_to_learn_python_but_no_personal_project/)). So, it may be a good idea to read a book in the meantime, watch some YouTube videos and check out a programming challenge website, while following the subreddits and looking out for interesting projects to contribute, or for ideas to start with your own.
You can also look for internships in academic groups that are using Python for their work. It may be (still) hard for you to tackle a complex project by yourself, just be honest about this and talk with your supervisor. Maybe there are small tasks that you can do, or maybe you can participate in a collaborative project, and help e.g. with testing or writing documentation. You can also participate in open-source projects, maybe one that you discovered on Reddit, or something else. One exciting project worth checking out is the Biopython library, [biopython.org](https://biopython.org/wiki/Contributing).

