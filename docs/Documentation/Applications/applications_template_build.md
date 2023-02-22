# Template for an Application Page

**Documentation:**  [ link to documentation](https://nrel.gov)

Write a brief description of the program here.
Include a link to the program's website homepage.

## Getting Started

This section provides the minimum amount of information necessary to successfully run a basic job on an NREL Cluster.
This information should be as complete and self-contained as possible.

Instructions should be step-by-step and include copy-and-pastable commands where applicable.

This template is for applications that are not supported as modules by NREL, so are only accessible to users by building from source.

### Building From Source

Here, give detailed and step-by-step instructions on how to build the code, if this step is necessary. 

Include where to download the source code

??? example "Building on Kestrel"

	Be explicit in your instructions. Ideally a user reading one of these sections can following along step-by-step and have a functioning build by the end.
	
	```
	Include relevant commands in blocks.
	```
	or as in-line `blocks`

	Be sure to state how to set-up the necessary environment, e.g.:

	```
	module load gcc/8.4.0
	module load openmpi/3.1.6/gcc-8.4.0
	module load hdf5/1.10.6/gcc-ompi
	```


	!!! note
		You can use this section to draw attention to important information.

	Give instructions on compile commands. E.g., to view the available make targets, type `make`. To compile all program executables, type:

	```
	make cleanall
	make all
	```


??? example "Building on Vermillion"

	information on how to build on Vermillion

??? example "Building on Swift"

	information on how to build on Swift


!!! note 
	You can use this section to draw attention to important information.

Include a section on how to run the job, e.g. with job script examples or commands for an interactive session.


### Example Job Scripts

??? example "Kestrel CPU"

	```slurm
	#!/bin/bash

	# In a comment summarize the hardware requested, e.g. number of nodes, 
        # number of tasks per node, and number of threads per task

	#SBATCH --time=
	#SBATCH --nodes=
	#SBATCH --ntasks-per-node=
	#SBATCH --cpus-per-task=
	#SBATCH --partition=
	#SBATCH --account=

	# include a section of relevant export and module load commands, e.g.:

	module load gcc/8.4.0

	export OMP_NUM_THREADS=

	# include a sample srun command or similar
	srun program.x

	```

??? example "Vermillion"

	If the submit script for Vermillion differs from Kestrel, then include a Vermillion example script here.
	If the submit script does not differ, then remove this section (starting from the `??? example "Vermillion"` line)


??? example "Swift"

	If the submit script for Swift differs from Kestrel, then include a Swift  example script here.
	If the submit script does not differ, then remove this section (starting from the `??? example "Swift"` line)


??? example "Template"
	
	Here's a template of a collapsible example.

	```
	You can include blocked sections
	```

	And unblocked sections.


## Advanced

Include advanced user information about the code here (see BerkeleyGW pages for example)

## Troubleshooting

Include known problems and workarounds here, if applicable


