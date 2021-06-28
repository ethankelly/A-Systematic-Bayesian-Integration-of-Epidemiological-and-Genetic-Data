cmake_minimum_required(VERSION 3.19)
project(A_Systematic_Bayesian_Integration_of_Epidemiological_and_Genetic_Data)

# see here: https://github.com/PointCloudLibrary/pcl/issues/3680
# when this is fixed, we can remove the following 3 lines.
if (NOT DEFINED CMAKE_SUPPRESS_DEVELOPER_WARNINGS)
    set(CMAKE_SUPPRESS_DEVELOPER_WARNINGS 1 CACHE INTERNAL "No dev warnings")
endif ()

set(CMAKE_CXX_STANDARD 14)

include_directories(scripts)

set(SOURCE_FILES scripts/phylo_seir_fmd_inference.cpp
        scripts/phylo_seir_fmd_inference_functions.cpp
        scripts/phylo_seir_fmd_inference_header.h
        scripts/phylo_seir_fmd_inference_IO.cpp)

add_executable(A_Systematic_Bayesian_Integration_of_Epidemiological_and_Genetic_Data ${SOURCE_FILES})

find_package(GSL REQUIRED ~/usr/library/Cellar/gsl)
# Either specify BOOST_ROOT or BOOST_INCLUDEDIR and BOOST_LIBRARYDIR.
set(BOOST_ROOT "~/usr/local/Cellar/boost/1.76.0")
set(BOOST_INCLUDEDIR "~/usr/local/Cellar/boost/1.76.0/include")
set(BOOST_LIBRARYDIR "~/usr/local/Cellar/boost/1.76.0/lib")
set(Boost_NO_SYSTEM_PATHS ON)
set(Boost_USE_MULTITHREADED ON)
set(Boost_USE_STATIC_LIBS ON)
set(Boost_USE_STATIC_RUNTIME OFF)
set(BOOST_ALL_DYN_LINK OFF)

# Load settings for the external project "Boost".
find_package(Boost 1.76.0 REQUIRED COMPONENTS system filesystem)
if (Boost_FOUND)
    include_directories(SYSTEM ${Boost_INCLUDE_DIR})
    #link_directories (${Boost_LIBRARY_DIRS})
endif ()
target_link_libraries(A_Systematic_Bayesian_Integration_of_Epidemiological_and_Genetic_Data GSL::gsl GSL::gslcblas)
