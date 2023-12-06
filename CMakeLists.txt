cmake_minimum_required(VERSION 3.20)
project(spblas-project)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_CXX_FLAGS "-O3 -march=native")

include(FetchContent)
FetchContent_Declare(
  spblas
  GIT_REPOSITORY https://github.com/SparseBLAS/spblas-reference.git
  GIT_TAG main)
FetchContent_MakeAvailable(spblas)

add_subdirectory(src)
