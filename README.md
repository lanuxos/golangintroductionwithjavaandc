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
