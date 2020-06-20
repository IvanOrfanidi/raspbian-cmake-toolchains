# Version CMake
cmake_minimum_required(VERSION 3.10)

# Project name
project(main C CXX)

# Add CMake scripts (includes) into scope
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/raspbian-cmake-toolchains")

# Set standart and optimization level
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O0")

# Source files
file(GLOB_RECURSE SOURCES
  src/*.cpp
  src/*.h)

# Compiler flags
set(CMAKE_C_FLAGS_INIT "${CMAKE_C_FLAGS_INIT} -Wl,-rpath-link")
set(CMAKE_CXX_FLAGS_INIT "${CMAKE_CXX_FLAGS_INIT} -Wl,-rpath-link")

set(COMPILER_FLAGS "-Wall")
add_definitions(${COMPILER_FLAGS})

# Compiling target
add_executable(${PROJECT_NAME} ${SOURCES})

# Link target
target_link_libraries(${PROJECT_NAME})
