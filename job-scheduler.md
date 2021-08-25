If you execute many processes (jobs) from the command line, you may need
additional software to preserve your shell session or to submit/manage a
queue of jobs. You also need to monitor your processes for their resource usage
(CPU, memory, I/O). 

* TOC
{:toc}

## Basic terms

- **A program** is an executable file (that was compiled from code).
- **A process** is a running instance of a program with its own address
  space (place in memory). E.g., the
  [shell](https://en.wikipedia.org/wiki/Shell_(computing)) is a program, and you
  can have multiple running instances of the shell, therefore they are different
  processes. The kernel assigns every process a unique **PID** (process
  identifier) when the process is created. Every process has a **parent
  process**
  ([thegeekstuff.com](https://www.thegeekstuff.com/2013/07/linux-process-life-cycle/)).
  It's your responsibility to monitor the resource usage of a process, and to
  kill it if something goes wrong (e.g. if it takes too long or becomes
  unresponsive).
- **A job** is any process (or process group) you start in the shell. The
  job is not done until the processes complete, and a job can be stopped,
  resumed, or terminated ([linuxcommand.org](https://linuxcommand.org/lc3_lts0100.php)).
- A shell **session** is your current shell environment. Whenever you open a new
  shell (e.g. a new terminal tab), you start a new shell session.

Important tools and commands
([linux.com](https://www.linux.com/training-tutorials/how-kill-process-command-line/),
[YouTube](https://www.youtube.com/watch?v=TJzltwv7jJs)):

- `ps aux | grep <username>` or `ps aux | grep <process-name>` - list running
  processes and identify specific user/process
- `kill -9 <PID>` - kill process by PID ([linuxcommand.org](http://linuxcommand.org/lc3_lts0100.php))
- `killall <process-name>` - kill process by name
- `top` or `htop` - essential tool, process viewer and manager
  ([peteris.rocks](https://peteris.rocks/blog/htop/),
  [YouTube](https://www.youtube.com/watch?v=ZnEDfqr4Rm0))
    - for `htop`, you may want to adapt the meters to your liking ([superuser.com](https://superuser.com/a/806619/))

## Session management

One problem with remote logins (e.g. via SSH) is that when the connection is
gone, the current shell session is also gone. This is where tools like `screen`
or the more powerful `tmux` come in. They continue running in the background,
and you can re-attach to the session later, at any time, from any computer
(unless the server was restarted in the meantime, which terminates all
processes). This allows to retain the same session for a long time, which makes
it easier to run interactive jobs or view previous commands/output.

Tmux tutorials (pick one that you like):

- [hamvocke.com](https://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/)
- [danielmiessler.com](https://danielmiessler.com/study/tmux/)
- [leimao.github.io](https://leimao.github.io/blog/Tmux-Tutorial/)
- [howtogeek.com](https://www.howtogeek.com/671422/how-to-use-tmux-on-linux-and-why-its-better-than-screen/)

## Job scheduling

If you have many jobs that need to be executed in an automated fashion, an
interactive session won't do. Running jobs that can run without end user
interaction, or can be scheduled to run as resources permit, is called [batch
processing](https://en.wikipedia.org/wiki/Batch_processing). In batch processing
you are instructing a system to execute commands from a list or queue. This is
usually done by a [job scheduler](https://en.wikipedia.org/wiki/Job_scheduler).
There are many schedulers available, most of which are intended for
high-performance computing, and can distribute and manage jobs on a big cluster
of computers
([example](https://curc.readthedocs.io/en/latest/running-jobs/batch-jobs.html)).
The jobs announce their priority and their required resources like CPU and
memory, and the scheduler starts the job when it sees fit, and watches over its
execution. This allows an efficient sharing of computing resources between many
users. This complexity is usually not required on a single server. A simple job
queue can still be useful in some cases. For example, Task Spooler allows to
define jobs that depend on other jobs, so that these jobs won't run until
their dependencies are finished. In all cases you should be aware of the
processes you are currently running and of their resource usage (use `htop`).

[Task-Spooler](https://vicerveza.homeunix.net/~viric/soft/ts/):

- [douglasrizzo.com.br](https://douglasrizzo.com.br/ts-queue-experiments/)
- [librecv.org](https://librecv.org/t/deep-learning-experiments-with-task-spooler/463)

You may also consider using a [pipeline building
framework](https://www.biostars.org/p/91301/) ([Leipzig
2017](https://academic.oup.com/bib/article/18/3/530/2562749)).
This is
especially useful if you plan to set up a stable analysis pipeline over a large
number of samples. Examples are [Snakemake](https://github.com/snakemake/snakemake),
[Nextflow](https://github.com/nextflow-io/nextflow) or
[Bpipe](https://github.com/ssadedin/bpipe); for a collection of pipelines, see
[here](https://github.com/pditommaso/awesome-pipeline).

## Links

- [linux.com](https://www.linux.com/audience/devops/make-peace-your-processes-part-1/)
- Task Spooler alternatives:
    - nq - [GitHub](https://github.com/leahneukirchen/nq),
      [hacker-news](https://hacker-news.news/post/25920517)
    - Pueue - [GitHub](https://github.com/Nukesor/pueue)
- `crontab`, `at` - single-use jobs or regularly running jobs; not useful for batch
  processing, because jobs are not executed sequentially
  ([redhat.com](https://www.redhat.com/sysadmin/single-use-cron),
  [linoxide.com](https://linoxide.com/schedule-job-linux-commands/), [superuser.com](https://superuser.com/questions/220364/how-to-run-commands-as-in-a-queue/))