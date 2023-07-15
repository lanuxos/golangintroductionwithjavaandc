# ยินดีที่ได้รู้จัก Golang  ผ่านภาษาชีและจาวา
# golangintroductionwithjavaandc
# Golang introduction with Java and C

# Commands
```
go mod init MODULE_NAME // initial go.mod for dependency tracking
go mod tidy
go get <URL>
go mod edit -replace xxx=yyy
go build file_name.go
```
# Keywords [const, func, import, package, type, var, chan, interface, map, struct, break, case, continue, default, else, fallthrough, for, goto, if, range, return, select, switch, defer, go]
# Identifiers
- combine with unicode alphabet, unicode number, underscore
- Capital letter for public variable, lower case for private one
- 
# Packages
```
// one by one import package
import "fmt"
import "math/rand"

// import multiple packages
import (
    "fmt"
    "time"
)
func main(){
    fmt.Println("Now is: ", time.Now())
}

// change package's name
import (
    f "fmt"
    t "time"
)
func mani(){
    f.Println("Now is: ", t.Now())
}

// external packages reference
// before run the package, 
// must run "go mod tidy" first

// install package manually
// run command "go get PACKAGE_NAME"
// run command "go get github.com/google/uuid"
import (
    "fmt"
    "github.com/google/uuid"
)
func main(){
    fmt.Println(uuid.New())
}

// replace online package with local package
// through command "go mod edit -replace abc.com/package=./go_package"
// or just edit "go.mod" directly as
replace abc.com/package => ./go_package
```
# Variable types [bool, string, int, int8, int16, int32, int64, uint, uint8, uint16, uint32, uint64, uintptr, byte [int8], rune [int32], float32, float64, complex64, complex128, slice, map, channel, function, interface, const, type]
```
var NAME TYPE

// variables initialize
var NAME TYPE = VALUE
var NAME1, NAME2 TYPE = VALUE1, VALUE2
var NAME1, NAME2 = VALUE1, VALUE2
NAME := VALUE // only allow in function scope, not package level

// multiple declare variables
var (
    NAME TYPE = VALUE
    NAME1 TYPE = VALUE1
    NAME2 TYPE = VALUE2
)

// Zero values [0, false, "", nil]

// Type conversions
T(v)
var i int = 15
var f float64 = float64(i)

// type interface [short variable declaration]
a := 1 // means a is integer type

// constants
const PI = 3.14 // cannot use := to assign value

// variable with memory
// in function level, declared variable must use, 
// else comply error, package and statement as well; 
// except declare in package level or 
// use const instead for non-use variable

// type
type MyInt int64
type MyFloat float64
type MyString string

// rune
var a rune = 97
fmt.Printf("%q\n", a) // 'a'
```
# string
- len(VARIABLE)
- combine strings with "+" / plus sign
- fmt.Printf("%")
    - [any kind of value] %v, %#v, %T, %%, %t
    - [integer value] %b, %c, %d, %o, %O, %q, %x, %X, %U
    - [floating value] %b, %e, %E, %f, %F, %g, %G, %x, %X
    - [string, slice of byte value] %s, %q, %x, %X
    - [slice value] %p
    - [pointer value] %p
- escape characters
    - \a for alert/bell
    - \b for backspace
    - \\ for backslash (\)
    - \t for horizontal tab
    - \n for line feed [new line]
    - \f for form feed
    - \r for carriage return
    - \v for vertical tab
    - \' for single quote in rune type
    - \" for double quote in string type
