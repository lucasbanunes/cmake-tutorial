# Set the minimum required version of CMake to be 3.10
cmake_minimum_required(VERSION 3.10)

# Creates a project named Tutorial with version 1.0
# https://cmake.org/cmake/help/latest/command/project.html#command:project
project(Tutorial VERSION 1.0)


# Sets the C++ standard to C++11 using
# the CMAKE_CXX_STANDARD variable to 11
# and the variable CMAKE_CXX_STANDARD_REQUIRED makes
# the C++11 standard a requirement
# https://cmake.org/cmake/help/latest/command/set.html
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Use configure_file to configure and copy TutorialConfig.h.in to
# TutorialConfig.h
# https://cmake.org/cmake/help/latest/command/configure_file.html
configure_file(TutorialConfig.h.in TutorialConfig.h)

# Add an executable called Tutorial to the project
# This means that tutorial.cxx will be compiled into an executable binary
add_executable(Tutorial tutorial.cxx)

# Use target_include_directories to include ${PROJECT_BINARY_DIR}
# in the Tutorial target
# This means that when Tutorial is compiled, it will have access to the
# header files in ${PROJECT_BINARY_DIR}
# https://cmake.org/cmake/help/latest/command/target_include_directories.html
target_include_directories(Tutorial PUBLIC
                           "${PROJECT_BINARY_DIR}"
                           )
