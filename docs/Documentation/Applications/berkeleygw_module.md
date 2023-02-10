# BerkeleyGW

[BerkeleyGW](https://www.berkeleygw.org) is a massively parallel many-body perturbation theory code capable of performing RPA, GW, and BGW-BSE calculations, which can be used to investigate properties of materials with high accuracy.

## Getting Started

This section provides the minimum amount of information needed to run a BerkeleyGW job on an NREL cluster.

First, see which versions of BerkeleyGW are available with `module avail` and load your preferred version with `module load`:

```console
module avail berkeleygw
   berkeleygw/3.0.1-cpu    berkeleygw/3.0.1-gpu (D)

module load berkeleygw/3.0.1-gpu
```

Next, create a job script. Below are example job scripts for the available NREL systems.

### Sample Job Scripts

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

??? example "Vermillion"

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

	# put module loads here

        # put export variables here

        # put srun command here, e.g.:
	srun epsilon.cplx.x

	```

??? example "Swift"

	```slurm
	#!/bin/bash

	# summarize number of nodes, number of tasks per node, and number of threads per task in this comment 

	#SBATCH --time=01:00:00
	#SBATCH --nodes=2
	#SBATCH --ntasks-per-node=18
	#SBATCH --cpus-per-task=2
	#SBATCH --partition=standard
	#SBATCH --account=Account to charge job to 

	# put module loads here

        # put export variables here

        # put srun command here, e.g.:
	srun epsilon.cplx.x

	```


## Troubleshooting

Include known problems and workarounds here, if applicable
