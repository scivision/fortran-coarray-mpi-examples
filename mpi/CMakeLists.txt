set_directory_properties(PROPERTIES LABELS mpi)

add_executable(mpi_basic-C basic.c)
target_link_libraries(mpi_basic-C MPI::MPI_C)
add_test(NAME mpi_Cbasic COMMAND mpi_basic-C)

add_executable(mpi_version-C mpivers.c)
target_link_libraries(mpi_version-C MPI::MPI_C)
add_test(NAME mpi_Cversion COMMAND mpi_version-C)

set_tests_properties(mpi_Cbasic mpi_Cversion PROPERTIES TIMEOUT 5)


if(NOT MPI_Fortran_F08_MODULE_WORKS)
  message(STATUS "SKIP: MPI-3 Fortran tests")
  return()
endif()

add_executable(mpi_basic basic.f90)
target_link_libraries(mpi_basic MPI::MPI_Fortran)
add_test(NAME mpi_Fbasic COMMAND mpi_basic)

add_executable(mpi_version mpivers.f90)
target_link_libraries(mpi_version MPI::MPI_Fortran)
add_test(NAME mpi_version COMMAND mpi_version)

set_tests_properties(mpi_Fbasic mpi_version PROPERTIES TIMEOUT 5)

# --- more than one MPI image

add_executable(mpi_hello helloworld.f90)
target_link_libraries(mpi_hello MPI::MPI_Fortran)

add_test(NAME mpi:hello
COMMAND ${MPIEXEC_EXECUTABLE} ${MPIEXEC_NUMPROC_FLAG} ${MPIEXEC_MAX_NUMPROCS} $<TARGET_FILE:mpi_hello>
)
set_tests_properties(mpi:hello PROPERTIES
RESOURCE_LOCK cpu_mpi
TIMEOUT 5
FIXTURES_SETUP mpi_fxt
)

# --- actual message passing

add_executable(mpi_pass thread_pass.f90)
target_link_libraries(mpi_pass MPI::MPI_Fortran)

if(MPIEXEC_MAX_NUMPROCS GREATER_EQUAL 2)

add_test(NAME mpi:pass
COMMAND ${MPIEXEC_EXECUTABLE} ${MPIEXEC_NUMPROC_FLAG} 2 $<TARGET_FILE:mpi_pass>
)

set_tests_properties(mpi:pass PROPERTIES
RESOURCE_LOCK cpu_mpi
TIMEOUT 5
FIXTURES_REQUIRED mpi_fxt
)

endif()
