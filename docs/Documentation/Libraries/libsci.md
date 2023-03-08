# LibSci (Library for Scientific Computing)

**Documentation:** [LibSci](https://support.hpe.com/hpesc/public/docDisplay?docId=a00115110en_us&docLocale=en_US&page=Cray_Scientific_and_Math_Libraries_CSML_.html)

LibSci is a collection of numerical libraries developed by Cray for scientific and engineering computing. LibSci is optimized for performance on cray machines and interconnect architecture, and supports both single-precision and double-precision arithmetic. Most LibSci components contain both single- and multi-processor support along with multithreading support for parallel execution on shared-memory systems. Like [MKL](mkl.md), LibSci includes the following math functions: 

* BLAS (Basic Linear Algebra Subroutines) 
* CBLAS (C interface to the legacy BLAS) Note: not sure if this is also in MKL? 
* BLACS (Basic Linear Algebra Communication Subprograms) 
* LAPACK (Linear Algebra routines) 
* ScaLAPACK (parallel Linear Algebra routines) 

And additionally, libraries that are unique to Cray systems including: 
* IRT (Iterative Refinement Toolkit) - a library of solvers and tools that provides solutions to linear systems using single-precision factorizations while preserving accuracy through mixed-precision iterative refinement. 
* CrayBLAS - a library of BLAS routines autotuned for Cray XC series systems through extensive optimization and runtime adaptation.  

## Availability

LibSci is available on Kestrel only, as:
- Standard version: `cray-libsci/22.10.1.2` 
- For accelerators: `cray-libsci_acc/22.10.2.1`

## Resources

for an in-depth look at how to link scientific libraries when building software, see our [tutorial on linking libraries](deepdive.md).

for an overview of scientific libraries and quick comparison to other available libraries, see our [scientific libraries overview](intro_libraries.md).
