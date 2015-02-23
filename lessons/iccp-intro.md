[![](https://bytebucket.org/davis68/resources/raw/f7c98d2b95e961fae257707e22a58fa1a2c36bec/logos/baseline_cse_wdmk.png?token=be4cc41d4b2afe594f5b1570a3c5aad96a65f0d6)](http://cse.illinois.edu/)

# Introduction to Illinois CampusCluster
### Computational Science and Engineering Training • Spring 2015

<a id='contents'></a>
## Contents
- [What is Campus Cluster?](#whatis)
- [Running Code](#running)
- [A Friendlier Campus Cluster](#friend)
    - [Motivation 2](#motiv2)
- [Credits](#credits)


---
<a id='whatis'></a>
## What is Campus Cluster?
-   Campus Cluster background
-   Shells & architecture (graphic)


---
<a id='env'></a>
## Environment
-   Logging in and first look
    -   `ssh`, `pwd`, `ls`, `ls /`, `exit`
-   Navigating the environment (`ssh`, module, file system)
    -   Accessing Campus Cluster (`ssh`; PuTTY for Windows)
        -   `ssh`
        -   `scp` to/from `$USER@taub:~/hpc-sp14/data/aeotab_9.xlsx`
        -   `wget http://www.eia.gov/forecasts/aeo/er/excel/aeotab_10.xlsx`
    -   `who`/`whoami`
    -   `nano`/`vi`/`emacs`
    -   `module` (`ldd bin/nwchem ; module load intel mvapich2 ; ldd bin/nwchem`)
        -   What are the advantages of `module`?  (tab completion,
            namespace clutter, versions)
-   Filesystem
    -   `/`, `/home` (2GB), `/projects` (more), `/scratch` (running),
        `/gpfs/gpfs_data01/.snapshots/*/{home, projects}`
    -   `ln -s /scratch/users/$USER ./scratch`
    -   `ln -s /projects/cse/shared/$USER`
    -   Exercise:  `ln -s /gpfs/gpfs_data01/.snapshots ./backup`


---
<a id='running'></a>
## Running Code

We will use example codes obtained as follows to illustrate compiling, queueing, and running code on Campus Cluster.

    wget https://github.com/uiuc-cse/hpc-sp15/raw/gh-pages/lessons/hpc-code-examples.tar.gz
    tar -xvzf hpc-code-examples
    module load gcc

-   Queueing
    -   Campus Cluster operations model:  all buy nodes, have guaranteed
        access, but available otherwise
    -   Moab/Torque
        -   `qsub`, `qstat`, `qdel`, `qhold`, `qrls`, `qpeek`, `showq`,
            `showstart`
        -   Fairshare queuing divides requested resources among system users
            or groups (rather than just between processes).  It incorporates
            the historic behavior of a user and group into job priority
            decisionmaking.  In principle, this allows groups and users to
            fairly access the resource.  However, this can be frustrating
            for a new user to understand, particularly when one has a number
            of jobs in the queue and it takes a long time for them to run.
-   `mpiexec`
-   Compiling
    -   If you're writing scientific code, you're almost definitely using 
        C/C++, Fortran, or Python, so it behooves us to check and see what
        the options for those are.
        -   C/C++:  `icc`/`icpc` and `gcc`/`g++`
            (my only real complaint is that `gcc` is out-of-date---
            4.7.1 is June 2012 and doesn't support some C++11 and OpenMP 4.0 
            features)
        -   Fortran:  `ifort` and `gfortran` (not `g95`)
        -   Python:  2.7.8, 3.4.1 are both available, plus legacy versions
        -   The latest versions are always preferred for compiling new 
            programs.
-   Installing
    -   As you do not have administrator privileges on Campus Cluster, you
        won't be able to `make install` your software.  You have two 
        options:
        -   Set up a "local" installation for yourself:  create and add to
            your `$PATH` appropriate directories like `~/bin`.
        -   Create a group-wide installation if you are part of a research
            group and can maintain the software.  [guide](https://campuscluster.illinois.edu/user_info/doc/software_guidelines.html)
    -   Subsequent to a successful installation, you can create a `modulefile` which works with `module` to update the environment for other users of your software application.


---
<a id='friend'></a>
## A Friendlier Campus Cluster
-   `.bash_profile` (`ls color`), `alias` (but not to `cc`), `ssh-keygen`
-   Running jobs in `~/scratch`:
    `cd ~/scratch ; mkdir $PBS_JOBID ; cd $PBS_JOBID`
-   Preventative maintenance (PM) is scheduled for the third Wednesday of
    each month—long jobs submitted just prior to this time cannot run until
    afterwards.
-   Installing your own software
    -   Local paths for `~/bin`, `~/.local`, etc.
-   Campus Cluster user resources:
    -   Campus Cluster User Forum
    -   Campus Cluster Walk-In Help
-   [Summary Handout](https://github.com/uiuc-cse/hpc-sp15/raw/gh-pages/lessons/hpc-handout.pdf)


---
<a id='credits'></a>
## Credits

Neal Davis developed these materials for [Computational Science and Engineering](http://cse.illinois.edu/) at the University of Illinois at Urbana–Champaign.  Some tips were suggested by Jay Alameda and Mark van Moers of NCSA.  In addition, the support of NCSA and Campus Cluster personnel such as Wayne Hoyenga, Martin Biernat, and Kandace Turner-Jones, has also been invaluable.

<img src="http://i.creativecommons.org/l/by/4.0/88x31.png" align="left">
This content is available under a [Creative Commons Attribution 4.0 Unported License](https://creativecommons.org/licenses/by/4.0/).

[![](https://bytebucket.org/davis68/resources/raw/f7c98d2b95e961fae257707e22a58fa1a2c36bec/logos/baseline_cse_wdmk.png?token=be4cc41d4b2afe594f5b1570a3c5aad96a65f0d6)](http://cse.illinois.edu/)