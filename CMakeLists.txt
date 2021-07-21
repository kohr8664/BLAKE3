cmake_minimum_required(VERSION 3.21.0)

project(blake3)

# Project source files
set(
    SRCS
    ./src/blake3.c
    ./src/blake3_dispatch.c
    ./src/blake3_portable.c
    ./src/blake3_avx2.c
    ./src/blake3_avx512.c
    ./src/blake3_sse2.c
    ./src/blake3_sse41.c
)

# Add the library to the building system
add_library(blake3 SHARED ${SRCS})

# Add the include folder
target_include_directories(blake3 PRIVATE "./include")

# Enable compiler optimizations
target_compile_options(blake3 PRIVATE -O3)

# Set specific compiler flags for some files
set_source_files_properties(
    ./src/blake3_avx2.c
    PROPERTIES COMPILE_FLAGS "-fPIC -mavx2"
)

set_source_files_properties(
    ./src/blake3_avx512.c
    PROPERTIES COMPILE_FLAGS "-fPIC -mavx512f -mavx512vl"
)

set_source_files_properties(
    ./src/blake3_sse2.c
    PROPERTIES COMPILE_FLAGS "-fPIC -msse2"
)

set_source_files_properties(
    ./src/blake3_sse41.c
    PROPERTIES COMPILE_FLAGS "-fPIC -msse4.1"
)
