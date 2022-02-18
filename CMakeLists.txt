cmake_minimum_required(VERSION 3.18)

project(ufs-weather-model
        VERSION 1.0
        LANGUAGES C CXX Fortran)

set(nems_binary ${CMAKE_CURRENT_SOURCE_DIR}/NEMS/exe/NEMS.x)

add_custom_command(OUTPUT ${nems_binary}
                  COMMAND gmake app=coupledFV3_AQM build
                  WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/NEMS
                  VERBATIM USES_TERMINAL)

add_custom_target(ufs_model ALL
                  COMMAND cp ${nems_binary} ${CMAKE_CURRENT_BINARY_DIR}/ufs_model
                  DEPENDS ${nems_binary})