- raw string literal by using backticks(`)
```
msg := `line 1
line 2
line 3
`
```
- escape HTML
```
const div = `<div class="container"></div>`
fmt.Println(html.EscapeString(div))
```
- escape URL
```
const u = `https://google.com`
fmt.Println(url.PathEscape(u))
```
- fmt.Scanf()
```
func main(){
    var v string
    fmt.Printf("Enter your name here: ")
    fmt.Scanf("%s", &v)
    fmt.Printf("Hello, %s", v)
}
```
- fmt.Scan()
```
func main(){
    var v string
    fmt.Prinf("Enter your name here: ")
    fmt.Scan(&v)
    fmt.Printf("Hello, %s", v)
}
```
- fmt.Sprintf() // same as fmt.Printf but return as string
- strconv.Itoa(123) / strconv.Atoi("321")
- strconv.ParseBool("true")
- strconv.ParseFloat("")
- strconv.ParseInt()
- strconv.ParseUint()
# Operators
- Arithmetic Operators [+ - * / % ++ --]
- Assignment Operators [= += -= *= /= %=]
    - x=y
    - x+=y same as x=x+y
    - x-=y same as x=x-y
    - x*=y same as x=x*y
    - x/=y same as x=x/y
    - x%=y same as x=x%y
- Comparison Operators [== != < <= > >=]
- Logical Operators [&& || !]
    - false &&  false   =   true
    - true  &&  true    =   true
    - false &&  true    =   false
    - false ||  false   =   false
    - true  ||  true    =   true
    - false ||  true    =   true
    - !                 =   not
- Bitwise Operators [& | ^ << >>]
    - &     AND
    - |     OR
    - ^     XOR
    - <<    ZERO FILL LEFT SHIFT
    - >>    SIGNED RIGHT SHIFT
- Operator Precedence
    - Postfix [left to right]
        () [] <- . ++ --
    - Unary [left to right]
        + - ! ~ ++ -- (type)* & sizeof
    - Multiplicative [left to right]
        * / %
    - Additive [left to right]
        + -
    - Shift [left to right]
        << >>
    - Relational [left to right]
        < <= > >=
    - Equality [left to right]
        == !=
    - Bitwise AND [left to right]
        &
    - Bitwise XOR [left to right]
        ^
    - Bitwise OR [left to right]
        |
    - Logical AND [left to right]
        &&
    - Logical OR [left to right]
        ||
    - Assignment [right to left]
        = += -+ *= /= %= >>= <<= &= ^= |=
    - Comma [left to right]
        ,
# Functions
```
func FUNCTION_NAME(PARAMETER PARAMETER_TYPE) RETURN TYPE {}
func la(name string) string { 
    // function_name is la, 
    // has name as string parameter and 
    // return string
    return name
}

// for no return function, 
// no need to declare return type
func noReturn(){} 

func returnMultiple(a, b int) (int, string){}

// Naked return functions
func nakedReturn(a, b int) (a, b int){
    return // same as return a, b
}

// block
func main(){
    a := 10
    {
        a := 20
        fmt.Println(a) // 20
    }
    fmt.Println(a) // 10
}
```
- variadic function
```
func vf(str ...string){ 
    // declare one str parameter 
    // but could have multiple slices
    fmt.Println(s[0])
    fmt.Println(s[1])
    fmt.Println(s[2])
}
```
# Anonymous Function
```
func(name string){
    fmt.Println("Hello, ", name)
} ("La") // Hello La
```
# Function Values
```
func todo(fn func(string) string) {
    msg := fn("everybody")
    fmt.Println(msg)
}
func main(){
    say := func(msg string) string {
        return "Hello" + msg
    }
    todo(say) // Hello everybody
}
```
# Function Closures
// any anonymous function could interact with 
// surround variables, called "closure"
```
func add() func(int) int {
    sum := 0
    return func(a int) int {
        // could use "sum" variable in anonymous function, 
        // even it is not in this function scope
        sum += a 
        return sum
    }
}
func main(){
    one, two := add(), add()
    for i:=0; i<3; i++ {
        fmt.Println(one(1), two(2)) // 1 2; 2 4; 4 6
    }
}
```
# Flow Control Statements
- if, if...else, if...else if...else
```
if condition_expression {
    statement
}
v := 1
if v < 5 {
    fmt.Println("v is less than five")
}

if short_statement; condition_expression {
    statement
}
if v:=1; v<5 {
    fmt.Println("v is less than five")
}

if short_statement; condition_expression{
    if_statement
} else if short_statement; condition_expression {
    else_if_statement
} else {
    else_statement
}
```
- for
```
for init_statement; condition_expression; post_statement {
    statement
}

for i:=0; i<5; i++ {
    fmt.Println("number ", i)
}

// init_statement and post_statement could leave out as:
for ; condition_expression; {
    statement
}

// use "for" instead of "while"
for condition_expression {
    // when condition_expression is true
    // below statement continue running
    // until condition_expression is false
    // below statement stop
    statement
}
j:=0
for ; j<5; {
    j += j
}
```
- forever
```
while (1) {}

for(;;){}

do {} while (1);
```
- break
```
func main(){
    count := 0
    for {
        if count < 3 {
            fmt.Println(count)
            count ++
        } else {
            break
        }
    }
}
```
- continue
```
for count:=0; count<3; count++ {
    if count == 0{
        continue // when count=0, skip to next loop
    }
}
```
- switch...case
```
switch short_statement; expression {
    case expression1:
        // run statement1 when 
        // above expression == expression1 and
        // exit the switch block
        statement1; 
    case expression2:
        // run statement2 when 
        // above expression == expression2 and
        // exit the switch block
        statement2;
    case expression3:
        // run statement3 when 
        // above expression == expression3 and
        // exit the switch block
        statement3;
    default:
        // run default_statement when 
        // above expression != above expressions and
        // exit the switch block
        default_statement;
}

import (
    "fmt"
    "time"
)
func main(){
    fmt.Println("When's May?")
    m := time.Now().Month()
    switch time.May {
        case m:
            fmt.Println("This month")
        case m+1:
            fmt.Println("Next month")
        case m-1:
            fmt.Println("Last month")
        default:
            fmt.Println("Too far away")
    }
}

// fallthrough
switch short_statement; expression {
    case expression1:
        statement1
        fallthrough 
        // continue to case expression2, 
        // if no fallthrough after met the condition, 
        // this flow will break and exit the block
    case expression2:
        statement2
        fallthrough
}

// switch without condition
switch {
    case expression1:
        statement1
    case expression2:
        statement2
    default:
        default_statement
}
```
- defer [stacked postpone, last in first out]
```
defer fmt.Println("Golang") // last print
defer fmt.Println("world") // secondly
fmt.Println("hello") // first print
```
- goto
```
fmt.Println("A") // print out
goto FINISH
fmt.Println("C") // no print
FINISH:
    fmt.Println("B") // print out
```
# Pointer [*T]
// the special variable which hold or 
// point to memory address
```
var p *int // p is nil, point to integer at memory address

a := 1
b := &a // b point to a at memory address
c := &a // c point to a at memory address
// but could not directly point to plain data as d := &123
// except array, slice or map as pa := &[2]int{1,2}
*c := 5 // a will change to 5 too
d := b // d [standard variable, not pointer] only copy value of b
var p *int
p := b // p copy pointer/memory address from b
```
# Struct
```
type MyStruct struct {
    field1 type
    field2 type
}

type Axis struct {
    X int
    Y int
}

func main(){
    a1:=Axis{1,2}
    fmt.Println(a1) // {1 2}
    fmt.Println(a1.X, a1.Y) // {1 2}
    a1.X = 4 // struct literals
}

var a struct {
    X, Y int
}
a1 = a{1,2}
a2 = a{X: 1, Y: 2}
a3 = a{X: 1}
a4 = a{Y: 2}
a5 = a{}
a6 = &a{1l,22}

// anonymous struct
s := struct {
    Name string
    Age int
} {
    "La",
    30, // when declaring no need comma [,] but assigning value must have
}
```
# Arrays/Slice
- array is a list of certain value
```
[n]T // nil zero value

var a [5]int

var hw [2]string
hw[0]="hello"
hw[1]="world"
fmt.Println(hw) // [hello world]

var b := [...]int{1,2,3} 
// same as b:=[3]int{1,2,3}
// it count the length automatically
```
- slice is a list with dynamic members
```
[]T

// len() and cap()
s := []int{1,2,3}
len(s) // 3
cap(s) // 3

// slicing
s[0:2]
s[:] // slice from first index [0] to last index

// make()
s1 := make([]int, 5) // len(s1) = cap(s1) = 5

// slice in slice
double_slice := [][]int {
    []int{0,1},
    []int{1,0},
}

// append()
s2 = append(s1, 5)
```
# Map [key_type] value_type
```
map[T_key]T_value

var m map[string]int // m = nil
m["x"] = 3
m["y"] = 5

var m1:=map[string]int{
    "x":3,
    "y":5,
}

type Axis struct {
    X,Y int
}
var m2:=map[string]Axis{
    "foo": Axis{1,2},
    "bar": Axis{3,-5},
}
var m3:=map[string]Axis{
    "foo": {1,2},
    "bar": {3,-5},
}

m1["x"]=100

delete(m2, "foo")

value, key := m["x"] // if m map have "x" key, value equal "value" and key equal "true"

value := m["y"]

len(m)
```
# range
```
var num = []int{1,2,3,4,5}
var m = map[string]int{
    "x":1,
    "y":2,
}
func main(){
    for i, v := range num {
        fmt.Printf("index is %d, value is %D\n", i, v)
    }

    for i, _ := range num {
        fmt.Printf("index is %d\n", i)
    }

    for _, v := range num {
        fmt.Printf("value is %d\n", v)
    }

    for k,v := range m {
        fmt.Printf("key is %s, value is %d\n", k, v)
    }

    for k, _ := range num {
        fmt.Printf("key is %d\n", k)
    }

    for _, v := range num {
        fmt.Printf("value is %d\n", v)
    }
}
```
# Method
# Generics
```
// type parameters
func compare[T comparable](a T, b T){
    fmt.Println(a == b)
}

func search[T comparable](s []T, n T) int {
    for i, v  := range s {
        if v == n {
            return i
        }
    }
    return -1
}
func main() {
    s1 := []int{2,4,8,10}
    fmt.Println(search(s1, 4)) // 1
    s2 := []string{"red", "pink", "blue"}
    fmt.Println(search(s2, "white")) // -1
}

// generic types
type MyStruct[T any] struct {
    Val T
}
a := MyStruct[int]{1}
b := MyStruct[bool]{false}
c := MyStruct[string]{"Hello"}
```
# Concurrency // process at the same time or parallel [goroutine]
```
go f(x, y, z)

import (
    "fmt"
    "time"
)
func say(s string) {
    for i:=0; i<3; i++ {
        time.Sleep(100 * time.Millisecond)
        fmt.Println(s)
    }
}
func main(){
    s := "World"
    go say(s)
    say("Hello")
}

// Channels
ch := make(chan int)
ch <- v1 // v1 is int variable 

func sum(s []int, ch chan int){
    sum := 0
    for _, v := range s {
        sum += v
    }
    ch <- sum
}
func main(){
    ch := make(chan int)
    go sum([]int{1,2,3}, ch) // 1+2+3=6
    go sum([]int{4,5,6}, ch) // 4+5+6=15
    a,b := <-ch, <-ch
    fmt.Println(a, b) // 15 6
}

// inline goroutine
func todo(ch chan int){
    ch <- 1
}
ch := make(chan int)
go todo(ch)

ch1 := make(chan int)
go func(){
    ch <- 1
}()
fmt.Println(<-ch) // 1

// Buffered Channels
ch := make(chan int, 10) // 10 is buffer argument

// range with close()
v, ok := <-ch // to check what if the channel is closed?

func compute(s []int, ch chan int){
    for _, v := range s {
        ch <- v * 2
    }
    close(ch)
}
func main(){
    ch := make(chan int, 3)
    go compute([]int{1,2,3}, ch)
    for {
        v, ok := <- ch
        if !ok {
            break
        }
        fmt.Println(v)
    }
}

func compute(s []int, ch chan int){
    for _, v := range s {
        ch <- v * 2
    }
    close(ch)
}
func main(){
    ch := make(chan int, 3)
    go compute([]int{1,2,3}, ch)
    for v := range ch{
        fmt.Println(v)
    }
}

// select ...case
func main(){
    ch := make(chan int)
    quit := make(chan int)
    go func(){
        for i:=0; i<3; i++ {
            fmt.Println(<-ch)
        }
        quit <- 0
    }()
    count := 0
    for {
        select {
            case ch <- count:
                count += 2
            case <- quit:
                fmt.Println("quit")
                return
        }
    }
}

// select ...case ...default
select {
    case i:= <-ch:
        statement
    default:
        statement
}

import (
    "fmt"
    "time"
)
func main(){
    tick := time.Tick(100*time.Millisecond)
    finish := time.After(500*time.Millisecond)
    count := 0
    for {
        select {
            case <- tick:
                count += 1
                fmt.Println("Count: ", count)
            case <- finish:
                fmt.Println("Finish")
                return
            default:
                fmt.Println("^_^")
                time.Sleep(50*time.Millisecond)
        }
    }
}

// len() and cap() with buffered channel
ch := make(chan int, 10)
fmt.Printf("length= %d, capacity= %d", len(ch), cap(ch)) // length= 0, capacity= 10
```
