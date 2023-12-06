# spblas-example-project
This is an example project demonstrating how to use [spblas](https://github.com/SparseBLAS/spblas-reference) as a dependency.

You should be able to include spblas as a dependency using CMake.  It should automatically pull its required dependencies
(mdspan and, if your compiler is older, range-v3), which will also be linked if you link your binaries with `spblas`.

## Primary CMakeLists.txt
Use `FetchContent` to fetch the most recent version of `spblas`.  `spblas` will be imported as a library, which you can
then use as a dependency.

```cmake
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
```

## Linking Binaries with `spblas`
All you should need to do from here is use `target_link_libraries` to link your binaries
with `spblas.`

```cmake
function(add_example example_name)
  add_executable(${example_name} ${example_name}.cpp)
  target_link_libraries(${example_name} spblas)
endfunction()

add_example(simple_spmv)
```
