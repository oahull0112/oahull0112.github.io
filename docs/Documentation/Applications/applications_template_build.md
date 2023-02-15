# Template for an Application Page

**Documentation**  [ link to documentation](https://nrel.gov)

Write a brief description of the program here.

## Getting Started

This section provides the minimum amount of information necessary to successfully run a basic job on an NREL Cluster.
This information should be as complete and self-contained as possible.

Instructions should be step-by-step and include copy-and-pastable commands where applicable.

For example, describe how the user can load the program module with `module avail` and `module load`:

```
module avail program
   program/2.0.0    program/1.0.0
```

```
module load program/2.0.0
```

### Building From Source

Here, give detailed and step-by-step instructions on how to build the code, if this step is necessary. 

If building from source is not necessary for the user (e.g. because it already exists as a module), but might be something that power users would want to do, then move this entire section out from under the `Getting Started` section.

If building from source is unlikely to be something users have  an interest in, then use the `application_template_module.md` file as a template instead.

If building from source is necessary, include detailed instructions for how to do it on each applicable HPC system:

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
!!! note
	You can use a note to draw attention to the information in this section

!!! note
	If the submit scripts for Vermillion, Swift, and Kestrel are all the same, remove all of the submit script collapsible sections (remove the `??? example` headers that are inside the `### Example Job Scripts` header), and give a submit script directly below the `### Example Job Scripts` header.


## Advanced

Include advanced user information about the code here (see BerkeleyGW pages for example)

## Troubleshooting

Include known problems and workarounds here, if applicable


