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
