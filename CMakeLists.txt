cmake_minimum_required (VERSION 3.9)
MESSAGE(STATUS "CMAKE_ROOT: " ${CMAKE_ROOT})

# Project name
project(Parser-SPEF)

include(CTest)

# Turn on the verbose
set(CMAKE_VERBOSE_MAKEFILE ON)

# CXX target properties
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
#set(USE_WERROR ON)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -O2")
message(STATUS "CMAKE_BUILD_TYPE: " ${CMAKE_BUILD_TYPE})
message(STATUS "CMAKE_CXX_COMPILER: " ${CMAKE_CXX_COMPILER})
message(STATUS "CMAKE_CXX_FLAGS: " ${CMAKE_CXX_FLAGS})
message(STATUS "CMAKE_EXE_LINKER_FLAGS: " ${CMAKE_EXE_LINKER_FLAGS})


# add the binary tree to the search path for include files
include_directories(${PROJECT_SOURCE_DIR})
include_directories(parser-spef)
include_directories(doctest)


# -----------------------------------------------------------------------------
# Example program 
# -----------------------------------------------------------------------------
message(STATUS "Building examples ...")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/example)

message(STATUS "EXAMPLE_CXX_FLAGS: " ${EXAMPLE_CXX_FLAGS})
message(STATUS "EXAMPLE_EXE_LINKER_FLAGS: " ${EXAMPLE_EXE_LINKER_FLAGS})

add_executable(simple example/simple.cpp)

#target_compile_options(simple PRIVATE "-pg")
#target_link_libraries(simple stdc++fs "-pg")
target_link_libraries(simple stdc++fs)

# -----------------------------------------------------------------------------
# Unittest
# -----------------------------------------------------------------------------
enable_testing()

message(STATUS "Building unit tests ...")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/unittest)

add_executable(parser-spef unittest/parser-spef.cpp)
target_link_libraries(parser-spef stdc++fs)

add_executable(benchmark unittest/benchmark.cpp)
target_link_libraries(benchmark stdc++fs)


add_test(HeaderFix ${PROJECT_SOURCE_DIR}/unittest/parser-spef -tc=Header.Fix)
add_test(HeaderRandom ${PROJECT_SOURCE_DIR}/unittest/parser-spef -tc=Header.Random)
add_test(NameMap ${PROJECT_SOURCE_DIR}/unittest/parser-spef -tc=NameMap)
add_test(Port ${PROJECT_SOURCE_DIR}/unittest/parser-spef -tc=Port)
add_test(Net ${PROJECT_SOURCE_DIR}/unittest/parser-spef -tc=Net)
add_test(NameExpansion ${PROJECT_SOURCE_DIR}/unittest/parser-spef -tc=NAME_EXPANSION)
add_test(Benchmark ${PROJECT_SOURCE_DIR}/unittest/benchmark)


