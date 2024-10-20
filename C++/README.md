<h1 style="color:#fc036b">CMake</h1>

<h3 style="color:#fc036b">Intro</h3>

> - <a style="color:#000000"> It is used to manage the build process of software using a simple configuration file, called CMakeLists.txt</a>
>
> - <a style="color:#000000">It generates platform-specific build files (like Makefiles for Unix/Linux or Visual Studio project files for Windows) based on the configuration you provide</a>

<h3 style="color:#fc036b">Pros</h3>

> - <a style="color:#000000">CMake allows you to write build scripts once & use it across different OS w/o modification</a>
>
> - <a style="color:#000000"><strong>Out-of-source-builds:</strong> You can build your software in a separate directory from the source code -> keeps source tree clean & organized from artifact</a>
>
> - <a style="color:#000000"><strong>Dependency Management:</strong> It can help manage complex project dependencies, making it easier to integrate 3rd party libraries</a>
>
> - <a style="color:#000000"><strong>Modular:</strong> It allows you to break large projects into smaller components that can be developed, built, and tested independently</a>
>
> - <a style="color:#000000"><strong>Customization & Flexibility:</strong> You can define custom targets, add pre-/post-build commands, and configure build options</a>

<h3 style="color:#fc036b">Workflow</h3>

> - <a style="color:#000000">File structure</a>

```
/HelloWorldProject
| - CMakeLists.txt
| - main.cpp
| _ build/
    | - CMakeCache.txt
    | - Makefile
    | _ CMakeFiles/
        | _ (various files)
    | - HelloWorld (executable)
    | _ main.o
```

> - <a style="color:#000000">main.cpp</a>

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, World!" << std::endl;
    return 0;
}
```

> - <a style="color:#000000">CMakeLists.txt</a>

```
# below is always the first line: cmake should be installed and must have a minimum version of 3.10
cmake_minimum_required(VERSION 3.10)

# Set the project name - there could be multiple projects in 1 CMakeLists.txt file
project(HelloWorld VERSION 1.0)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Add an executable target
add_executable(HelloWorld main.cpp)

```

> - <a style="color:#000000">In Bash terminal, execute following: </a>

```
> mkdir build    // Creating a build directory in the root of the project repo
> cd build

> cmake ..       // '..' refers to the parent directory where CMakeLists.txt is located
                 // cmake command generates Makefile (or .sln in Windows), CMakeCache.txt, CMakeFiles directory with various configuration files
> make           // maybe creates lib files *.a, *.so -> unix or *.dll -> windows | .o or .obj compiled version of source code files in CMakeFiles dir
                 // maybe generates log files
> ./HelloWorld

Output: "Hello, World!"

```


<h1 style="color:#fc036b">C++</h1>

<h3 style="color:#fc036b">Intro</h3>

> - <a style="color:#000000">For applications that require speed and/or access to some low-level features. It supports procedural, object-oriented, functional and generic programming</a>

```cpp
#include "hello_world.h"

using namespace std;

namespace hello_world
{

string hello()
{
    return "Hello, World!";
}

}
```

```cpp
// This is an include guard.
#if !defined(HELLO_WORLD_H)
#define HELLO_WORLD_H

// Include the string header so that we have access to 'std::string'
#include <string>

// Declare a namespace for the function(s) we are exporting.
namespace hello_world {

// Declare the 'hello()' function, which takes no arguments and returns a
// 'std::string'. The function itself is defined in the hello_world.cpp source
// file. Because it is inside of the 'hello_world' namespace, it's full name is
// 'hello_world::hello()'.
std::string hello();

}  // namespace hello_world

#endif
```

> - <a>In C++, files with a .h extension are header files. Header files typically contain declarations for functions, classes, and variables. This allows you to define the interface of your code separately from its implementation.</a>
>
> - <a>Guard Against Multiple Inclusions: Header files often use include guards (#ifndef, #define, #endif) or #pragma once to prevent multiple inclusions of the same header file in a single compilation unit, which can cause redefinition errors.</a>
>
> - <a>Code reusability, Separation of Interface and Implementation, Organizes code into modules</a>
