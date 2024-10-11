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

> - <a style="color:#000000">Numbers</a>

```go
var x int = 42
f := float64(x)

fmt.Printf("x is of type: %s\n", reflect.TypeOf(x))
// Output: x is of type: int

fmt.Printf("f is of type: %s\n", reflect.TypeOf(f))
// Output: f is of type: float64
```

> - <a style="color:#000000">Strings</a>

```go
import "strings"

strings.ToUpper("test") // => "TEST"
```

> - <a style="color:#000000">ifs</a>

```go
num := 7
// no brackets for if statement
if v := 2 * num; v > 10 {
    fmt.Println(v)
} else if v == num {
    fmt.Println("equal 0?")
} else {
    fmt.Println(num)
}
// Output: 14
```
