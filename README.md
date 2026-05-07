# bisicles_container
Definition files and configuration files for building BISICLES within a container

## Introduction
Containerisation allows you to compile code that can be easily ported from one platform to another (with some restrictions). As the name suggests, all the dependencies are contained -- there are no undefined references.

The BISICLES container comes with an operating system, compilers, libraries (MPI, HDF5, NetCDF, FFTW, PETSc) and the BISICLES executables (driver and filetools). . It can be thought as a replacement for the 
modules used on many high performance computers to load in dependencies.

## Prerequisites
You need to have Apptainer or Singularity installed.

## How to build a container
On an HPC, load Singularity/Apptainer then type
```
cd bisicles-container/defs
apptainer build bisicles.sif defs/bisicles_apptainer_petsc.def
```
or, on a local laptop if you encounter the error `FATAL: ...permission denied`,
```
sudo apptainer build --force bisicles.sif defs/bisicles_apptainer_petsc.def
```
Now take a cup of coffee.

Note: if you're using Singularity you may replace `apptainer` with `singularity` in the above and below commands.

## How to run a shell within a container
```
apptainer shell ~/bisicles-container/bisicles.sif
```
And then to run bisicles:
```
nohup mpirun -np 10 $BISICLES_HOME/BISICLES/code/exec2D/driver2d.Linux.64.mpicxx.mpif90.OPT.MPI.PETSC.ex
```
Or without PETSc:
```
nohup mpirun -np 10 $BISICLES_HOME/BISICLES/code/exec2D/driver2d.Linux.64.mpicxx.mpif90.OPT.MPI.ex
```
