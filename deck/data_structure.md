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

## Array

var name [n]T

```go
    var array [5]string
```

---

## Array auto counting

var name [n]T

```go
    primes := [...]int{2, 3, 5, 7, 11, 13}    

```

---

## Foreach in Array

var name [n]T

```go
    primes := [...]int{2, 3, 5, 7, 11, 13}

    for i := range primes {
        fmt.Println(primes[i])
    }
```

---

## Foreach index & value

var name [n]T

```go
    primes := [...]int{2, 3, 5, 7, 11, 13}

    for i, prime := range primes {
        fmt.Println(i, prime)
    }
```

---

## Slice

var name []T

```go
    var slice []int

    primes := [...]int{2, 3, 5, 7, 11, 13}    
    slice = primes[1:4]

    for i := range slice {
        fmt.Println(slice[i])
    }
```

---

## Zero value of slice is nil

```go
    var s []int

    if s == nil {
        fmt.Println("it's nil")
    }

// make it first
    s := make([]int, 5)
```

---

## append slice

```go
    s := []int{1, 2, 3, 4, 5}
    s = append(s, 6, 7, 8)
```

---

## Exercise: couple

"abcdef" -> []string{"ab","cd","ef"}
"abcdefg" -> []string{"ab","cd","ef","g*"}

---

## Exercise: moretypes/18

https://go.dev/tour/moretypes/18
https://go-tour-th.appspot.com/moretypes/18

---

## Variadic function (Variable number of arguments)

func variadic(nums ...int)

---

## Spread operator

```go
func variadic(nums ...int) {
    
}

var slice = []int{1, 3, 5, 7, 9}
variadic(slice...)

```

---

## len() with slice

```go
    s := []primes{2, 3, 5, 7, 11, 13}

    fmt.Println(len(s))
```

---

## map[T]T

```go
    var m map[string]string
```

---

## zero value of map is nil

```go
    var m map[string]string

    if m == nil {
        fmt.Println("it's nil")
    }
```

---

## map need home

### make

```go
    m := make(map[string]string)

    if m == nil {
        fmt.Println("it's nil")
    }

    m["a"] = "apple"
    m["b"] = "banana"
    m["c"] = "coconut"
    m["d"] = "durian"
    m["e"] = "elderberry"
    m["f"] = "fig"
    m["g"] = "guava"
```

---

## construct map

```go
    m := map[string]string{
        "a" : "apple",
        "b" : "banana",
        "c" : "coconut",
        "d" : "durian",
        "e" : "elderberry",
        "f" : "fig",
        "g" : "guava",
    }

    for k, v := range m {
        fmt.Println(k, v)
    }
```

---

## delete a key

```go
    m := map[string]string{
        "a" : "apple",
        "b" : "banana",
        "c" : "coconut",
        "d" : "durian",
        "e" : "elderberry",
        "f" : "fig",
        "g" : "guava",
    }

    delete(m, "d")

    for k, v := range m {
        fmt.Println(k, v)
    }
```

---

## len() with map

```go
    m := map[string]string{
        "a" : "apple",
        "b" : "banana",
        "c" : "coconut",
        "d" : "durian",
        "e" : "elderberry",
        "f" : "fig",
        "g" : "guava",
    }

    fmt.Println(len(m))
```

---

## Exercise: map

open a file oscar_age_male.csv

https://github.com/focusive/go102/tree/master/testdata

print any actors name who got the oscar more than one time

```txt
    Marlon Brando
    Daniel Day-Lewis
    Sean Penn
    Tom Hanks
    Fredric March
    Spencer Tracy
    Gary Cooper
    Jack Nicholson
    Dustin Hoffman
```

---

## Exercise: map represent json

http://www.groupkt.com/post/c9b0ccb9/country-and-other-related-rest-webservices.htm

http://services.groupkt.com/country/get/iso3code/IND

---

## Type

> type newType T

```go
    type text string
```

> type aliasType = T

```go
    type text = string
```

---

## method on primitive type inspired by Java

```go
    type Int int

    func (i Int) toString() string{
        return strconv.Itoa(int(i))
    }
```

---

## Exercise

New Int Type with Method

.String() to convert integer to string
.Set(n int) to set new value

---

## struct type

```go
    type Rectangle struct {
        Width  float64
        Length float64
    }
```

---

## Construct struct instance

```go
    rec := Rectangle{Width: 10, Length: 12}

    area := rec.Width * rec.Length
```

---

## method on struct

```go
    type Rectangle struct {
        Width  float64
        Length float64
    }

    func (r Rectangle) Area() float64 {
        return r.width * r.length
    }
```
---

## Exercise: struct represent json

http://www.groupkt.com/post/c9b0ccb9/country-and-other-related-rest-webservices.htm

http://services.groupkt.com/country/get/iso3code/IND

---

[Next >](./interface.md#1)