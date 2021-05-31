cmake_minimum_required(VERSION 2.8)
 
PROJECT(demoEMDQ)

set( CMAKE_BUILD_TYPE Release )
set( CMAKE_CXX_FLAGS "-std=c++11 -Wall -O2 -march=native" )

find_package( OpenCV REQUIRED )
find_package( Eigen3 REQUIRED )
include_directories(${EIGEN3_INCLUDE_DIR})

find_package(OpenMP)
if (OPENMP_FOUND)
    set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
    set (CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
endif()

add_executable(demoEMDQ demo.cxx EMDQ.h EMDQ.cxx DualQ.h DualQ.cxx)

target_link_libraries( demoEMDQ ${OpenCV_LIBS})

if (OPENMP_FOUND)
	target_link_libraries( demoEMDQ PRIVATE OpenMP::OpenMP_CXX)
endif()
