---
title: Commands and Routine of Simulation on Graham, a Compute Canada Cluster
toc: true
date: 2019-01-30 05:41:19
tags: [Research Daily, HPC, CAML]
categories: Research Daily
---
Again, I am using the cluster [GRAHAM](https://docs.computecanada.ca/wiki/Graham) for the simulation and here is the routine I normally use in the cluster end for my project.
<!--more-->

### Login and Version Control
- For convenience, I make an alias of the ssh connection called `graham`. Details could be check in the [previous blog](https://swang251.github.io/2018/10/04/Passwordless-SSH-connection-to-a-Cluster/).
- I am using [Git](https://git-scm.com/) and [Bitbucket](https://bitbucket.org/) for version control.

### Compilation
- For the LBM simulation, I got my projects stored in the folder *lbm* and the Palabos library in *palabos*, make sure they are in the same directory level.
- I am using [CMake](https://cmake.org/) for cross-platform compiling. I use CMake because my laptop for a preliminary test is MacBook with MacOS but the cluster will always be Linux.
- I got two folders *cmake-build-debug* for locally compiling and *cmake-cluster* for the cluster end.
- The local version is built using CLion, everything is straightforward. On the cluster end, go to the folder *cmake-cluster* and use the command `cmake ../`
- Sometimes, we need to manually load cmake module. Use `module avail cmake` to check the available cmake version and use, e.g., `module load cmake/3.12.3` to load the new cmake version.

### Running Jobs
- For each project, there will be a corresponding batch file *\*\*.sh*. For example
```
#!/bin/bash
#SBATCH --account=def-SUPERVISOR
#SBATCH --time=01:00:00
#SBATCH --ntasks=64
#SBATCH --mem-per-cpu=128M
#SBATCH --job-name=JOBNAME
#SBATCH --output=%x-%j-np64.out

mpirun -np 64 ./projectName
```

- make sure everything is included
  - output directory created (or automatically created)
  - program parameters
  - have the modified code compiled (`make`)
- submit the job: `sbatch ./projectName.sh`
  - you will see *Submitted batch job 11315557*
- job status: `squeue -u $USER`
  - you will see *JOBID     USER      ACCOUNT           NAME  ST START_TIME        TIME_LEFT NODES CPUS   GRES MIN_MEM NODELIST (REASON)*
- cancel job: `scancel JobID`
- check the efficiency of the job: `seff JobID`
- The information of the submitted job, including the output, would be written in the *.out* files.

### File transfer
- File transfer is normally done by [Globus](https://www.globus.org/), details can be found [here](https://docs.computecanada.ca/wiki/Globus)

### CPU-based ParaView client-server visualization
For large data processing, it will be more convenient to handle it on the cluster end, making use of ParaView cliend-server mechanisms.

- check the [Compute Canada Documentation Wiki](https://docs.computecanada.ca/wiki/Visualization#CPU-based_ParaView_client-server_visualization_on_general_purpose_clusters)


