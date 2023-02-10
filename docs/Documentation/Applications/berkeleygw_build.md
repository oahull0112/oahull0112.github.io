# BerkeleyGW

[BerkeleyGW](https://www.berkeleygw.org) is a massively parallel many-body perturbation theory code capable of performing RPA, GW, and BGW-BSE calculations, which can be used to investigate properties of materials with high accuracy.

## Getting Started

This section provides the minimum amount of information needed to run a BerkeleyGW job on an NREL cluster.

BerkeleyGW must be built from source to run on NREL systems.

## Building Instructions

Include step-by-step instructions that the user can paste into their terminally

First, [download BerkeleyGW](https://berkeleygw.org/download/) 

??? example "Building on Kestrel"

	The following `arch.mk` file was used to build BerkeleyGW-3.0 on Kestrel on (date).
        Copy this arch.mk file into your BerkeleyGW directory.
	
	```make
	COMPFLAG  = -DGNU
	PARAFLAG  = -DMPI -DOMP
	MATHFLAG  = -DUSESCALAPACK -DUNPACKED -DUSEFFTW3 -DHDF5
	
	FCPP    = /usr/bin/cpp -C
	F90free = mpifort -ffree-form -ffree-line-length-none -fopenmp -fno-second-underscore -cpp
	LINK    = mpifort -fopenmp
	# FHJ: -funsafe-math-optimizations breaks Haydock and doesn't give any significant speedup
	FOPTS   = -O3 -funroll-loops 
	FNOOPTS = $(FOPTS)
	MOD_OPT = -J  
	INCFLAG = -I
	
	C_PARAFLAG  = -DPARA
	CC_COMP = mpiCC
	C_COMP  = mpicc
	C_LINK  = mpicc
	C_OPTS  = -O3 -ffast-math
	C_DEBUGFLAG = 
	
	REMOVE  = /bin/rm -f
	
	# Math Libraries                                                                                                                                                                                            
	FFTWPATH     =  /projects/scatter/mylibraries_CentOS77/
	#/nopt/nrel/apps/fftw/3.3.3-impi-intel/
	#FFTWLIB      = $(FFTWPATH)/lib/libfftw3.a
	FFTWLIB      =  $(FFTWPATH)/lib/libfftw3_omp.a $(FFTWPATH)/lib/libfftw3.a
	FFTWINCLUDE  =  $(FFTWPATH)/include
	
	LAPACKLIB = /projects/scatter/mylibraries_CentOS77/lib/libopenblas.a
	
	SCALAPACKLIB = /projects/scatter/mylibraries_CentOS77/lib/libscalapack.a
	
	HDF5PATH      = /nopt/nrel/apps/base/2020-05-12/spack/opt/spack/linux-centos7-x86_64/gcc-8.4.0/hdf5-1.10.6-dj4jq2ffttkdxksimqe47245ryklau4a
	HDF5LIB      =  ${HDF5PATH}/lib/libhdf5hl_fortran.a \
	                ${HDF5PATH}/lib/libhdf5_hl.a \
	                ${HDF5PATH}/lib/libhdf5_fortran.a \
	                ${HDF5PATH}/lib/libhdf5.a /home/ohull/.conda-envs/bgw/lib/libsz.a -lz -ldl
	HDF5INCLUDE  = ${HDF5PATH}/include

	PERFORMANCE  =

	TESTSCRIPT = 
	```

	Then, load the following modules:

	```
	module load gcc/8.4.0
	module load openmpi/3.1.6/gcc-8.4.0
	module load hdf5/1.10.6/gcc-ompi
	```

	Choose whether to use the real or complex flavor of BerkeleyGW by copying the corresponding file to flavor.mk. For example, for the complex version:

	`cp flavor_cplx.mk flavor.mk`

	!!! note
		If you are unsure which to use, select the complex flavor.

	Finally, compile the code. To view the available make targets, type `make`. To compile all BerkeleyGW executables, type:
	```
	make cleanall
	make all
	```


??? example "Building on Vermillion"

	information on how to build on Vermillion

??? example "Building on Swift"

	information on how to build on Swift

## Sample Job Scripts

??? example "Kestrel CPU"

	```slurm
	#!/bin/bash

	# summarize number of nodes, number of tasks per node, and number of threads per task in this comment 

	#SBATCH --time=01:00:00
	#SBATCH --nodes=2
	#SBATCH --ntasks-per-node=18
	#SBATCH --cpus-per-task=2
	#SBATCH --partition=standard
	#SBATCH --account=Account to charge job to 

	export OMP_NUM_THREADS=2

	srun epsilon.cplx.x
	```
		
??? example "Kestrel GPU"

	Put job example here

??? example "Vermillion"

	Put job example here

??? example "Swift"

	Put job example here

## Troubleshooting

Include known problems and workarounds here, if applicable

## Documentation

Documentation for the BerkeleyGW program can be found [here](https://berkeleygw.org/documentation/)
