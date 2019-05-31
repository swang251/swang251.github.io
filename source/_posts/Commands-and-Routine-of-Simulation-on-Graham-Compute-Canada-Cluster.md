---
title: Simulation Routine, and Code/Result Management across Laptop and Cluster
toc: true
date: 2019-01-30 05:41:19
tags: [Research Daily, HPC, CAML]
categories: Research Daily
---


For my research involving the lattice Boltzmann method, I normally run most of the simulation on the cluster [GRAHAM](https://docs.computecanada.ca/wiki/Graham) of Compute Canada. It is boring and inconvenient to manage the code and the simulation results across my own laptop and the cluster. But still, I am building up my own way to manage everything and try to make it as easy as possible. Here I briefly note down how I organize my codes using Cmake and Git, and what is the routine of running simulation on the cluster.

<!--more-->

### Software/Tool List
- [Git](https://git-scm.com/) (version control)
- [Bitbucket](https://bitbucket.org/) (remote repository storage)
- [Sourcetree](https://www.sourcetreeapp.com/) (Git GUI)
- [CMake](https://cmake.org/) (cross-platform building software)
- [CLion](https://www.jetbrains.com/clion/) (C++ IDE)
- [Emacs](https://www.gnu.org/software/emacs/) (Text editor for code editing on the cluster)
- [Slurm](https://slurm.schedmd.com/overview.html) (job scheduler used by Compute Canada clusters)
- [Globus](https://www.globus.org/) (file transfer)
- [Paraview](https://www.paraview.org/) (result visualization)


### Login and Version Control
- For convenience, I make an alias of the ssh connection called `graham`. Details could be check in my [previous blog](https://swang251.github.io/2018/10/04/Passwordless-SSH-connection-to-a-Cluster/).
- I am using [Git](https://git-scm.com/) and [Bitbucket](https://bitbucket.org/) for version control.

### File Structure
- For the LBM simulation, I got my projects stored in the folder *lbm* and the Palabos library in *palabos*, make sure they are in the same directory level.
- Each project is named as the case short name + dimension. For example, I have *aeolianToneCylinder2D* and *ductRadiation2DAxisymmetric*.
- In each project, the file structure is shown below. It includes 
  - *main.cpp*: the main c++ file, 
  - *CMakeLists.txt*: the CMake configuration file,
  - *./laptop-cmake-build-debug/*: the workspace folder for the laptop, including the 
    - CMAKE workspace files,
	- Makefile,
	- excutable file,
	- .xml simulation setup file,
  - *./cluster-cmake-build-debug/*: the workspace folder for the cluster,
    - CMAKE workspace files,
	- Makefile,
	- excutable file,
	- .xml simulation setup file ,
	- .sh file for submitting batch jobs,
  - *./Analysis/*: the folder for the simulation results and the analysis scripts.
    - .m matlab script
	- .vtk for visualization
	- .dat for simulaiton 
```
aeolianToneCylinder2D
+-- main.cpp
+-- CMakeLists.txt
+-- laptop-cmake-build-debug
|   +-- aeolianToneCylinder2D.xml
+-- cluster-cmake-build-debug
|   +-- aeolianToneCylinder2D.xml
|   +-- aeolianToneCylinder2D.sh
+-- Analysis
|   +-- *.m
|   +-- ResultFolders
```

### Build and Compilation

- I am using [CMake](https://cmake.org/) for cross-platform project building (MacOS for my laptop and Linux on the cluster).
- Each platform owns its own workspace folder, i.e., *./laptop-cmake-build-debug* for the laptop and *./cluster-cmake-build-debug* for the cluster.
- The project on the laptop is built and debugged through CLion which is straight forward.
- On the cluster end, go to the folder *./cluster-cmake-build-debug* and use the command `cmake ../` to build the project. Then, use `make` to compile everything.
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
#SBATCH --mail-user=EMAILADDRESS
#SBATCH --mail-type=BEGIN
#SBATCH --mail-type=END
#SBATCH --mail-type=FAIL 

mpirun -np 64 ./projectName ./projectName.xml
```
  - `--mail` provides the option for notification at different stage of the simulation which is quite useful.

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


