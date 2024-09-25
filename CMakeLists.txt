# Minimum CMake version
cmake_minimum_required(VERSION 3.10)

# Project name and version
project(MyOpenGLProject VERSION 1.0)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Find OpenGL package
find_package(OpenGL REQUIRED)

# Add the source files
set(SOURCES
    src/main.cpp
    lib/glad.c   # Ensure this path is correct relative to your project structure
)
include(FetchContent)
FetchContent_Declare(
  glfw
  GIT_REPOSITORY https://github.com/glfw/glfw.git
  GIT_TAG 3.3.2  # Use the latest stable version tag
)
FetchContent_MakeAvailable(glfw)

# Add executable for your project
add_executable(MyOpenGLProject ${SOURCES})

# Add glad as a library
add_library(glad STATIC lib/glad.c)   # Ensure glad.c is in the lib/ folder

# Include directories for glad
target_include_directories(glad PUBLIC include)  # Include path for glad.h

# Find and link GLFW
#find_package(GLFW3 REQUIRED)

# Link libraries to your executable
target_link_libraries(MyOpenGLProject
    glad
    ${OPENGL_LIBRARIES}
    glfw
)
