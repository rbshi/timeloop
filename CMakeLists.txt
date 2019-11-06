cmake_minimum_required(VERSION 3.10)

project(timeloop VERSION 1.0)

# package requirements
find_library(LIBCONFIG++ NAMES config++ libconfig++)
if(NOT LIBCONFIG++)
  message(FATAL_ERROR "config++ library not found")
endif()
# find_library(LIBYAML-CPP NAMES yaml-cpp)
# find_library(ncurses ncurses)
# find_library(boost_iostreams)
# find_library(boost_serialization)
# find_library(tinfo)
# find_library(gpm)

include_directories(src)

set( CMAKE_CXX_FLAGS "-Wall -Wextra -fmax-errors=1 -std=c++14 -pthread" )
set( CMAKE_EXE_LINKER_FLAGS "-std=c++11 -static-libgcc -static-libstdc++ -pthread -lconfig++ -lyaml-cpp -lncurses -lboost_iostreams -lboost_serialization" )

# get_filename_component( CURRENT_SOURCE_ABS_DIR  ${CMAKE_CURRENT_SOURCE_DIR} ABSOLUTE )
add_definitions( -DBUILD_BASE_DIR=\"${CMAKE_CURRENT_SOURCE_DIR}\" )

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})

set(SOURCES_MAPPER
    src/data/cnn/cnn-layers.cpp
    src/loop-analysis/tiling.cpp
    src/loop-analysis/nest-analysis.cpp
    src/pat/pat.cpp
    src/applications/mapper/main.cpp
    src/mapping/loop.cpp
    src/mapping/nest.cpp
    src/mapping/mapping.cpp
    src/mapspaces/mapspace-base.cpp
    src/model/arithmetic.cpp
    src/model/buffer.cpp
    src/model/topology.cpp
    src/util/numeric.cpp
    src/util/map2d.cpp
    src/workload/problem-shape.cpp
    src/workload/workload.cpp
    src/workload/operation-space.cpp
    src/compound-config/compound-config.cpp
    )
set (SOURCES_MODEL
    src/data/cnn/cnn-layers.cpp
    src/loop-analysis/tiling.cpp
    src/loop-analysis/nest-analysis.cpp
    src/pat/pat.cpp
    src/applications/evaluator/main.cpp
    src/mapping/loop.cpp
    src/mapping/nest.cpp
    src/mapping/mapping.cpp
    src/mapping/parser.cpp
    src/model/arithmetic.cpp
    src/model/buffer.cpp
    src/model/topology.cpp
    src/util/numeric.cpp
    src/util/map2d.cpp
    src/workload/problem-shape.cpp
    src/workload/workload.cpp
    src/workload/operation-space.cpp
    src/compound-config/compound-config.cpp
    )
set (SOURCES_METRICS
    src/loop-analysis/tiling.cpp
    src/loop-analysis/nest-analysis.cpp
    src/pat/pat.cpp
    src/applications/metrics/main.cpp
    src/mapping/loop.cpp
    src/mapping/nest.cpp
    src/model/arithmetic.cpp
    src/model/buffer.cpp
    src/model/topology.cpp
    src/util/numeric.cpp
    src/util/map2d.cpp
    src/workload/problem-shape.cpp
    src/workload/workload.cpp
    src/workload/operation-space.cpp
    src/compound-config/compound-config.cpp
    )

add_executable(timeloop-mapper ${SOURCES_MAPPER})
add_executable(timeloop-model ${SOURCES_MODEL})
add_executable(timeloop-metrics ${SOURCES_METRICS})