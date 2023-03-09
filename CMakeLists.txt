project(mmpbsa_py)

#Sources for nab executables.
#Only built in serial builds.
set(MMPBSA_NABNMODE_SOURCES mmpbsa_entropy.nab)
set(MMPBSA_ENERGY_SOURCES mmpbsa_energy.nab)

#------------------------------------------------------------------------------------------

install_python_library()

add_nab_executable(mmpbsa_py_nabnmode NAB_SOURCES ${MMPBSA_NABNMODE_SOURCES})
add_nab_executable(mmpbsa_py_energy NAB_SOURCES ${MMPBSA_ENERGY_SOURCES})

install(TARGETS mmpbsa_py_energy mmpbsa_py_nabnmode DESTINATION ${BINDIR} COMPONENT Python)

if(MPI)
	if(NOT mpi4py_ENABLED)
		message(STATUS "WARNING: MMPBSA.py.MPI will not be usable since mpi4py is not enabled")
	endif()
endif()