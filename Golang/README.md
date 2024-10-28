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
// Function arguments are the concrete values passed to the function
// Function parameters are the names defined in the function's signature

package greeting

// Hello is a public function.
func Hello (name string) string {
    return hi(name)
}

// hi is a private function.
func hi (name string) string {
    return "hi " + name
}

// Multiple parameters, multiple return values
func SumAndMultiply(a, b int) (int, int) {
    return a+b, a*b
}
// Called like this:
aplusb, atimesb := SumAndMultiply(a, b)

/* As well as parameters, return values can optionally be named. If named return values are used, a return statement without arguments will return those values. This is known as a 'naked' return. */
func SumAndMultiplyThenMinus(a, b, c int) (sum, mult int) {
    sum, mult = a+b, a*b
    sum -= c
    mult -= c
    return
}

// Pass by Value vs. Pass by Reference
val := 2
func MultiplyByTwo(v int) int {
    v = v * 2
    return v
}
newVal := MultiplyByTwo(val)
// newval is 4, val is still 2 because only a copy of its value was passed into the function

// all arguments (except slices and maps) are passed by value in Go, i.e. a copy is made of the value or data provided to the function.
// If you want to change the data in the function, then you should use pointers as argument
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


func ScaleRecipe(v1 []float64, v2 int) ([]float64) {
    res := make([]float64, len(v1))
    for index, _ := range v1 {
        res[index] = (v1[index]/2.0) * float64(v2)
    }
    return res
}
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

> - <a style="color:#000000">Structs</a>

```go
type Shape struct {
    name string
    size int
}

s := Shape {
    name: "Square",
    size: 25,
}

// Update the name and the size
s.name = "Circle"
s.size = 35
fmt.Printf("name: %s size: %d\n", s.name, s.size)
// Output: name: Circle size: 35


func NewShape(name string) Shape {
	return Shape{
		name: name,
		size: 100, //default-value for size is 100
	}
}

NewShape("Triangle")
// => Shape { name: "Triangle", size: 100 }

// Another way of creating a new instance of a struct is by using the new built-in
s := new(Shape) // s will be of type *Shape (pointer to shape)
fmt.Printf("name: %s size: %d\n", s.name, s.size)
// Output: name:  size: 0
```

> - <a style="color:#000000">For...Loop</a>

```go
// FixBirdCountLog returns the bird counts after correcting
// the bird counts for alternate days.
func FixBirdCountLog(birdsPerDay []int) []int {
    for i := 0; i<len(birdsPerDay); i+=2 {
        birdsPerDay[i] += 1;
    }
    return birdsPerDay;
	//panic("Please implement the FixBirdCountLog() function")
}

func Quantities(layers []string) (int, float64) {
    n := 0
    s := 0
    // index is the index where we are
    // element is the element from someSlice for where we are
    for _, element := range layers {
        if element == "noodles" {
            n += 1
        }
        if element == "sauce" {
            s += 1
        }
        
    }
    return n*50, 0.2*float64(s)
}
```

> - <a style="color:#000000">For...is also Go's while loop</a>

```go
// YearsBeforeDesiredBalance calculates the minimum number of years required to reach the desired balance.
func YearsBeforeDesiredBalance(balance, targetBalance float64) int {
	myBalance := balance
    years := 0
    for myBalance < targetBalance {
        myBalance = AnnualBalanceUpdate(myBalance)
        years += 1
    }
    return years
}
```

> - <a style="color:#000000">Randomizing</a>

```go
import "math/rand"

n := rand.Intn(100) // n is a random int, 0 <= n < 100

x := []string{"a", "b", "c", "d", "e"}
// shuffling the slice put its elements into a random order
rand.Shuffle(len(x), func(i, j int) {
	x[i], x[j] = x[j], x[i]
})
```

> - <a style="color:#000000">Maps</a>

```go
  // declaration with make function
  foo := make(map[string]int)
  // Add a value in a map with the `=` operator:
  foo["bar"] = 42
  // Here we update the element of `bar`
  foo["bar"] = 73
  // To retrieve a map value, you can use
  baz := foo["bar"]
  // To delete an item from a map, you can use
  delete(foo, "bar")

  value, exists := foo["baz"]
  // If the key "baz" does not exist,
  // value: 0; exists: false
```
