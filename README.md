# ยินดีที่ได้รู้จัก Golang  ผ่านภาษาชีและจาวา
# golangintroductionwithjavaandc
# Golang introduction with Java and C

# Commands
```
go mod init
go mod tidy
go get <URL>
go mod edit -replace xxx=yyy
```
# Variable types [bool, string, int, int8, int16, int32, int64, uint, uint8, uint16, uint32, uint64, uintptr, byte [int8], rune [int32], float32, float64, complex64, complex128, slice, map, channel, function, interface, const, type]
# string
- fmt.Printf("%")
    - [any kind of value] %v, %#v, %T, %%, %t
    - [integer value] %b, %c, %d, %o, %O, %q, %x, %X, %U
    - [floating value] %b, %e, %E, %f, %F, %g, %G, %x, %X
    - [string, slice of byte value] %s, %q, %x, %X
    - [slice value] %p
    - [pointer value] %p
- fmt.Scanf()
- fmt.Scan()
- fmt.Sprintf()
- strconv.Itoa(123) / strconv.Atoi("321")
- strconv.ParseBool("true")
- strconv.ParseFloat("")
- strconv.ParseInt()
- strconv.ParseUint()
# Operators
- Arithmetic Operators [+ - * / % ++ --]
- Assignment Operators [= += -= *= /= %=]
    - x=y
    - x+=y == x=x+y
    - x-=y == x=x-y
    - x*=y == x=x*y
    - x/=y == x=x/y
    - x%=y == x=x%y
- Comparison Operators [== != < <= > >=]
- Logical Operators [&& || !]
- Bitwise Operators [& | ^ << >>]
- Operator Precedence
# Functions
```
func FUNCTION_NAME(PARAMETER PARAMETER_TYPE) RETURN TYPE {}
func la(name string) string {
    return name
}
func noReturn(){} // for no return func, no need to declare return type
func returnMultiple(a, b int) (int, string){}
func nakedReturn(a, b int) (a, b int){
    return
}
```
- variadic function
```
func vf(str ...string){ // declare one str parameter but could have multiple slices
    fmt.Println(s[0])
    fmt.Println(s[1])
    fmt.Println(s[2])
}
```
# Anonymous Function
```
func(name string){
    fmt.Println("Hello, ", name)
} ("La")
```
# Function Values
# Function Closures
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

for ; condition_expression; {
    statement
}
for condition_expression {
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
        statement1;
    case expression2:
        statement2;
    case expression3:
        statement3;
    default:
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

switch short_statement; expression {
    case expression1:
        statement1
        fallthrough // continue to case expression2, if no fallthrough after met the condition, this flow will break
    case expression2:
        statement2
        fallthrough
}

switch {
    case expression1:
        statement1
    case expression2:
        statement2
    default:
        default_statement
}
```
- defer [postpone, last in first out]
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
```
var p *int // p is nil, point to integer in memory

a := 1
b := &a // b point to a in memory
c := &a // c point to a in memory
```
# Structs
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
    a1.X = 4
}

var a struct {
    X, Y int
}
```
# Arrays/Slice
- array is a list of certain value
```
[n]T

var a [5]int

var hw [2]string
hw[0]="hello"
hw[1]="world"
fmt.Println(hw) // [hello world]

var b := [...]int{1,2,3} // same as b:=[3]int{1,2,3}
```
- slice is a list with dynamic members
```
[]T

s := []int{1,2,3}

len(s) // 3
cap(s) // 3

s[0:2]
s[:]

s1 := make([]int, 5) // len(s1) = cap(s1) = 5

double_slice := [][]int {
    []int{0,1},
    []int{1,0},
}

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
```
// there are two types of receiver [value and pointer receiver]
// value receiver
func (r T) method_name(){} // r - receiver with T type

type MyInt int
func (m MyInt) Add(value int) int {
    return int(m) + value
}
func main(){
    num := MyInt(3)
    fmt.Println(num.Add(5)) // 8
}

type Rectangle struct {
    Width, Height int
}
func (r Rectangle) Area() int {
    return r.Width * r.Height
}
func main(){
    rec := Rectangle{3, 4}
    fmt.Println(rec.Area()) // 12
}

type Rectangle string {
    Width, Height int
}
func Area(r Rectangle) int {
    return r.Width * r.Height
}
func main(){
    rec := Rectangle{3, 4}
    fmt.Println(Area(rec)) // 12
}

// pointer receiver
func (p *T) method_name() {}

type Rectangle struct {
    Width, Height int
}
func (r *Rectangle) Area() int {
    return r.Width * r.Height
}
func main(){
    rec := &Rectangle{3, 4}
    fmt.Println(rec.Area()) // 12
}
```
# Interfaces
```
type Area interface {
    Compute() float64
}

type MyInf interface {
    Todo()
}
type MyStruct struct {
    S string
}
func (m MyStruct) Todo() {
    fmt.Println("Say ", m.S)
}
func main(){
    var m MyInf = MyStruct("Hello")
    m.Todo() // Say Hello
}

// inline declare interface
func main(){
    var m interface {
        Todo()
    }
    fmt.Printf("%v, %T\n", m, m) // (<nil>, <nil>)
}

// empty interface, no method interface
interface{}

// any
var a any
a = 5
fmt.Println(a) // 5
a = "Hello"
fmt.Println(a) // Hello

a1 := [4]any{1, 2.2, "OK", true} // same as >>> a1:=[4]interface{}{1, 2.2, "OK", true}

a2 := []any{1, 2.2, "OK", true}

func display(value ...any) { // func display(value ...interface{})
    for _, v:= range value {
        fmt.Println("value is ", v)
    }
}
func main(){
    display(1,2.2, "OK", false)
}

// type assertion: i:=j.(T) // j is interface type
var i any = "any_value"
j := i.(string) // var j string = i.(string)

// check interface value type
var i any = "any_value"
j,k := i.(string) // j="any value", k=true
j,k := i.(int) // j=0, k=false because i hold string

// type switches
func todo(i any) {
    switch t := i.(type) {
        case int:
            fmt.Println("Number is ", v)
        case string:
            fmt.Println("String is ", v)
        default:
            fmt.Printf("type is %T \n", v)
    }
}
func main(){
    todo(5) // Number is 5
    todo("something") // String is something
    todo(true) // type is bool
}

// Stringer
type Stringer interface {
    String() string
}
type Rectangle struct {
    Width, Height int
}
func (r *Rectangle) String() string {
    return fmt.Sprintf("Width is %d, Height is %d", r.Width, r.Height)
}
func main(){
    rec := $Rectangle{3,4}
    fmt.Println(rec) // Width is 3, Height is 4
    fmt.Println(rec.String()) // Width is 3, Height is 4
}

// Errors
type error interface {
    Error() string
}

func main(){
    i, err := strconv.Atoi("5") // convert string to integer
    if err != nil {
        fmt.Printf("Could not convert number: %v\n", err) // this statement does not run, because "5" is string, could convert into integer
        return
    }
    fmt.Println("Converted", i "to integer") // Converted 5 to integer
}
func main(){
    i, err := strconv.Atoi("abc")
    if eer != nil {
        fmt.Printf("Could not convert number: %v\n", err) // Could not convert number: strconv.Atoi: parsing "abc": invalid syntax
        return
    }
    fmt.Println("Convert ", i, " to integer") // this statement is not run
}

// reader
type Reader interface {
    Read(buf []byte) (n int, err error)
}
```
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
