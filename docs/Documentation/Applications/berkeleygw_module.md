# BerkeleyGW

**Documentation:** [BerkeleyGW](https://www.berkeleygw.org)

[BerkeleyGW](https://www.berkeleygw.org) is a massively parallel many-body perturbation theory code capable of performing RPA, GW, and GW-BSE calculations, which can be used to investigate properties of materials with high accuracy.

## Getting Started

This section provides the minimum amount of information needed to run a BerkeleyGW job on an NREL cluster.

First, see which versions of BerkeleyGW are available with `module avail` and load your preferred version with `module load`:

```console
module avail berkeleygw
   berkeleygw/3.0.1-cpu    berkeleygw/3.0.1-gpu (D)
```
The `module avail berkeleygw` command shows that two BerkeleyGW modules are available. To select the GPU-enabled version of BerkeleyGW, for example, we use the `module load` command:

```console
module load berkeleygw/3.0.1-gpu
```

Next, create a job script. Below are example job scripts for the available NREL systems. Continuing the above example, we would select the "Kestrel GPU" example script.

### Sample Job Scripts

??? example "Kestrel CPU"

	```slurm
	#!/bin/bash

	# This job requests 72 MPI tasks across 2 nodes (36 tasks/node) and no threading

	#SBATCH --time=01:00:00
	#SBATCH --nodes=2
	#SBATCH --ntasks-per-node=36
	#SBATCH --partition=standard
	#SBATCH --account=


	srun epsilon.cplx.x

	```

??? example "Kestrel GPU"

	Populate with Kestrel GPU submission script
	```slurm
	Put the script inside a code block
	```

??? example "Vermillion"

	Populate with Vermillion submission script
	```slurm
	Put the script inside a code block
	```

??? example "Swift"

	Populate with Swift submission script
	```slurm
	Put the script inside a code block
	```

In the above scripts, be sure to include your allocation on the `#SBATCH --account` line.

Save the submit script with the filename of your choice, e.g. "bgw.in"

To submit the job to the scheduler, type:

`sbatch bgw.in`

## Advanced

### IO Settings

For large systems, the wavefunction binary file format yields significantly slower read-in times relative to an HDF5-format wavefunction file. The BerkeleyGW code includes utilities to convert wavefunction binary files to HDF5 format and vice-versa called hdf2wfn.x and wfn2hdf.x (see [documentation](
http://manual.berkeleygw.org/3.0/meanfield-utilities/#wfn2hdfx)). It is recommended to use HDF5-formatted wavefunction files where possible.

### Lustre File Striping

BerkeleyGW supports wavefunction files in HDF5 format and binary format. Wavefunction inputs to BerkeleyGW can become large depending on the system under investigation. Large (TODO: define large for Kestrel. Probably > 10 GB) HDF5 wavefunction files benefit from Lustre file striping, and the BerkeleyGW code can see major runtime speed-ups when using this feature.

!!! tip
	Binary format wavefunction files do not benefit from Lustre file striping

For more on Lustre file striping, see (TODO: documentation section on Lustre file striping?)

### Advanced submission script example

Because multiple executables in BerkeleyGW require the WFN input files (WFN and WFNq), we can streamline the file linking inside a submission script. We can also include the Lustre file striping step in our submission script. The below example script shows how this can be done for the BerkeleyGW epsilon executable.

??? example "Advanced submit script"

	```slurm
	#!/bin/bash
	#SBATCH -t 00:20:00
	#SBATCH -N 8
	#SBATCH --gpus-per-node=4
	#SBATCH -C gpu
	#SBATCH -o BGW_EPSILON_%j.out
	#SBATCH --account=
	
	WFN_folder=/path/to/folder/that/contains/WFN/and/WFNq
	
	mkdir BGW_EPSILON_$SLURM_JOBID
	lfs setstripe -c 60 BGW_EPSILON_$SLURM_JOBID
	cd    BGW_EPSILON_$SLURM_JOBID
	ln -s  ../epsilon.inp .
	ln -sfn  ${WFN_folder}/WFNq.h5      .   
	ln -sfn  ${WFN_folder}/WFN.h5   ./WFN.h5
	
	ulimit -s unlimited
	export OMP_PROC_BIND=true
	export OMP_PLACES=threads
	export BGW_WFN_HDF5_INDEPENDENT=1
	
	export OMP_NUM_THREADS=16
	srun -n 32 -c 32 --cpu-bind=cores ./epsilon.cplx.x
	```
	
Submit the job with `sbatch submit_script_filename`


## Troubleshooting

Include known problems and workarounds here, if applicable

Maybe include here notable differences between NREL clusters for BerkeleyGW?


