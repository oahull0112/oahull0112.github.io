# Fortran
!!! tip "NOTE"
	This page is a **prototype**. Verify that the information is accurate if you copy and paste sections (e.g. make sure the listed compilers/MPI are indeed available, etc.)


## Getting Started
This section provides the minimum amount of information necessary to successfully compile a basic Fortran code, and then a basic Fortran MPI code. See [External Resources](https://nrel.gov) for general Fortran language tutorials and Fortran-MPI tutorials.

### Hello World

First, we must choose the compiler with which to compile our program. We can choose between the GNU, Intel, Nvidia, and Cray compilers. For more information on compilers, see [Compilers](https://nrel.gov).

To see available versions of a chosen compiler, use `module avail`. For this example, we'll use gfortran, which is part of GNU's `gcc` package:

```
module avail gcc
   gcc/10.3.0          gcc/11.2.0          gcc/12.1.0(default)
```

To load a particular compiler, use `module load`. We'll use gcc/12.1.0.

```
module load gcc/12.1.0
```

Create a file named hello.f90, and save the following text to the file:

```
PROGRAM hello

write(*,*) "Hello World"

END PROGRAM hello
```

Now, we can compile the program with the following command:

`gfortran hello.f90 -o hello`

This creates an executable named `hello`. Execute it by typing the following into your terminal:

`./hello`

It should return the following output:

`Hello World`

### Hello World in MPI Parallel

Now that we have a working Hello World program, let's modify it to run on multiple MPI tasks.

On Kestrel, there are multiple implementations of MPI available. We can choose between OpenMPI, Intel MPI, MPICH, Nvidia's nvhpc, and Cray MPICH. These MPI implementations are associated with an underlying Fortran compiler. For example, if we type:

`module avail openmpi`

we find that both `openmpi/4.1.4-gcc` and `openmpi/4.1.4-intel` are available.

Let's choose the openmpi/gcc combination:

`module load openmpi/4.1.4-gcc`

Now, create a new file named `hello_mpi.f90` and save the following contents to the file:

```
PROGRAM hello_mpi
include 'mpif.h'

integer :: ierr, my_rank, number_of_ranks

call MPI_INIT(ierr)
call MPI_COMM_SIZE(MPI_COMM_WORLD, number_of_ranks, ierr)
call MPI_COMM_RANK(MPI_COMM_WORLD, my_rank, ierr)

write(*,*) "Hello World from MPI task: ", my_rank, "out of ", number_of_ranks

call MPI_FINALIZE(ierr)

END PROGRAM hello_mpi
```

To compile this program, type:

`mpif90 hello_mpi.f90 -o hello_mpi`

To run this code on the login node, type:

`mpirun -n 4 ./hello_mpi`

You should receive a similar output to the following (the rank ordering may differ):

```
 Hello World from MPI task:            1 out of            4
 Hello World from MPI task:            2 out of            4
 Hello World from MPI task:            3 out of            4
 Hello World from MPI task:            0 out of            4
```

Generally, we don't want to run MPI programs on the login node! Let's submit this code as a job. Create a file named `job.in` and modify the file to contain the following:

```
#!/bin/bash

#SBATCH --time=00:01:00
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=4
#SBATCH --partition=debug
#SBATCH --account=

module load openmpi/4.1.4-gcc

srun -n 4 ./hello_mpi &> hello.out

```

Submit the job by typing:

`sbatch job.in`

When the job is done, the file hello.out should contain the same output as you found before (the ordering of ranks may differ).

## Compilers

Available Fortran compilers:

* Include versions, also? Or just say to `module avail compiler`?
* Could make sense to have two subsections here, one for standalone compilers, and another for PrgEnv programming environments
* Actualy, three sections: standalone fortran compilers, PrgEnv associated compilers, and Fortran-MPI (both standalone and prgenv sections?)
* could have a table, something like:

| Creator | Compiler Executable | Module Avail | Available Versions |
|:-------:|:-------------------:|:------------:|:------------------:|
| GNU     | gfortran            | gcc          | 12.1.0, 11.2.0, 10.3.0, 10.1.0|
| Intel   | ifort               | intel-oneapi | 2023.0.0, 2022.1.0, 2021.8.0 |
| Intel   | ifort               | intel-classic| 2022.1.0
| Cray    | ftn                 | cce          | 14.0.4
| Nvidia  | nvfortran           | nvhpc        | 22.7

Note that in addition to the standalone Fortran compilers listed above, the various available programming environments available on the HPC (use `module avail PrgEnv` to view available programming environments) contain an associated Fortran compiler. For example, `module load PrgEnv-gnu/8.3.3` will load gfortran/12.1.0 into your environment, which you can verify with the `gfortran --version` command. If using a PrgEnv from a given creator, the loaded fortran compiler executable will be given by the same name as listed in the above table.

| Creator | Compiler Executable | Module Avail          | Fortran Compiler Version |
|:-------:|:-------------------:|:---------------------:|:------------------------:|
| GNU     | gfortran            | PrgEnv-gnu/8.3.3      | 12.1.0
| GNU     | gfortran            | PrgEnv-gnu-amd/8.3.3  | broken?
| Intel   | ifort               | PrgEnv-intel/8.3.3    | 2021.6.0
| Cray    | ftn                 | PrgEnv-Cray/8.3.3     | 14.0.4
| Nvidia  | nvfortran           | PrgEnv-nvhpc/8.3.3    | 22.7.0
| Nvidia  | nvfortran           | PrgEnv-nvidia/8.3.3   | broken?

Available Fortran-MPI compilers ('toolchains'?):

* list

| Creator | Compiler Executable | Module Avail          | MPI version |Fortran Compiler Version |
|:-------:|:-------------------:|:---------------------:|:-----------:|:-----------------------:|
|


## Troubleshooting

Include known problems and workarounds here, if applicable

## External Resources

* [Basic Fortran Tutorial](https://pages.mtu.edu/~shene/COURSES/cs201/NOTES/fortran.html) 
* [Fortran/MPI on an HPC Tutorial](https://curc.readthedocs.io/en/latest/programming/MPI-Fortran.html)

