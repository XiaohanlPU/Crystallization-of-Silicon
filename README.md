# Tutorial: Crystallization of Silicon

This repository contains input files for simulating the crystallization of silicon using enhanced sampling methods.
Silicon is described using the Stillinger-Weber potential [Stillinger and Weber,  Phys. Rev. B, v. 31, p. 5262, (1985)](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.31.5262).

## Requirements

This tutorial uses the molecular dynamics engine LAMMPS patched with the PLUMED 2 enhanced sampling plugin.

### Installation

<!--
PLUMED can be installed with the following commands:
```
mkdir plumed2-install
installfolder=$(pwd)/plumed2-install
wget https://github.com/plumed/plumed2/releases/download/v2.6.0/plumed-2.6.0.tgz
tar -xf plumed-2.6.0.tgz
cd plumed-2.6.0/
./configure --prefix=$installfolder
make -j 2
make install
cd ..
```
If the previous commands are succesful, you can proceed to install LAMMPS:
-->

LAMMPS and PLUMED can be installed with the following commands:

```
wget https://github.com/lammps/lammps/archive/stable_3Mar2020.tar.gz
tar -xf stable_3Mar2020.tar.gz
cd lammps-stable_3Mar2020/src
make lib-plumed args="-b"
make yes user-plumed
make yes-manybody
make yes-molecule
make mpi # or make serial if you don't have an MPI library
lammpsexe=$(pwd)/lmp_mpi # or lammpsexe=$(pwd)/lmp_serial if you don't have an MPI library
cd ../lib/plumed/plumed2/bin/
plumedexe=$(pwd)/plumed
```

Now you should be able to use *$lammpsexe* and *$plumedexe* to execute LAMMPS and PLUMED, respectively.
If you close the shell these variables will be lost.
A better alternative for more experienced users would be to include the appropriate folders in the *PATH* environment variable by adding a line in your ```~/.bashrc```.

## Introduction


## Example

The folder ```Metadynamics-1700K``` contains the input files to run the simulation.
You can run the example with the command:
```
$lammpsexe < start.lmp > out.lmp
```
This will run a 5 ns long metadynamics simulation at 1700 K and 1 bar.
Several output files will be created.
out.lmp file contains LAMMPS' output.
PLUMED's output files are plumed.out and COLVAR.
Inspect the COLVAR file, this will contain the collective variable, the bias potential, and other interesting quantities as a function of simulation time.

## Objectives

The following tasks are proposed:
* Repeat the simulation at different temperatures, e.g. in steps of 50 o 100 K
* Study the convergence of the free energy surface (FES) as a function of simulation time (a minimum of 2 ns per simulation is required and 5 ns are suggested)
* Plot the FES obtained at different temperatures
* Calculate the liquid-solid free energy difference (one should integrate the FES but the difference in free energy between the minima should be a good approximation) 
* Calculate the melting temperature and discuss finite size effects
