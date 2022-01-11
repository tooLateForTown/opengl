# OpenGL Setup Notes for COMP 471 
## Purpose 
This document represents my notes on working with OpenGL.  It was created when I wa staking COMP 471 (Computer Graphics) course at Concordia University in Montreal in 2021.  

## Installing on XCode on M1 
I was able to get the GLEW [hello world](https://www.glfw.org/documentation.html) working.  I did this using [This youtube video](https://www.youtube.com/watch?v=MHlbNbWlrIM) and [this signing fix](https://stackoverflow.com/questions/61925299/trying-to-setup-xcode-with-opengl) for repairing the signing.  One important note is that the version of homebrew I am using writes to /opt/homebrew/Cellar instead of to /opt/... 


## Installing on CLion on M1.  
The following CMakeLists.txt seems to work:  
```
cmake_minimum_required(VERSION 3.21)
set(CMAKE_CXX_STANDARD 14)
project(firstopengl)

set(CMAKE_PREFIX_PATH /opt/homebrew/Cellar) # Brew

#OpenGL
find_package(OpenGL REQUIRED COMPONENTS OpenGL)
find_package(GLEW REQUIRED)
find_package(glfw3 REQUIRED)

# Eigen3 CMake setup
set(ENV{EIGEN3_ROOT} /Users/derek/sdk/eigen-3.4.0)
set(CMAKE_MODULE_PATH /Users/derek/sdk/eigen-3.4.0/cmake)
find_package(Eigen3 REQUIRED)
include_directories(${EIGEN3_INCLUDE_DIR})

#find_package(OpenGL REQUIRED)
#find_package(glfw3 3.3.6 REQUIRED)

#include_directories(/opt/homebrew/Cellar/glfw/3.3.6/include)

#link_directories(/opt/homebrew/Cellar/glfw/3.3.6/lib)

add_executable(firstopengl main.cpp)
#target_link_libraries(firstopengl glfw3 )
target_link_libraries(${PROJECT_NAME} OpenGL::GL GLEW::glew glfw)


```
This assumes you used brew to install GLFW and GLEW.
