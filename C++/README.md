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

# Set the project_name - there could be multiple projects in 1 CMakeLists.txt file
project(HelloWorld VERSION 1.0)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Add an executable target
add_executable(HelloWorld main.cpp)
# 1st arg is project_name and 2nd arg is source_file

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

<h3 style="color:#fc036b">*.cmake</h3>

> - <a style="color:#000000">Used as configurations and module files</a>
>     - <a style="color:#000000">project specific setting</a>
>     - <a style="color:#000000">functions reused across multiple CMake projects or modules</a>
>     - <a style="color:#000000">find and configure 3rd party libs</a>
>        - <a style="color:#000000">ex: findXYZ.cmake might define how to locate and use a lib named XYZ setting necessary variables linke include directories and linkerflags</a>

<h3 style="color:#fc036b">include(...)</h3>

> - <a style="color:#000000">include command is used to include another CMake script/module</a>

<h3 style="color:#fc036b">function(func_name ARG1 ARG2) ... endfunction()</h3>

```cpp
function(FIND_AND_SET_CLANG17)
    find_program(CLANGPP_17 clang++-17)
    find_program(CLANG_17 clang-17)

    if(NOT CLANGPP_17 OR NOT CLANG_17)
        message(FATAL_ERROR "Clang-17 not found. Make sure you have clang-17 and clang++-17 installed and in your PATH")
    endif()

    set(CMAKE_CXX_COMPILER "${CLANGPP_17}" PARENT_SCOPE)
    set(CMAKE_C_COMPILER "${CLANG_17}" PARENT_SCOPE)
endfunction()

# in another file
# Include the CMake file where the function is defined
include(path/to/the/file_with_function.cmake)

# Call the function to find and set Clang 17
FIND_AND_SET_CLANG17()
```

<h3 style="color:#fc036b">Setting Variables</h3>

```cpp
set(MY_VARIABLE "Hello, World!")
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

```cpp
// Both below chunks of code function the same

// without namespace
#include <iostream>

int main() {
  std::cout << "Hello World!";
  return 0;
}

// with namespace
#include <iostream>
using namespace std;

int main() {
  cout << "Hello World!";
  return 0;
}
```

<h3 style="color:#fc036b">Variables</h3>

```cpp
int potatoes = 40;           // Variables can be defined like this
int tomatoes{80};            // or like this (this is a more modern c++ way

int myNum = 5;               // Integer (whole number without decimals)
double myFloatNum = 5.99;    // Floating point number (with decimals)
char myLetter = 'D';         // Character
string myText = "Hello";     // String (text)
bool myBoolean = true;       // Boolean (true or false)

int myAge = 25;
cout << "I am " << myAge << " years old.";

const int myNum = 15;  // myNum will always be 15
myNum = 10;  // error: assignment of read-only variable 'myNum'

float f1 = 35e3;    // indicates 10 to the power of 3
double d1 = 12E4;

// Include the string library
#include <string>

// Create a string variable
string greeting = "Hello";

// Output string value
cout << greeting;

string myString = "Hello";
cout << myString[0];    // Outputs H
cout << myString[myString.length() - 1];    // Outputs o
myString[0] = 'J';
cout << myString;    // Outputs Jello instead of Hello
```

<h3 style="color:#fc036b">Input</h3>

```cpp
#include <iostream>
using namespace std;

int main() {
  int x;
  cout << "Type a number: "; // Type a number and press enter
  cin >> x; // Get user input from the keyboard
  cout << "Your number is: " << x;
  return 0;
}

string fullName;
cout << "Type your full name: ";
getline (cin, fullName);    // used for reading input w/ an entire line with space
cout << "Your name is: " << fullName;

// Type your full name: Kan Kab
// Your name is: Kan Kab
```

<h3 style="color:#fc036b">Math</h3>

```cpp
// Include the cmath library
#include <cmath>

cout << min(5, 10);    // doesn't need the math library

cout << sqrt(64);
cout << round(2.6);
cout << log(2);

cout << (10 > 9); // returns 1 (true), because 10 is higher than 9

int myNumbers[5] = {10, 20, 30, 40, 50};
for (int i : myNumbers) {
  cout << i << "\n";
}

int myNumbers[5] = {10, 20, 30, 40, 50};
cout << sizeof(myNumbers);    // outputs: 20

// A vector with 3 elements
vector<string> cars = {"Volvo", "BMW", "Ford"};

// Adding another element to the vector
cars.push_back("Tesla");

string letters[2][4] = {
  { "A", "B", "C", "D" },
  { "E", "F", "G", "H" }
};
```

<h3 style="color:#fc036b">Structs</h3>

```cpp
// Create a structure variable called myStructure
struct {
  int myNum;
  string myString;
} myStructure;

// Assign values to members of myStructure
myStructure.myNum = 1;
myStructure.myString = "Hello World!";

// Print members of myStructure
cout << myStructure.myNum << "\n";
cout << myStructure.myString << "\n";

// Declare a structure named "car"
struct car {
  string brand;
  string model;
  int year;
};

int main() {
  // Create a car structure and store it in myCar1;
  car myCar1;
  myCar1.brand = "BMW";
  myCar1.model = "X5";
  myCar1.year = 1999;

  // Create another car structure and store it in myCar2;
  car myCar2;
  myCar2.brand = "Ford";
  myCar2.model = "Mustang";
  myCar2.year = 1969;
 
  // Print the structure members
  cout << myCar1.brand << " " << myCar1.model << " " << myCar1.year << "\n";
  cout << myCar2.brand << " " << myCar2.model << " " << myCar2.year << "\n";
 
  return 0;
}
```

<h3 style="color:#fc036b">References</h3>

```cpp
string food = "Pizza";

cout << &food; // Outputs 0x6dfed4

string food = "Pizza";
string &meal = food;

cout << food << "\n";  // Outputs Pizza
cout << meal << "\n";  // Outputs Pizza

string food = "Pizza";  // Variable declaration
string* ptr = &food;    // Pointer declaration

// Reference: Output the memory address of food with the pointer (0x6dfed4)
cout << ptr << "\n";

// Dereference: Output the value of food with the pointer (Pizza)
cout << *ptr << "\n";
```

<h3 style="color:#fc036b">Functions</h3>

```cpp
// pass by reference
#include <iostream>
using namespace std;

void swapNums(int &x, int &y) {
  int z = x;
  x = y;
  y = z;
}

int main() {
  int firstNum = 10;
  int secondNum = 20;

  cout << "Before swap: " << "\n";
  cout << firstNum << secondNum << "\n";    \\ 1020

  swapNums(firstNum, secondNum);

  cout << "After swap: " << "\n";
  cout << firstNum << secondNum << "\n";    \\ 2010

  return 0;
}
```
