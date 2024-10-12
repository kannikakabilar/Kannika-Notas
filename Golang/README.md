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

food := "taco"
fmt.Sprintf("Bring me a %s", food)
// Returns: Bring me a taco

number := 4.3242
fmt.Sprintf("%.2f", number)
// Returns: 4.32
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

> - <a style="color:#000000">Slices (Arrays)</a>
> <br> Slices in Go are based on arrays. Arrays have a fixed size. A slice, on the other hand, is a dynamically-sized, flexible view of the elements of an array.

```go
var empty []int                 // an empty slice
withData := []int{0,1,2,3,4,5}  // a slice pre-filled with some data

withData[1] = 5
x := withData[1] // x is now 5

newSlice := withData[2:4]
// => []int{2,3}
newSlice := withData[:2]
// => []int{0,1}
newSlice := withData[2:]
// => []int{2,3,4,5}
newSlice := withData[:]
// => []int{0,1,2,3,4,5}

a := []int{1, 3}
a = append(a, 4, 2)
// => []int{1,3,4,2}

nextSlice := []int{100,101,102}
newSlice  := append(withData, nextSlice...)
// => []int{0,1,2,3,4,5,100,101,102}
```

```go
package cards

// FavoriteCards returns a slice with the cards 2, 6 and 9 in that order.
func FavoriteCards() []int {
    res := []int{2, 6, 9}
    return res;
	//panic("Please implement the FavoriteCards function")
}

// GetItem retrieves an item from a slice at given position.
// If the index is out of range, we want it to return -1.
func GetItem(slice []int, index int) int {
    if(len(slice)>index && index>=0){
        return slice[index];
    }else{
        return -1;
    }
	//panic("Please implement the GetItem function")
}

// SetItem writes an item to a slice at given position overwriting an existing value.
// If the index is out of range the value needs to be appended.
func SetItem(slice []int, index, value int) []int {
    if(len(slice)>index && index>=0){
        slice[index] = value;
        return slice;
    }else{
        return append(slice, value);
    }
	//panic("Please implement the SetItem function")
}

// PrependItems adds an arbitrary number of values at the front of a slice.
func PrependItems(slice []int, values ...int) []int {
    return append(values, slice...);
	// panic("Please implement the PrependItems function")
}

// RemoveItem removes an item from a slice by modifying the existing slice.
func RemoveItem(slice []int, index int) []int {
    if(index<len(slice) && index>=0){
        res := slice[:index];
        return append(res, slice[index+1:]...);
    }else{
        return slice;
    }
	//panic("Please implement the RemoveItem function")
}
```

> - <a style="color:#000000">Switch...case</a>

```go
operatingSystem := "windows"

switch operatingSystem {
case "windows":
    // do something if the operating system is windows
case "linux":
    // do something if the operating system is linux
case "macos":
    // do something if the operating system is macos
default:
    // do something if the operating system is none of the above
}
```
