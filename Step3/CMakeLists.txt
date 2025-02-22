cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(Tutorial VERSION 1.0)

# This create a library that will be used to propagate the C++ standard
# to the compiler flags
# when you link this library to a target, the compiler flags will be set
# automatically to match the C++ standard used to compile this library
# If you go inside the other CMakeLists, they will link to this library too
add_library(tutorial_compiler_flags INTERFACE)
target_compile_features(tutorial_compiler_flags INTERFACE cxx_std_11)

# Because of the code on the top we don't need to do this anymore
# specify the C++ standard
# set(CMAKE_CXX_STANDARD 11)
# set(CMAKE_CXX_STANDARD_REQUIRED True)

# configure a header file to pass some of the CMake settings
# to the source code
configure_file(TutorialConfig.h.in TutorialConfig.h)

# add the MathFunctions library
add_subdirectory(MathFunctions)
# Since MathFunctions now lists that whoever uses it needs these includes
# with the interface keyword, we don't need to do it here
# list(APPEND EXTRA_INCLUDES "${PROJECT_SOURCE_DIR}/MathFunctions")

# add the executable
add_executable(Tutorial tutorial.cxx)

# links the compiler flags to the executable
target_link_libraries(Tutorial PUBLIC MathFunctions tutorial_compiler_flags)

# add the binary tree to the search path for include files
# so that we will find TutorialConfig.h
# Since MathFunctions now lists that it needs these includes, we don't need to do it here
target_include_directories(Tutorial PUBLIC
                           "${PROJECT_BINARY_DIR}"
                        #    ${EXTRA_INCLUDES}
                           )
