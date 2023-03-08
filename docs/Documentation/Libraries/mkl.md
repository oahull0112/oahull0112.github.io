# MKL (Math Kernel Library)


**Documentation:** [MKL](https://www.intel.com/content/www/us/en/developer/tools/oneapi/onemkl-documentation.html)

MKL is a collection of highly optimized mathematical libraries provided by Intel for use in scientific, engineering, and financial applications. The library is designed to take full advantage of the latest Intel processors, including multi-core processors, and can significantly improve the performance of numerical applications. Core math functions include: 

* BLAS (Basic Linear Algebra Subroutines) 
* LAPACK (Linear Algebra routines) 
* ScaLAPACK (parallel Linear Algebra routines) 
* Sparse Solvers 
* Fast Fourier Transforms 
* Vector Math 

## Availability

MKL is available on NREL systems:

| Kestrel                          | Swift                       | Vermillion           |
|:--------------------------------:|:---------------------------:|:--------------------:|
| intel-oneapi-mkl/2023.0.0-intel  |                             |                      |

## Resources

for an in-depth look at how to link to mkl when building software, see our [tutorial on linking libraries](deepdive.md).

for an overview of scientific libraries and quick comparison to other available libraries, see our [scientific libraries overview](intro_libraries.md).
