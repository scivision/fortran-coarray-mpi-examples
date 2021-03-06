# Fortran Coarray and MPI Examples

[![cmake](https://github.com/scivision/fortran-coarray-mpi-examples/actions/workflows/cmake.yml/badge.svg)](https://github.com/scivision/fortran-coarray-mpi-examples/actions/workflows/cmake.yml)
[![intel-oneapi](https://github.com/scivision/fortran-coarray-mpi-examples/actions/workflows/intel-oneapi.yml/badge.svg)](https://github.com/scivision/fortran-coarray-mpi-examples/actions/workflows/intel-oneapi.yml)

A few very basic examples, perhaps use to test Coarray and MPI library functionality.
GCC/Gfortran, Intel oneAPI, NAG, Cray, IBM XL and other compilers support Fortran 2008 Coarrays.

Free, popular MPI 3.0 interfaces for C and Fortran include:

* [OpenMPI](https://www.open-mpi.org/) (Linux, Mac)
* [MPICH](https://www.mpich.org/) (Linux, Mac)
* [Intel MPI](https://software.intel.com/content/www/us/en/develop/tools/oneapi/components/mpi-library.html#gs.01cdz4) (Linux, Windows)

Build:

```sh
cmake -B build
cmake --build build
```

Run self-tests:

```sh
ctest --test-dir build
```

## Message Passing

Pass data between two MPI threads.
In this usage, MPI_Recv blocks waiting for MPI_Send

```sh
mpirun -np 2 mpi/mpi_pass
```

## Notes

See
[OpenMPI docs](https://www.open-mpi.org/faq/?category=running#adding-ompi-to-path)
re: setting PATH and LD_LIBRARY_PATH if CMake has trouble finding OpenMPI for a compiler.

* https://hpc-forge.cineca.it/files/CoursesDev/public/2017/MasterCS/CalcoloParallelo/MPI_Master2017.pdf
