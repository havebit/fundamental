---
html: true
inlineSVG: true
paginate: true
header: '![image width:80px](https://go.dev/images/go-logo-blue.svg)'
footer: '![image width:80px](https://go.dev/images/gophers/pilot-bust.svg)'
theme: base-theme
style: |
    section {
        font-family: Arial, Helvetica, sans-serif;
    }
    section h1 {
        color: #00A29C;
    }
    section h2 {
        color: #00A29C;
    }
---

# Basic Syntax

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

| name[0] | name[1] | name[2] | name[3] | name[4] |
|---------|---------|---------|---------|---------|
|   ""    |   ""    |   ""    |   ""    |   ""    |
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
    var slice []string // it's nil
```

---

## Make Slice

```go
    slice := make([]int,4)
```

| int[0] | int[1] | int[2] | int[3] |
|---------|---------|---------|---------|
|   0    |   0    |   0    |   0    |

---

<!-- Scoped style -->
<style scoped>
section th {
    border: 1px solid black;
}
section td:nth-child(5) {
    width: 100px;
    border: 1px dotted gray;
    background-color: #fddd00;
    position: relative;
    animation-name: example;
    animation-duration: 10s;
}
section th:nth-child(5) {
    width: 12px;
    border: 1px dotted black;
    background-color: #fddd00;
}
</style>

## Append Slice

```go
append([]T, ...T) []T
```

```go
ืnums := make([]int,4)
```

| int[0] | int[1] | int[2] | int[3] |
|:-------:|:-------:|:-------:|:-------:|
|   0    |   0    |   0    |   0    |

```go
nums = append(nums, 5)
```

| int[0] | int[1] | int[2] | int[3] | int[4]
|:-------:|:-------:|:-------:|:-------:|:-------:|
|   0    |   0    |   0    |   0    |   5

---

## Deep to Slice: Make with lenght

<!-- Scoped style -->
<style scoped>
section th {
    border: 1px solid black;
}
section td:nth-child(2) {
    width: 100px;
    border: 1px dotted gray;
    background-color: #eeeeee;
    position: relative;
    animation-name: example;
    animation-duration: 10s;
}
section th:nth-child(5) {
    width: 12px;
    border: 1px dotted black;
    background-color: #dddddd;
}
section th:nth-child(6) {
    width: 12px;
    border: 1px dotted black;
    background-color: #dddddd;
}

@keyframes example {
  0%   {background-color:#ffffff; left:0px; top:0px;}
  25%  {background-color:#eeeeee; left:0px; top:10px;}
  50%  {background-color:#eeeeee; left:0px; top:20px;}
  75%  {background-color:#dddddd; left:0px; top:30px;}
  100% {background-color:#cccccc; left:0px; top:40px;}
}

</style>

```go
nums := make([]int,4)
```

| &nbsp;&nbsp; type &nbsp;&nbsp; | &nbsp;&nbsp; ptr &nbsp;&nbsp; | &nbsp;&nbsp; len &nbsp;&nbsp; | &nbsp;&nbsp; cap &nbsp;&nbsp; |
|:----:|:----:|:----:|:----:|
|[]int | *<br/> ⇣ <br/> [array] |  4   |   4  |

|0|0|0|0|
|-|-|-|-|

---

## Deep to Slice: Make with lenght and capacity

<!-- Scoped style -->
<style scoped>
section th {
    border: 1px solid black;
}
section td:nth-child(2) {
    width: 100px;
    border: 1px dotted gray;
    background-color: #eeeeee;
    position: relative;
}
section th:nth-child(5) {
    width: 12px;
    border: 1px dotted black;
    background-color: #dddddd;
}
section th:nth-child(6) {
    width: 12px;
    border: 1px dotted black;
    background-color: #dddddd;
}

</style>

```go
nums := make([]int,4,6)
```

| &nbsp;&nbsp; type &nbsp;&nbsp; | &nbsp;&nbsp; ptr &nbsp;&nbsp; | &nbsp;&nbsp; len &nbsp;&nbsp; | &nbsp;&nbsp; cap &nbsp;&nbsp; |
|:----:|:----:|:----:|:----:|
|[]int | *<br/> ⇣ <br/> [array] |  4   |   6  |

|0|0|0|0|||
|-|-|-|-|-|-|

---

<style scoped>
section {
    display: inline-block;
}

section strong {
    background-color: #fefeef;
    color: #00A29C;
    padding-top: 4px;
    padding-bottom: 4px;
    padding-left: 10px;
    padding-right: 10px;
}

section pre {
    display: inline;
    background-color: #fddd00;
    width: 350px;
    float: left;
    margin-right: 40px;
    font-size: 20px;
}

section table {
    width: auto;
    font-size: 20px;
}

</style>

## Assign array range to Slice

var name []T

```go
    primes := [4]int{2, 3, 5, 7}    ➡️
