Welcome to Roy Lab
================
Last updated 4/24/2024

Here's some information to help you feel less lost. It is an overwhelming amount of information, but we don't expect anyone to go figure it all out and learn everything in weeks. It's to point you to resources so you can orient yourself, and then hopefully you can teach yourself how to fish. Have fun! We got your back.



-   [Checklist for mentor](#checklist-for-mentor)
-   [Teams](#teams)
-   [Linux basics](#linux-basics)
-   [Our servers](#our-servers)
-   [Server best practices](#server-best-practices)
-   [Directory structure](#directory-structure)
-   [Terminal management](#terminal-management)
-   [Command line editor](#command-line-editor)
-   [Programming languages](#programming-languages)
    -   [C++](#c)
    -   [Bash](#bash)
    -   [Python](#python)
    -   [R](#r)
    -   [Matlab](#matlab)
    -   [FAQ: why don't we implement things in Python or R?](#faq-why-dont-we-implement-things-in-python-or-r)
-   [Software](#software)
    -   [Programs directory](#programs-directory)
    -   [Git repositories](#git-repositories)
    -   [Module](#module)
    -   [Conda](#conda)
-   [Documenting our work](#documenting-our-work)
-   [Lab meetings](#lab-meetings)
-   [Sharing files](#sharing-files)
    -   [Google shared drive](#google-shared-drive)
    -   [Discovery pages](#discovery-pages)
    -   [Version control with git](#version-control-with-git)
-   [Github/git](#githubgit)
-   [Condor](#condor)
-   [Printing and IT support](#printing-and-it-support)
-   [Papers & readings](#papers-and-readings)
-   [Conferences/seminars](#conferencesseminars)
    -   [Recommended seminars at UW Madison](#recommended-seminars-at-uw-madison)
    -   [Venues to present at UW Madison](#venues-to-present-at-uw-madison)
    -   [National and international conferences](#national-and-international-conferences)
    -   [Conference travel funding](#conference-travel-funding)
-   [Lab space and food](#lab-space-and-food)
-   [CS classes](#cs-classes)

Checklist for mentor
--------------------

Please go through this list to make sure the new member is set up for access.

- [ ] WID login - Sushmita will request this for them.
- [ ] Roy group email listserv - Sushmita will add them.
- [ ] Teams - add them to Teams, appropriate channels.
- [ ] elog - ask Sara to create an action item for them.
    - They will need to be on WiscVPN or Discovery VPN to access elogs.
- [ ] Google shared drive - ask Erika or Sushmita to add them to the shared drive.
- [ ] git - add them to our git group so they can see our private repos.
- [ ] Zotero - add them to our group.
- [ ] Let them know when and where the lab meetings are.
- [ ] Create any relevant project folder for them on datavault.
- [ ] Discovery building/lab access

Teams
-----------

Most of our communications go through Microsoft Teams (it's like Slack). We will add your WiscID to our group so you can join. You can install a [Desktop app for Teams](https://kb.wisc.edu/office365/page.php?id=73588). 

One caveat: please **don't** post results on Teams; the search functionality isn't great and it will get lost in the messages. Refer to [Documenting our work](#documenting-our-work) section.

Linux basics
------------

All our servers are Linux servers. We do everything on them: running programs, writing programs, analyzing results, etc. You interact with the servers via command line by ssh'ing into them (see [Our servers](#servers)). If you are not familiar with the Linux command line, here are some resources so you can teach yourself. You only need to know the very basics to get started.

-   Tutorial: <https://linuxjourney.com/lesson/the-shell>
-   Cheat sheet: <https://rumorscity.com/wp-content/uploads/2014/08/10-Linux-Unix-Command-Cheat-Sheet-021.jpg>

At the beginning of every fall and spring semester, WACM (Women in Association for Computing Machinery), a student group over at CS, offers Linux workshops. Check the workshop date at the UW-Madison WACM website.

Our servers
-----------

We have lots of servers: they have different capacity for CPUs, memories, storage, and different amount allocated for [Condor](#condor) (a distributed computing platform supported by UW-Madison HT-Condor group). You ssh into them like this:

`ssh [wid_id]@[server_name].discovery.wisc.edu`

Your \[wid\_id\] and temp password is in the email that IT sent you (it is NOT your NetID). For example:

`ssh elee1@roy-submit.discovery.wisc.edu`

| Server     	|  RAM (GB)| \# of CPUs (logical cores)|  Scratch storage (TB)|  % dedicated to Condor|  # of GPUs | Mem/GPU (GB)   |  GPU spec 	|
|:--------------|---------:|--------------------------:|---------------------:|----------------------:|-----------:|---------------:|------------------:|
| roy-submit 	|       256| 40                        |                   1.9|                      0|	       	  0|		   0|		NA	|
| roy-exec-1 	|       768| 20                        |                   2.5|                     75|           0|		   0|		NA	|
| roy-exec-2 	|       768| 20                        |                   2.4|                     75|           0|	    	   0|		NA	|
| roy-exec-3 	|      1024| 112                       |                   2.0|                     75|           0|		   0|		NA	|
| roy-exec-4 	|      1024| 112                       |                   2.0|                     75|           0|		   0|		NA	|
| roy-exec-5	|      1024| 112                       |                   2.0|                     75|           0|		   0|		NA	|
| roy-exec-6 	|       512| 16                        |                   0.0|                     75|           0|		   0|		NA	|
| roy-exec-7 	|        64| 12                        |                   0.0|                     75|           0|		   0|		NA	|
| roy-exec-8 	|      1024| 144                       |                   1.3|                     75|           0|		   0|		NA	|
| roy-exec-9 	|       512| 112                       |		   1.8|			    50| 	  2|	          80| 		A100	|
| roy-exec-10	|      2048| 96			       |		   1.3|			    50| 	  0|		   0|		NA	|
| roy-exec-11	|      2048| 96			       | 	           1.3|			    50| 	  2|		  48| 		L40	|

Server best practices
---------------------

Tips for preventing server crashes:
	
DO NOT
- run a program that writes to standard out in a loop overnight unless you have done this already and have a sense of how much space it needs.
	
DO
- check `df -h .` for disk space usage in current directory.
- check `top -u <your username>` or `top -u <your username>` for memory availablity and CPU usage before and while running a high-memory or multi-core job or multiple jobs locally.
- check ganglia for computing resource avilablility
    - https://ganglia.discovery.wisc.edu/?c=Systems%20Biology&m=load_one&r=hour&s=by%20name&hc=4&mc=2
    - CPU: https://ganglia.discovery.wisc.edu/?r=hour&cs=&ce=&c=Systems+Biology&h=&tab=m&vn=&hide-hf=false&m=cpu_report&sh=1&z=small&hc=4&host_regex=&max_graphs=0&s=by+name
    - Memory: https://ganglia.discovery.wisc.edu/?r=hour&cs=&ce=&c=Systems+Biology&h=&tab=m&vn=&hide-hf=false&m=mem_report&sh=1&z=small&hc=4&host_regex=&max_graphs=0&s=by+name
- remove intermediate output files and tar up or gzip output files before generating more large output files.
- use smallest possible dataset for troubleshooting.
- parallelize tasks and distribute computing as much as possible, e.g., per-chromosome runs instead of genome-wide runs of HiCReg.
- communicate via Teams to coordinate intensive computing runs.
- to minimize the number of times you have to scp output files (especially images) back and forth between the server and your local machine, attach datavault to your Mac/Windows following the instructions [here](https://elog.discovery.wisc.edu/Software/202).
- before installing big complicated dependencies, check [module](#module) and ask about pre-existing conda environments.

Directory structure
-------------------

-   You have a personal home directory (`/mnt/ws/home/[wid_id]/`), but it has a storage cap and others can't access it so don't put any official work there.
-   Our lab's work is stored in WID's data vault, an overarching storage and file system for all of WID. `/mnt/dv/wid/projects2/`, `/mnt/dv/wid/projects3/`, `/mnt/dv/wid/projects5/` all have storage for our lab. Ask which project is relevant to you.
-   `/mnt/dv/wid/projects2/Roy-common/` has `data` and `programs` subdirectories, which contains tons of downloaded data and external/our own programs and scripts. If you're wondering if something's already out there, look around or ask instead of reinventing the wheel!
-   Whenever you create a new directory, put a README file with when you created it, who you are, and what the content of the folder is going to be. If you don't know how to create a file in command line, see [Command line editor](#vim).

Terminal Management
-------------------
Screen or Tmux is helpful in managing your terminal and navigating the command line. It allows you to create a new "window" or split your screen so you can monitor locally running jobs easily. Both tools are already installed in our servers; you can just pick one and go for it. 

- Tutorial for Screen: <https://linuxize.com/post/how-to-use-linux-screen/>
- Tutorial for Tmux: <https://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/>
  - to create a new session: `tmux new-session -s [session name]`
  - to detach or pause a session: ctrl + b + d
  - to reattach or get back into a session: `tmux a -t [session name]`
  - to get in read-only mode: `tmux a -rt [session name]`
  - to see list of sessions open: `tmux ls`
  - to kill a session: `tmux kill-session -t [session name]`
  - to kill everything: `tmux kill-server`

Command line editor
-------------------

Since we do all our work on the command line, we don't have a pretty/GUI-based IDE like Eclipse; we write the code in a command line Editor, and we compile and run on the command line. If you're not familiar with a command line editor, you can teach yourself how to use one of them. Either vim or emacs is fine, people just have different preferences. Just pick one and go for it.

-   Vim tutorial: <https://www.openvim.com/>

Programming languages
---------------------

Below are programming/scripting/numerical/statistical languages that we use and what we use them for. You might be like, I have to learn all this right now? You don't; you pick them up as you go, as you need. And don't reinvent the wheel - first ask if there's a script that already does something. And there may be terminology/tool (in **bold**) you may not have heard of below. Just look them up to get a sense of what they are so you can remember to pick it up when there's a suitable use case.

### C++

We implement our programs/algorithms in C++. If you know Java and C, the best way to pick up C++ might be by using the code in our [git repository](#git) as a blueprint and googling things as you go. If you want a grasp of the basics:

-   Tutorial: <http://www.cplusplus.com/doc/tutorial/>

C++ programs are compiled with **gcc/g++**.

-   Tutorial: sections 1.6-1.10, 2.1 in <https://www3.ntu.edu.sg/home/ehchua/programming/cpp/gcc_make.html>
-   Also ask for or look for existing make files and copy applicable parts.

You can debug C++ programs with **gdb**.

-   Tutorial: <https://www.youtube.com/watch?v=bWH-nL7v5F4>

### Bash

-   For preprocessing/postprocessing files: **awk** is a very fast scripting language that's particularly useful for processing column-wise data files.
-   For wrapping other scripts/programs: if you have a preprocessing step, actual program, and some post processing step, a.k.a. a pipeline, you can wrap it all into a bash script. Also look into **snakemake** if you're a sucker for clean processes.

### Python

-   For external programs: other researchers may have released their programs in Python. We install them in a [**conda**](#conda) environment. We recommed not to use **pip** because it puts things in a global path and makes conflicts. Don't mix conda and pip.
-   For preprocessing/postprocessing files: if **awk** (see [Bash](#bash) above) fails you, you can use Python as a simple scripting language.
-   For visualization: **seaborn** is a particular favorite for generating pretty charts. You can use a **Jupyter/iPython notebook** to run code and create visualizations on the fly.

### R

-   For external programs: other researchers may have released their programs in R. Install them in a conda environment; you might instaill them via bioconductor.
-   visualization: **ggplot** is a powerful framework in R to produce nice visuals. Whether you use Python or R to visualize, it's up to you. You can also use R in **Jupyter notebooks**.

### Matlab

-   For external programs: other researchers (especially those in CS or optimization field) may have released their programs in Matlab.
-   For proof-of-concept implementation: Matlab has fast linear algebra operations implemented. If you want to try out an algorithm, try doing it in Matlab before you laboriously implement it in C++.
-   For visualization: Matlab has a very straight forward visualization framework. You can of course use Matlab instead of Python or R to visualize.

### FAQ: why don't we implement things in Python or R?

Because they are slow. A lot of it has to do with the fact that they are not compiled languages. Some of it has to do with the fact that their libraries/modules/packages for doing numerical calculations/algebra is either slow, or we don't know exactly what the underlying implementation is doing (if you're writing your algorithms, abstraction can be a bad thing because it takes away control). Another thing is, it is very easy to write sloppy code that patches together a whole bunch of scripts rather than writing a production-grade program.

Software
--------

### Dependencies
Before installing big complicated dependencies or 3rd party programs, check [modules](#module) and ask if there is an existing conda environment you can use.

- ArchR is notoriously hard to install. In roy-exec-1 to roy-exec-9, it is available in module `R-4.3.1-Monocle3-ArchR`; in roy-exec-10, under module `conda3-py310_23.11.0-2`.
- For installing libtorch, follow the instructions [here](https://github.com/Roy-lab/libtorch_examples?tab=readme-ov-file#installing-libtorch-and-associated-libraries). 
- When making a [conda](#conda) environment, specify a path with the `conda create --prefix /path/to/env` and create it somewhere accessible to all lab members, i.e., not in your home directory. You can easily point to the environment path in your elogs this way.

### Programs directory

`/mnt/dv/wid/projects2/Roy-common/programs` contains tons of external and our own programs and scripts. If you're wondering if something's already out there, look around or ask instead of reinventing the wheel!

### Git repositories

See [below](#githubgit).

### Module

Discovery IT installs useful software on the computing cluster and makes it available through the Module system. Tools like Anaconda, Samtools, gcc, and Matlab can all be loaded up for immediate use without additional installation step.

-   To see which packages are currently available, use the command: `module avail`
-   To load a module, for example Matlab r2015a, use the command: `module load matlab-r2015a`
-   To view your loaded modules, use the command: `module list`
-   To unload a module if you would like to use a different version, for example unloading Matlab r2015a, use the command: `module unload matlab-r2015a`
-   To install additional R packages not available in a module, see <https://elog.discovery.wisc.edu/Software/232>. 
-   NOTE: ArchR is notoriously hard to install. In roy-exec-1 to roy-exec-9, it is available in module `R-4.3.1-Monocle3-ArchR`; in roy-exec-10, under module `conda3-py310_23.11.0-2`.

### Conda

As you read in [Python](#python), [R](#r), and [dependencies](#dependencies) above, we sometimes have to install external programs deployed in those languages. It gets complicated when different programs need different versions of Python/R and dependencies. Conda lets you create an isolated environment to install different packages.

-   First load the Anaconda module: see [Module](#module).
-   Follow the conda documentation to create and manage environments: <https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#>
-   Specify a path with the `conda create --prefix /path/to/env` and create the environment somewhere accessible to all lab members, i.e., not in your home directory. You can easily point to the environment path in your elogs this way.
-   If you want to completely change the location where conda environments and packages are installed by default, follow the steps:
    - Make a new .conda folder, e.g. in /mnt/dv/wid/project5/Roy-singlecell/<work_folder>/.conda
    - Do `conda config --prepend pkgs_dirs <path to .conda folder>/pkgs`
    - Do `conda config --prepend envs_dirs <path to .conda folder>/envs` 
- After this you can do the usual conda commands of creating and activating environments.

Documenting our work
--------------------

When you join our team, you should have your own Action Items list in elog.

-   NOTE: You can only access [elog.discovery.wisc.edu](https://elog.discovery.wisc.edu/) if you are on the UW/WID network or are VPN'd in (look up how to set up WiscVPN if you need to).
-   Put an elog under Action Items to document your to-do list and progress each weak.
-   Also put notes from meeting with Sushmita there.

As you work on a specific project, Sushmita or someone will let you know under which elog list you can document your experiments and results.

-   Each elog should have at least a goal/motivation, method, and results section.
-   Document any relevant directory locations (input files, outputfiles, program/code/scripts, etc.) needed to replicate the work.

Feel free to ask for an example elog!

Lab meetings
------------

-   There is a weekly lab meeting. Members rotate each week, presenting the problem they are working on.
-   If you're presenting next week, send your slides to Sushmita ahead of time (or print a copy for her).
-   The meetings are informal with lots of back-and-forth and you may not get through everything you prepared. That's okay!
-   [![Generic badge](https://img.shields.io/badge/COVID-Protocol-ff69b4.svg)](https://shields.io/) All our meetings are currently taking place online. The presenter will start a meeting in Teams > Roy Group > Group Meetings.
-   Slides are shared on [Google Shared Drive](#google-shared-drive) under Lab Meeting Slides folder.

Sharing files
-------------

### Google shared drive

We use Google shared drive to share slides, posters, documents, and other data amongst ourselves and with our collaborators. Note we use the UW-Madison G Suite, with our WiscID email login - the shared drive ensures that the data doesn't disappear when someone leaves the University. Some resources:

- If you join our lab, it might be worth installing File Stream so you can access the shared drive directories right from your desktop: https://kb.wisc.edu/28362
- Knowledge Base: https://kb.wisc.edu/47616

### Discovery pages

Everyone with a WID ID (different from your WiscID) gets a free webpage and space at pages.discovery.wisc.edu/~\[wid\_id\]. You can actually copy in image files into this space from any of our servers, and look at it on a browser ([example](http://pages.discovery.wisc.edu/~elee1/gould/)):

`scp [file] [wid_id]@pages.discovery.wisc.edu:~/public_html/[target]`

### Version control with git

We are attempting to use git for version control when writing manuscripts. We'll see how it goes. [More on git below](#githubgit).

Github/git
----------

We put our programs and code in git (<https://github.com/Roy-lab/>). Sometimes you have to download external programs from git. You only need to set up authentication and know the very basics to get started.

-   Tutorial/reference: <https://elog.discovery.wisc.edu/Software/106>

Condor
------

We sometimes have to run the same program 10,000 times, for different input files and/or with different parameters. Doing this on our servers 'locally' is not feasible. We use Condor to send off our jobs to open computing slots throughout WID servers and UW-Madison at large. You have to wrap your program in a specific Condor script so that Condor knows what resources you need, what input files to grab/send, which output files to fetch after program is run. Go through the tutorials below, **in order**. Again, don't reinvent the wheel; ask if there's a script you can use as a blueprint.

1.  Condor basics: <http://chtc.cs.wisc.edu/helloworld.shtml>
2.  Running with multiple permutations/parameter combinations: <http://chtc.cs.wisc.edu/multiple-jobs.shtml#foreach>
3.  \[If you need to\] Running R/Python/Matlab: <http://chtc.cs.wisc.edu/howto_overview.shtml>

-   Condor office hours: check the websites above.
-   We post questions/tips/notices about Condor in Teams &gt; Roy Group &gt; Condor.

Printing and IT support
-----------------------

-   Discovery building has its own IT support. It has a great knowlege base (KB) with articles on how to do things, including how to set up printing: <https://kb.wisc.edu/discovery/>
-   If you're having access/connection/elog/server issues, ask first in Teams if others are having the same issue. If we can't solve it we may have you contact the help desk (info in the knowledge base) and cc' Sushmita.
-   The IT office is in the basement so you can hop down to ask questions when there isn't a pandemic. The poster printers are there, too.

Papers and readings
-----------------

-   Sushmita shares papers of note through her Twitter account (@sroyyors).
-   Lab members (including Sushmita) will share interesting papers on Teams &gt; Roy Group &gt; Papers channel.
-   We collect papers in Zotero, which also generates bibliographies when we write papers.

Conferences/seminars
--------------------

We encourage attending and presenting at relevant seminars and conferences. We post events of interest in Teams &gt; Roy Group &gt; Seminars, Talks, and Conferences channel. We schedule practice talks for anyone who wants to get feedback.

[![Generic badge](https://img.shields.io/badge/COVID-Protocol-ff69b4.svg)](https://shields.io/) Many of the conferences have gone online this year, and we have had members present successfully online. Practice talks have also gone online via Teams.

### Recommended seminars at UW Madison

Google them for schedules/presenters; we might have the schedule already posted on the whiteboard (which you'll be able to see once we're back in our physical lab).

-   Biostat seminars
-   CS seminars
-   Stats seminars
-   GSTP seminars
-   CIBM seminars
-   Genomics seminars
-   Computational biology journal club
-   AIRG (journal club)

### Venues to present at UW Madison

Get practice creating a poster and talking about your research.

-   WID symposium (summer)
-   Epigenetics symposium (fall)
-   Undergrad research seminar (spring)

### National and international conferences

-   RECOMB (late spring)
-   GLBIO (late spring)
-   ISMB (summer)
-   ASHG (late October/early November)
-   RSG-DREAM (December)
-   NeurIPS MLCB (December)
-   Cold Spring Harbor meetings (throughout the year)

### Conference travel funding

-   UW Madison grad school conference award: applications accepted year-around, look up the logistical details.
-   ISMB will offer travel fellowships - make sure you apply if your abstract is accepted.
-   Cold Spring Harbor always has a note telling students to contact a point person for financial aid questions.
-   ACM's Women in Computing also offers year-around scholarships for attending research computer science conferences.

Lab space and food
--------------

Only those with pre-approved access can get into the research floors of the Discovery building. 

-   Our lab is unlocked from 9am to 5pm.
-   The whiteboard in our lab has some useful information posted: our servers, upcoming seminar series, upcoming conferences.
-   You can grab the food on the shelves/cabinets in our side of the lab.
-   You can of course use the kitchen. Just leave it clean!

Classes
----------

If you do not come from a CS background, here's a sequence of classes we recommend (in order, taking into account pre-requisites).

1.  CS 200, CS 300 (Programming I and II)
2.  CS 540 (Intro to AI) and CS/BMI 576 (Intro to Bioinformatics)
3.  CS 760 (Machine learning) and CS/BMI 776 (Advanced Bioinformatics)

Additionally, these classes cover materials very relevant to our work, but may not be offered every semester:

-   BMI 826-023/CS 838 Network Biology
-   CS/STAT/ECE/ME 532 Matrix Methods in Machine Learning
-   STAT 451 Introduction to Machine Learning and Statistical Pattern Classification
-   Introduction to Deep Learning From Sebastian Raschka

If you're coming from the computational side and want to dig deeper into biology, you may want to check out GENETICS 466 (Principles of Genetics). It does have some basic biology and chemistry pre-requisites. There are also seminars you can take for credit, spread throughout many different biology-related departments. Ask our lab members if you're curious about a class and how relevant you think it would be for our work.
