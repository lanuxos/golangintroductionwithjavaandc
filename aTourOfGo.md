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
- pointers
- structs
- struct fields
- pointers to structs
- struct literals
- arrays
- slices
- slices are like references to arrays
- slice literals
- slice defaults
- slice length and capacity
- nil slices
- creating a slice with make
- slices of slices
- appending to a slice
- range
- range continued
- maps
- map literals
- map literals continued
- mutating maps
- function values
- function closures
# Methods and interfaces
- 
# Generics
- 
# Concurrency
- 