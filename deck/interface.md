---
marp: true
html: true
paginate: true
header: '![image width:80px](https://go.dev/images/go-logo-blue.svg)'
footer: '![image width:80px](https://go.dev/images/gophers/pilot-bust.svg)'
---

<style>
section {
    font-family: Arial, Helvetica, sans-serif;
}
section h1 {
    color: #00A29C;
}
section h2 {
    color: #00A29C;
}
</style>

# go

## Basic Syntax

Pallat Anchaleechamaikorn
Go Developer

yod.pallat@gmail.com
https://github.com/pallat

https://go.dev/tour
https://github.com/uber-go/guide

---

## defer

A defer statement defers the execution of a function until the surrounding function returns.

The deferred call's arguments are evaluated immediately, but the function call is not executed until the surrounding function returns.

```go
res, _ := http.DefaultClient.Do(req)

defer res.Body.Close()
body, _ := ioutil.ReadAll(res.Body)
```

---

## a defer

```go
defer fmt.Println("end")

fmt.Println("Hello, Gophers")
```

---

## defer is stack

```go
defer fmt.Println("defer first")
defer fmt.Println("defer second")
defer fmt.Println("defer third")

fmt.Println("Hello, Gophers")
```

---

## Questions? What is the result

```go
func doSomething(n int) {
    defer fmt.Println(n)
    fmt.Println(n)
}
```

---

## Questions? One more

```go
func doSomething(n int) {
    defer fmt.Println(n)
    defer func() {
        fmt.Println(n)
    }()
    n = n * n
    fmt.Println(n)
}
```

---

## defer for recovering

```go
func catchMe() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println(r)
        }
    }()

    s := []int{}

    fmt.Println(s[1])
}
```

---

## interface{}: empty interface

```go
    var i interface{}

    i = 10
    fmt.Printf("type is %T, value is %v\n", i, i)

    i = "ten"
    fmt.Printf("type is %T, value is %v\n", i, i)

    i = struct {
        number int
        text string
    } {
        number: 10,
        text: "ten",
    }
    fmt.Printf("type is %T, value is %v\n", i, i)

    i = func() string {
        return "10"
    }
    fmt.Printf("type is %T, value is %v\n", i, i)
```

---

## interface: What is the real type?

```go
var i interface{}

i = 10
fmt.Printf("type is %T, value is %v\n", i, i)

var n int

n = i
```

---

## interface: type assertion

```go
var i interface{} = "hello"
s := i.(string)
fmt.Println(s)
if s, ok := i.(string); ok {
    fmt.Println(s)
}
```

---

## exercise: FizzBuzz(string|int)

```go
foobar.SayAny(3)
"Foo"

foobar.SayAny("3")
"Foo"
```

---

## switch

```go
switch {
case n%15 == 0:
    s = "FizzBuzz"
case n%5 == 0:
    s = "Buzz"
case n%3 == 0:
    s = "Fizz"
default:
    s = strconv.Itoa(n)
}
```

---

## interface: type switch

```go
var i interface{} = "hello"
switch v := i.(type) {
case int:
    fmt.Printf("%T %d", v, v)
case string:
    fmt.Printf("%T %s", v, v)
default:
    fmt.Println("undefined type")
}
```

---

## interface

To define a set of method signatures

> Interfaces specify behaviors.
> An interface type defines a set
> of methods:

```go
type Stringer interface {
    String() string
}
```

`Interfaces` are `implemented` `implicitly`

---

## interface: error

```go
    type error interface {
        Error() string
    }
```

---

## Interface: names

By convention, one-method interfaces are named by the method name plus an -er suffix or similar modification to construct an agent noun: Reader, Writer, Formatter, CloseNotifier etc.

```go
    type areaer interface {
        area() float64
    }
```

---

## Example: Play with Stringer

---

## Exercise: Intn

test it

```go
func fizzBuzzString() string {
    src := rand.NewSource(time.Now().Unix())
    r := rand.New(src)
    
    return fmt.Sprintf("%s%s%s",fizzbuzz.Say(r.Intn(9)+1),fizzbuzz.Say(r.Intn(9)+1),fizzbuzz.Say(r.Intn(9)+1),fizzbuzz.Say(r.Intn(9)+1))
}
```

---

## Exercise test double

Random 4 number pass to FizzBuzz and test it

---

[Next >](./goroutine.md#1)