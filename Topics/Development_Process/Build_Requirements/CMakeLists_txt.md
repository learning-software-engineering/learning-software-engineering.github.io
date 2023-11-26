# **Learning CMakeLists.txt**

## Table of Contents
### [1. Brief Introduction to CMake](#brief-introduction-to-cmake)
### [2. What is CMakeLists.txt?](#what-is-cmakeliststxt)
### [3. Creating CMakeLists.txt](#creating-cmakeliststxt)
### [4. Other Notes](#other-notes)
### [5. References](#references)

---
## Brief Introduction to CMake

This article will help readers understand what `CMakeLists.txt` is, why it is used, and provide instructions on how to create a `CMakeLists.txt`. Before getting started, it is important to understand what is CMake. Note that it is presumed that the reader should have the very basic knowledge of C++, Make, and MakeFile.

Unlike Make, which is a build system that drives the compiler and other build tools to build your code, CMake (or Cross-platform Make) is a "generator" of build systems that can be used for general purpose build. It is much more high-level that it can generate a low-level build script in Ninja or Make or many other build systems, and then you run it.

The key feature of CMake is that it supports the cross-platform discovery of system libraries, and automatic discovery and configuration of the toolchain, which is much easier to use than Make.

To install CMake, check their [document](#https://cmake.org/download/) on how to download and install on Unix/Linux or Windows platform.


## What is CMakeLists.txt?

When CMake processes a project, the entry point is a source file called `CMakeLists.txt` in the top level of the source directory.

`CMakeLists.txt` file is the CMake configuration file, which contains a set of directives and instructions describing the project's source files and taargets (executable, library, or both) that will be used to build the program. It determines everything for the building process, from which source files to compile, to which options to choose for the libraries and to present to the users.

## Creating CMakeLists.txt

### CMake Language
`CMakeLists.txt` is written in [CMake Language](#https://cmake.org/cmake/help/latest/manual/cmake-language.7.html#manual:cmake-language(7)), which consists of comments, [commands](#https://cmake.org/cmake/help/latest/manual/cmake-commands.7.html#manual:cmake-commands(7)), and [variables](#https://cmake.org/cmake/help/latest/manual/cmake-variables.7.html#manual:cmake-variables(7)). 

* **Comments** start with `#`
  ```
  # This is a comment
  ```
* **Commands** start with command names and a list of whitespace-separated arguments (case-sensitive).
  ```
  find_package(LIBIGL REQUIRED QUIET)
  ```
* **Variables** are case-sensitive with only alphanumeric characters and underscores. 
  A number of useful variables are automatically defined by CMake (e.g `CMAKE_CURRENT_SOURCE_DIR`, `PROJECT_NAME`). 
  Use *set* command to set variable names, and *${variable_name}* to reference a varible in command arguments. 
  ```
  set(Foo a b c)    # Value of Foo is "a;b;c"

  command(${Foo})   # Foo is replaced by a;b;c 
                    # and expands to 3 arguments
  ```

It also provides the basic **Flow Control** - Conditional statements, Looping constructs, and Procedure definitions. Here are the examples:

* **Conditional statements (e.g [if](#https://cmake.org/cmake/help/latest/command/if.html#command:if))**
    ```
    if(<condition>)
    <commands>
    elseif(<condition>)     # optional block, can be repeated
    <commands>
    else()                  # optional block
    <commands>
    endif()
    ```
* **Looping Constructs (e.g [foreach](#https://cmake.org/cmake/help/latest/command/foreach.html#command:foreach), [while](#https://cmake.org/cmake/help/latest/command/while.html#command:while))**
    ```
    foreach(<variable>                  # <variable> to be referenced
            <list of variables>)        # <list of variables> to replace ${variable}
    command(${variable} <arguments>)    # ${variable} - current value from the list
    endforeach()

    while(<condition>)
    <commands>
    endwhile()
    ```
* **Procedure definitions (e.g [function](#https://cmake.org/cmake/help/latest/command/function.html#command:function), [macro](#https://cmake.org/cmake/help/latest/command/macro.html#command:macro))**
    ```
    function(<function_name> <parameters>)
    <commands>
    endfunction()

    macro(<macro_name> <parameters>)
    <commands>
    endmacro()
    ```

For more detailed knowledge of CMake Language, check the **highlighted links** above.

### Key Components and Concepts

A `CMakeLists.txt` typically consists of the following elements:

```
cmake_minimum_required(VERSION 3.10)

# Project name
project(MyProject)

# Add main.cpp file of the project root directory as a source file
set(SOURCE_FILES main.cpp)

# Add executable targets
add_executable(MyExecutable ${SOURCE_FILES})

```
 * **cmake_minimum_required**
    CMake version check: the minimum version of CMake that should be used to process the project.
    You can specify a range of versions (as a general rule, set the highest version you've tested with):
    ```
    cmake_minimum_required(VERSION 3.15...3.25)
    ```
 * **project**
    Create project with the name of the project that is given to the cmake command.
    Projects can have versions, descriptions and languages specified.
    ```
    project(MyProject
        VERSION
            1.0
        DESCRIPTION
            "A project"
        LANGUAGES
            CXX
    )
    ```
 * **add_executable** - add executable target named `MyExecutable` with source files listed in `SOURCE_FILES` variable

**Variables and Options** can be set in the `CMakeLists.txt` to control various aspects of the building process.
```
set(CMAKE_CXX_STANDARD 14)              # enables the c++14 standards
option(BUILD_TESTS "Build tests" ON)    # build options - whether to build tests
```

**Include your directories and headerfiles**
```
# Adds directories to the compiler's include path.
include_directories("${CMAKE_CURRENT_SOURCE_DIR}/include/")
```

**Include your source files**
Suppose this is your project structure:
```
project_root/
|-- CMakeLists.txt
|-- src/
|   |-- file1.cpp
|   |-- file2.cpp
|   |-- ...
|-- other_files/
|   |-- ...
|-- main.cpp

``` 
You can add the source files in the `src` directory by:
```
file(GLOB SRC_FILES "*.cpp")

# Create a library or executable target using the source files
add_library(my_library ${SRC_FILES})
target_link_libraries(MyExecutable my_library)
```


**External Libraries** can be located using `find_package`
```
# Appends the "cmake" directory to the module path
# CMake modules are used to find and configure external libraries.
set(CMAKE_MODULE_PATH 
    ${CMAKE_MODULE_PATH} 
    ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

find_package(PACKAGE_NAME)     # Locate the package with PACKAGE_NAME

if(PACKAGE_NAME_FOUND)
    target_link_libraries (
        MyExecutable <libaries>         # Links against it.
    )
endif()

# The if-condition can be omitted if you specify the "REQUIRED":
find_package(PACKAGE_NAME REQUIRED) 
```

## Other Notes

()

Here is a [cheatsheet](#https://cppcheatsheet.com/notes/cmake_basic.html) of other useful commands for building a `CMakelists.txt`.

## References

* [CLion - CMake Build System](#https://www.jetbrains.com/help/clion/cmakelists-txt-file.html)
* [CMake vs Make](#https://stackoverflow.com/questions/25789644/what-is-the-difference-between-using-a-makefile-and-cmake-to-compile-the-code)
* [CMake - Writing CMakeLists File](#https://cmake.org/cmake/help/book/mastering-cmake/chapter/Writing%20CMakeLists%20Files.html)
* [HSF - CMakeLists](#https://hsf-training.github.io/hsf-training-cmake-webpage/03-cmakelists/index.html)
