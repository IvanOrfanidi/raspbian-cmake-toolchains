# Version CMake
cmake_minimum_required(VERSION 3.10)

# Project name
project(main C CXX)

# Add CMake scripts (includes) into scope
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/raspbian-cmake-toolchains")

# Set standart and optimization level
set(CMAKE_CXX_STANDARD 17)

# Source files
file(GLOB_RECURSE SOURCES
    src/*.cpp
    src/*.h
)

# Compiler flags
set(CMAKE_C_FLAGS_INIT "${CMAKE_C_FLAGS_INIT} -Wl,-rpath-link")
set(CMAKE_CXX_FLAGS_INIT "${CMAKE_CXX_FLAGS_INIT} -Wl,-rpath-link")

set(COMPILER_FLAGS
    "-Wall"
    "-Werror"
)
add_definitions(${COMPILER_FLAGS})

# Set build type
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif(NOT CMAKE_BUILD_TYPE)

# Compiling target
add_executable(${PROJECT_NAME} ${SOURCES})

# Link target
target_link_libraries(${PROJECT_NAME})
