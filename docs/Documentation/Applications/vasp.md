# Template for an Application Page

**Documentation:** [VASP](https://www.vasp.at/wiki/index.php/The_VASP_Manual)

VASP computes an approximate solution to the many-body Schrödinger equation, either within density functional theory (DFT), solving the Kohn-Sham equations, or within the Hartree-Fock (HF) approximation, solving the Roothaan equations. Hybrid functionals that mix the Hartree-Fock approach with density functional theory are implemented as well. Furthermore, Green's functions methods (GW quasiparticles, and ACFDT-RPA) and many-body perturbation theory (2nd-order Møller-Plesset) are available in VASP.

In VASP, central quantities, like the one-electron orbitals, the electronic charge density, and the local potential are expressed in plane wave basis sets. The interactions between the electrons and ions are described using norm-conserving or ultrasoft pseudopotentials, or the projector-augmented-wave method.

To determine the electronic ground state, VASP makes use of efficient iterative matrix diagonalization techniques, like the residual minimization method with direct inversion of the iterative subspace (RMM-DIIS) or blocked Davidson algorithms. These are coupled to highly efficient Broyden and Pulay density mixing schemes to speed up the self-consistency cycle. 

## Getting Started

### Accessing VASP

The VASP license requires users to be a member of a "workgroup" defined by the University of Vienna or Materials Design. If you are receiving "Permission denied" errors when trying to use VASP, you must be made part of the "vasp" Linux group first. To join, please contact us with the following information: 
* Your name
* The workgroup PI
* Whether you are licensed through Vienna (academic) or Materials Design, Inc. (commercial)
* If licensed through Vienna:
	- the e-mail address under which you are registered with Vienna as a workgroup member (this may not be the e-mail address you used to get an HPC account)
	- Your VASP license ID
* If licensed through Materials Design,
	- Proof of current licensed status

Once status can be confirmed, we can provide access to our VASP builds.

### Setting Up Software Environment

First, see which modules of VASP are available:

`module avail vasp`

and select a version:

`module load vasp/6.1.2`

Three distinct executables have been made available:

1. `vasp_gam` is for Gamma-point-only runs typical for large unit cells
2. `vasp_std` is for general k-point meshes with collinear spins
3. `vasp_ncl` is for general k-point meshes with non-collinear spins

`vasp_gam` and `vasp_std` builds include the alternative optimization and [transition state theory tools from University of Texas-Austin](http://theory.cm.utexas.edu/vtsttools/) developed by Graeme Henkelman's group, and [implicit solvation models from the University of Florida](https://vaspsol.mse.ufl.edu/) developed by Mathew and Hennig. 

### Example Job Scripts

??? example "Kestrel CPU"

	```slurm
	#!/bin/bash --login
	#SBATCH --job-name=job_name   # Replace job_name with your own
	#SBATCH --nodes=2             # This will deliver 2 36-core nodes
	#SBATCH --time=02:00:00       # REPLACE
	#SBATCH –-account=account_id  # Replace with your allocation ID
	#SBATCH --error=%x-%A.err     # This will create stderr file <job_name>-<jobid>.err
	#SBATCH --output=%x-%A.out .  # This will create stdout file <job_name>-<jobid>.out
	
	module purge
	module load vasp/6.1.2
	 
	JOB_BASENAME=$SLURM_JOB_NAME  # Captures the --job_name value from above
	SCRATCH=/scratch/$USER/$JOB_BASENAME
	 
	if [ -d $SCRATCH ]
	then
	   rm -rf $SCRATCH
	fi
	mkdir $SCRATCH
	
	cd $SLURM_SUBMIT_DIR  # Assumes you submitted job from directory containing VASP input
	
	# Minimal files needed for VASP run
	cp INCAR KPOINTS POSCAR POTCAR  $SCRATCH/.
	
	cd $SCRATCH

	# make sure to choose the correct VASP executable. Here we use vasp_gam
	srun -n $SLURM_NTASKS vasp_gam > $JOB_BASENAME.log

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

Include instructions on how to submit the job script

## Supported Versions

| Kestrel | Swift | Vermillion |
|:-------:|:-----:|:----------:|
| 0.0.0   | 0.0.0 | 0.0.0      |

## Advanced

Include advanced user information about the code here 

One common "advanced case" might be that users want to build their own version of the code.

### Building From Source

Here, give detailed and step-by-step instructions on how to build the code, if this step is necessary. Include detailed instructions for how to do it on each applicable HPC system. Be explicit in your instructions. Ideally a user reading one of the build sections can follow along step-by-step
and have a functioning build by the end.

If building from source is not something anyone would reasonably want to do, remove this section.

Be sure to include where the user can download the source code

??? example "Build Instructions on Kestrel"

	Include here, for example, a Kestrel-specific makefile (see berkeleygw example page). This template assumes that we build the code with only one toolchain, which may not be the case. If someone might reasonably want to build with multiple toolchains, use the "Multiple toolchain instructions on Kestrel" template instead.
	
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

	Give instructions on compile commands. E.g., to view the available make targets, type `make`. To compile all program executables, type:

	```
	make cleanall
	make all
	```
	
??? example "Building on Vermillion"

	information on how to build on Vermillion

??? example "Building on Swift"

	information on how to build on Swift


## Troubleshooting

Include known problems and workarounds here, if applicable

