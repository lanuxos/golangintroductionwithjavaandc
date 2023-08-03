# A Tour of Go
[a tour of go](https://go-tour-th.appspot.com/tour/welcome/1)

# Go offline
`go install golang.org/x/website/tour@latest`

# Packages, variables and functions
- package
- import
- exported names [Capital letter for public variables]
- functions 
    - with/without argument
    - multiple results
    - named return value [naked return]
- variables
    - var
    `var a, b, c string`
    - variables with initializers
    ```
    var i, j int = 1, 2
    var k = 3
    var (
        a string
        b int = 1
        c bool
    )
    ```
    - short variable declarations [only inside functions]
    `abc := 123`
    - basic types
        - bool
        - string
        - int
        - int8
        - int16
        - int32
        - int64
        - uint
        - uint8
        - uint16
        - uint32
        - uint64
        - uintptr
        - byte // alias for uint8
        - rune // alias for int32
        - float32
        - float64
        - complex64
        - complex128
    - zero values [0 false ""]
    - type conversions [T(v)]
    ```
    var i int = 1
    var j float64 = float64(i)
    var k uint = uint(j)
    ```
    - type inference
    ```
    var a int
    b := a // b is an int too
    c := 3.14
    d := c // d is float64
    ```
    - constants [const] // could not assign with := syntax
    - numeric constants
# Flow control statements [for, if, else, switch, defer]
- for 
    - init; condition; closed {}
    - for ; condition; {}
    - for condition {} // for is Go's while
    - for {} // forever
- if
    - if condition {}
    - if short_statement; condition {} // if with a short statement
    - if short_statement; condition {} else {}
- switch
    - switch evaluation order
    ```
    switch i {
        case a:
            // statement when i=a
        case b:
            // statement when i=b
        default:
            // statement when above cases did not run
    }
    ```
    - switch with no condition
    ```
    switch { // means the case condition is true
        case a:
            // statement when a is true
        case b:
            // statement when b is true
        default:
            // statement when above cases did not run
    }
    ```
- defer [stacking/last-in-first-out run after super/parent function return]
# More types [structs, slices, maps]
- pointers [variables' memory address]
```
i := 123
j = &i
*j = 321 // i = 321 too
```
- structs [collection of fields]
- struct fields
```
type MyStruct {
    X int
    Y string
}
z := MyStruct{123, "abc"}
z.X
z.Y = "efg"
```
- pointers to structs
```
type MyStruct {
    X int
    Y string
}

p := &v
p.X = 321 // MyStruct.X changed to 321 instead of 123 above
```
- struct literals
```
type MyStruct {
    X, Y int
}
var (
    v1 = MyStruct{1, 2} // v1 has type MyStruct
    v2 = MyStruct{X: 1} // Y:0
    v1 = MyStruct{} // X: 0, Y: 0
    p = &MyStruct(1, 2) // has type *MyStruct
)
```
- arrays [n]T
```
var a [3]int
a[0] = 1 // [1, nil, nil]
a[1] = 2 // [1, 2, nil]
a[2] = 3 // [1, 2, 3]
```
- slices []T
```
var a [10]int{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
var s []int = a[1:5] // [1, 2, 3, 4]
```
- slices are like references to arrays
- slice literals
```
var s []bool{true, false, true}
var ss []struct {
    i int
    b bool
}{
    {1, true},
    {2, false},
    {3, true}
}
```
- slice defaults
```
var a [10]int
// below slice all the same size of array member
a[0:10]
a[:10]
a[0:]
a[:]
```
- slice length and capacity
- nil slices [when length and capacity equal zero]
- creating a slice with make
```
s := make([]int, 5) // len(s) = 5
ss := make([]int, 0, 5) // len(ss) = 0, cap(ss) = 5
```
- slices of slices
```
ss := [][]int{
    []int{1,2,3},
    []int{4,5,6},
    []int{7,8,9},
}
```
- appending to a slice
```
var s []int // []
s = append(s, 0) // [0]
s = append(s, 1, 2, 3) // [0, 1, 2, 3]
```
- range
```
package main
import "fmt"
var s = []int{1,2,3,4,5}
func main(){
    // there are two return from range, index and value
    for i, v := range a {
        fmt.Printf("index: %d, has value: %d", i, v)
    }
}
```
- range continued
```
package main
import "fmt"
var s = []int{1,2,3,4,5}
func main(){
    // use underscore(_) to dismiss the value
    for i, _ := range a {
        fmt.Printf("index: %d, has value: %d", i, v)
    }
    // use underscore(_) to dismiss the index
    for _, i := range a {
        fmt.Printf("index: %d, has value: %d", i, v)
    }
}
```
- maps [key, value]
```
var m map[string]string
m["key1"] = "value1" // map[key1: value1]
```
- map literals
```
type MyStruct {
    Lat, Long float64
}
var m = map[string]MyStruct{
    "My House": MyStruct{
        123.456, 789.0
    },
    "My Office": MyStruct{
        654.321, 098.7
    }
}
```
- map literals continued
```
type MyStruct {
    Lat, Long float64
}
var m = map[string]MyStruct{
    "My House": {123.456, 789.0},
    "My Office": {654.321, 098.7}
}
```
- mutating maps
```
m[key] = element
element = m[key]
delete(m, key)
element, ok = m[key] // true, false
```
- function values // use function as other function argument
- function closures // 
# Methods and interfaces
- func receiver_name_and_type method_name return_type {}
```
type MyStruct struct {
	X, Y float64
}
func (s MyStruct) Met() float64 {
    // s is receiver which has struct type
    // Met() is method name
    // and return float64
	return s.X*s.Y
}
func main() {
	v := MyStruct{3, 4}
	fmt.Println(v.Met())
}
```
- methods are functions
```
// method is a function that has receiver
type MyStruct struct {
    X, Y float64
}
func Met(s MyStruct) float64 {
    return s.X*s.Y
}
func main() {
    v := MyStruct{3,4}
    fmt.Println(Met(v))
}
```
- pointer receivers
- pointer and functions
- methods and pointer indirection
- value or pointer receivers
- interfaces [declaring method license set]
- interfaces are implemented implicitly
- interface values
- interface values with nil underlying values
- nil interface values
- the empty interface
- type assertions
- type switches
- Stringer
- Error
- Reader
- Image
# Generics
- types parameters
    - constraint [comparable]
- generic types
# Concurrency
- goroutines
```
go f(x, y, z) // run in current goroutine
f(x, y, z) // run in another goroutine
```
- channels
```
ch := make(chan int)
ch <- v     // send v to channel ch
v := <-ch   // receive from ch, and 
            // assign value to v

// sum slice member with 2 goroutines
func sum(s []int, c chan int) {
	sum := 0
	for _, v := range s {
		sum += v
	}
	c <- sum // send sum to c
}
func main() {
	s := []int{7, 2, 8, -9, 4, 0}

	c := make(chan int)
	go sum(s[:len(s)/2], c)
	go sum(s[len(s)/2:], c)
	x, y := <-c, <-c // receive from c

	fmt.Println(x, y, x+y)
}
```
- buffered channels
`ch := make(chan int, 100)  // `
- Range and Close
- Select
- default selection
- sync.Mutex [mutual exclusion]