```

|primes[0]|primes[1]|primes[2]|primes[3]|
|:-:|:-:|:-:|:-:|
|2|3|5|7|

```go
    var slice []int
    slice = primes[1:3]
```

|primes[0]|primes[1]|primes[2]|primes[3]|
|:-:|:-:|:-:|:-:|
|2|**3**|**5**|7|
||**slice[0]**|**slice[1]**|

| type | ptr | len | cap |
|:----:|:----:|:----:|:----:|
|[]int | &primes |  2   |   3  |

---

<style scoped>
section {
    display: inline-block;
}

section strong {
    background-color: #fefeef;
    color: #00A29C;
    padding-top: 4px;
    padding-bottom: 4px;
    padding-left: 10px;
    padding-right: 10px;
}

section pre {
    display: inline;
    background-color: #fddd00;
    width: 350px;
    float: left;
    margin-right: 40px;
    font-size: 20px;
}

section table {
    width: auto;
    font-size: 20px;
}

</style>

## Assign array range to Slice: from 0

var name []T

```go
    primes := [4]int{2, 3, 5, 7}    ➡️
```

|primes[0]|primes[1]|primes[2]|primes[3]|
|:-:|:-:|:-:|:-:|
|2|3|5|7|

```go
    var slice []int
    slice = primes[0:3]
    slice = primes[:3]
```

|primes[0]|primes[1]|primes[2]|primes[3]|
|:-:|:-:|:-:|:-:|
|**2**|**3**|**5**|7|
|**slice[0]**|**slice[1]**|**slice[2]**|

| type | ptr | len | cap |
|:----:|:----:|:----:|:----:|
|[]int | &primes |  3   |   4  |

---

<style scoped>
section {
    display: inline-block;
}

section strong {
    background-color: #fefeef;
    color: #00A29C;
    padding-top: 4px;
    padding-bottom: 4px;
    padding-left: 10px;
    padding-right: 10px;
}

section pre {
    display: inline;
    background-color: #fddd00;
    width: 350px;
    float: left;
    margin-right: 40px;
    font-size: 20px;
}

section table {
    width: auto;
    font-size: 20px;
}

</style>

## Assign array range to Slice: to last element

var name []T

```go
    primes := [4]int{2, 3, 5, 7}    ➡️
```

|primes[0]|primes[1]|primes[2]|primes[3]|
|:-:|:-:|:-:|:-:|
|2|3|5|7|

```go
    var slice []int
    slice = primes[2:4]
    slice = primes[2:]
```

|primes[0]|primes[1]|primes[2]|primes[3]|
|:-:|:-:|:-:|:-:|
|2|3|**5**|**7**|
|||**slice[0]**|**slice[1]**|

| type | ptr | len | cap |
|:----:|:----:|:----:|:----:|
|[]int | &primes |  2   |   2  |

---

<style scoped>
section {
    display: inline-block;
}

section strong {
    background-color: #fefeef;
    color: #00A29C;
    padding-top: 4px;
    padding-bottom: 4px;
    padding-left: 10px;
    padding-right: 10px;
}

section pre {
    display: inline;
    background-color: #fddd00;
    width: 350px;
    float: left;
    margin-right: 40px;
    font-size: 20px;
}

section table {
    width: auto;
    font-size: 20px;
}

</style>

## Assign array range to Slice: all elements

var name []T

```go
    primes := [4]int{2, 3, 5, 7}    ➡️
```

|primes[0]|primes[1]|primes[2]|primes[3]|
|:-:|:-:|:-:|:-:|
|2|3|5|7|

```go
    var slice []int
    slice = primes[0:4]
    slice = primes[:]
```

|primes[0]|primes[1]|primes[2]|primes[3]|
|:-:|:-:|:-:|:-:|
|**2**|**3**|**5**|**7**|
|**slice[0]**|**slice[1]**|**slice[2]**|**slice[3]**|

| type | ptr | len | cap |
|:----:|:----:|:----:|:----:|
|[]int | &primes |  4   |   4  |

---

## len() with slice

```go
    s := []primes{2, 3, 5, 7, 11, 13}

    fmt.Println(len(s))
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

## Delete an element in Slice

```go
s := []int{1, 2, 3, 4, 5}
s = append(s[:2], s[3:]...)
```


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

## Method

```go
var i Int

s := i.toString()

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
        return r.Width * r.Length
    }
```
---

## Pointer Receiver

```go
type Book struct {
   Name   string
   Author string
}

func (book *Book) SetName(s string) {
   return book.Name = name
}

func (book Book) String() string {
   return book.Name + " by " + book.Author
}
```

---

## Exercise: Int with get/set

**New Int Type with Method**

**.String()** to convert integer to string
**.Set(n int)** to set a new value into it

---

[Next >](./interface.md#1)
