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

## First-Class Function

```go
var add = func(a, b int) int {
    return a + b
}

fmt.Println(add(1, 2))
```

---

## Higher-Order Function

```go
func hof(fn func(string) string) {
    ...
}

func hof() func(string) string {
    ...
}
```

---

## Higher-Order Function Blog

https://dev.to/pallat/hof-in-go-18mm

---

## Closure Function

```go
func main() {
    fn1, fn2 := factory()
    fn1()
    fn1()
    fmt.Println(fn2())

    fn1()
    fmt.Println(fn2())
}

func factory() (func(), func() int) {
    var i int
    return func() {
            i++
        },
        func() int {
            return i
        }
}
```

---

## Exercise Wrapper Function

> Make a Wrapper for FizzBuzz handler to validate JWT

---

## func type

```go
type areaFunc func(float64, float64) float64 
```

---

## Exercise JWT Validator

Validate JWT in FizzBuzzHandler

```http
GET http://localhost:8080/fizzbuzz/3

Header["Authorization"]: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
```

---

## method on function

```go
    type IntnFunc func(int) int

    func (fn IntnFunc) Intn(n int) int {
        return fn(n)
    }
```
---

## API

### Foo/Bar

---

## goroutine

```go
func main() {
    total := 10
    now := time.Now()
    for i := 0; i < total; i++ {
        go printout(i)
    }
    fmt.Println(time.Now().Sub(now))
}

func printout(i int) {
    fmt.Println(i)
}

```

---

## goroutine waiting

```go
var wg = sync.WaitGroup{}

func main() {
    total := 10
    wg.Add(total)
    now := time.Now()
    for i := 0; i < total; i++ {
        go printout(i)
    }
    wg.Wait()
    fmt.Println(time.Now().Sub(now))
}

func printout(i int) {
    fmt.Println(i)
    wg.Done()
}
```

---

## channel

keyword `chan`

- no buffered channel
- buffered channel

---

## buffered channel

```go
total := 10
ch := make(chan int, total)
for i := total; i > 0; i-- {
    ch <- i
}
close(ch)

for i := range ch {
    fmt.Println(i)
}
```

---

## no buffered channel

```go
func main() {
    total := 10
    ch := make(chan struct{})
    now := time.Now()
    for i := 0; i < total; i++ {
        go printout(i, ch)
    }
    for i := 0; i < total; i++ {
        <-ch
    }
    fmt.Println(time.Now().Sub(now))
}

func printout(i int, ch chan struct{}) {
    fmt.Println(i)
    ch <- struct{}{}
}
```

---
