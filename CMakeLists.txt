project                     (DioDe)
cmake_minimum_required      (VERSION 2.8)

# Default to Release
if                          (NOT CMAKE_BUILD_TYPE)
    set                     (CMAKE_BUILD_TYPE "Release" CACHE STRING "Choose the type of build, options are: Debug Release RelWithDebInfo MinSizeRel." FORCE)
    set_property            (CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release" "MinSizeRel" "RelWithDebInfo")
endif                       (NOT CMAKE_BUILD_TYPE)

include_directories         (include)

find_package                (CGAL)
include                     (${CGAL_USE_FILE})
add_definitions             (${CGAL_CXX_FLAGS_INIT})
include_directories         (${CGAL_INCLUDE_DIRS})

# CGAL 4.9.1 removes -O3 from the release flags. I want it back.
if                          (${CMAKE_BUILD_TYPE} STREQUAL "Release")
    set                     (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")
endif                       ()

set                         (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

add_subdirectory            (ext/pybind11)

add_subdirectory            (examples)
add_subdirectory            (bindings/python)
