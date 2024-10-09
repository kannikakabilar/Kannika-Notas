<h1 style="color:#0ed5eb">Go</h1>

<h3 style="color:#0ed5eb">Intro</h3>

> - <a style="color:#000000">Go is a statically typed, compiled programming language.</a>
> <br> 
>
> - <a style="color:#000000">Packages in Go</a>
> <br> Go applications are organized in packages. A package is a collection of source files located in the same directory. All source files in a directory must share the same package name - name of the last directory in the import path. For ex: files in the "math/rand" => package rand
>
> - When a package is imported, only entities (functions, types, variables, constants) whose names start with a capital letter can be used / accessed. The recommended style of naming in Go is that identifiers will be named using camelCase, except for those meant to be accessible across packages which should be PascalCase.
>
> - <a style="color:#000000">Variables</a>
> <br> All variables must have a defined type at compile-time

```go
var explicit int // Explicitly typed

count := 1 // Implicitly typed as int
count = 2  // Update to new value

count = false // This throws a compiler error due to assigning a non `int` type

const Age = 25 // Defines a numeric constant 'Age' with the value of 25 and its value cannot be changed
```

> - <a style="color:#000000">Functions</a>

```go
package greeting

// Hello is a public function.
func Hello (name string) string {
    return hi(name)
}

// hi is a private function.
func hi (name string) string {
    return "hi " + name
}
```
