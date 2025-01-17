# Notes: Introduction to Go

This document provides an introduction to the Go programming language as outlined in Unit 1, with an emphasis on relating Go concepts to C for ease of understanding. 


## Unit 1: Introduction to Go

### 1.1 Go Runtime and Compilation
- **Go is a compiled language**: Unlike interpreted languages, Go code is compiled into machine code.
- **Key tools**: The `go` command handles building, running, and testing.
  ```bash
  go build    # Compiles the code
  go run      # Compiles and runs the code
  go test     # Runs tests
  ```
- **Go vs. C**: Similar to C, Go produces efficient machine code but simplifies the process with an integrated toolchain.

**Practice Question:**
1. Write a `Hello, World!` program in Go and compile it using `go build`.

**Answer:**
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```
Compile and run with:
```bash
go build hello.go
./hello
```

---

### 1.2 Keywords and Identifiers
- **Keywords**: Reserved words like `func`, `var`, `if`, `else`, `for`. Cannot be used as identifiers.
- **Identifiers**: Names for variables, functions, etc., must start with a letter or underscore.

**Example:**
```go
var name string
func main() {
    fmt.Println("Go Keywords and Identifiers")
}
```

**Comparison to C:** Similar restrictions on identifiers, but Go avoids unnecessary complexity (e.g., no `typedef`).

**Practice Question:**
1. List five Go keywords and explain their purpose.

**Answer:**
- `func`: Declares a function.
- `var`: Declares a variable.
- `if`: Used for conditional statements.
- `for`: Loop construct.
- `const`: Declares a constant.

---

### 1.3 Constants and Variables
- **Constants**: Declared using `const`, cannot be changed.
- **Variables**: Declared using `var` or `:=` syntax.

**Example:**
```go
const Pi = 3.14
var radius float64 = 5
area := Pi * radius * radius
```

**Comparison to C:** Similar to `#define` and variable declarations, but Go handles scoping better.

**Practice Question:**
1. Declare a constant and a variable, then compute a simple expression.

**Answer:**
```go
const Pi = 3.14159
var diameter = 10.0
circumference := Pi * diameter
fmt.Println("Circumference:", circumference)
```

---

### 1.4 Operators and Expressions
- Arithmetic: `+`, `-`, `*`, `/`, `%`
- Relational: `==`, `!=`, `<`, `>`, `<=`, `>=`
- Logical: `&&`, `||`, `!`

**Example:**
```go
x, y := 10, 20
sum := x + y
fmt.Println("Sum:", sum)
```

**Comparison to C:** Operators are nearly identical, but Go disallows implicit type conversions.

**Practice Question:**
1. Write a Go program using all relational operators.

**Answer:**
```go
x, y := 10, 20
fmt.Println(x == y) // false
fmt.Println(x != y) // true
fmt.Println(x < y)  // true
fmt.Println(x > y)  // false
fmt.Println(x <= y) // true
fmt.Println(x >= y) // false
```

---

### 1.5 Local Assignments
- **Short declaration**: `:=` initializes and assigns variables in the same step.
- **Block scope**: Variables declared inside functions are not accessible outside.

**Example:**
```go
func main() {
    x := 42
    fmt.Println(x)
}
```

**Comparison to C:** No need for explicit type declarations, unlike C's `int x = 42`.

**Practice Question:**
1. Demonstrate scope by declaring variables inside and outside a function.

**Answer:**
```go
var globalVar = "I am global"
func main() {
    localVar := "I am local"
    fmt.Println(globalVar)
    fmt.Println(localVar)
}
```

---

### 1.6 Booleans, Numeric, Characters
- **Booleans**: `true`, `false`
- **Numeric types**: `int`, `float64`
- **Characters**: Represented using runes (`rune` type, alias for `int32`).

**Example:**
```go
var isActive bool = true
char := 'A'
fmt.Println(isActive, char)
```

**Practice Question:**
1. Declare a boolean, an integer, and a rune. Print their values.

**Answer:**
```go
isAvailable := true
num := 100
char := 'G'
fmt.Println(isAvailable, num, char)
```

---

### 1.7 Pointers and Addresses
- **Syntax**: `*` for dereferencing, `&` for address-of.
- **No pointer arithmetic in Go.**

**Example:**
```go
x := 10
ptr := &x
fmt.Println("Address:", ptr, "Value:", *ptr)
```

**Comparison to C:** Similar concepts, but Go abstracts low-level operations for safety.

**Practice Question:**
1. Use pointers to swap two variables' values.

**Answer:**
```go
func swap(a, b *int) {
    temp := *a
    *a = *b
    *b = temp
}

func main() {
    x, y := 5, 10
    swap(&x, &y)
    fmt.Println("x:", x, "y:", y)
}
```

---

### 1.8 Strings
- Immutable, UTF-8 encoded.
- Concatenation: `+`

**Example:**
```go
str := "Hello, " + "World!"
fmt.Println(str)
```

**Practice Question:**
1. Write a program to reverse a string.

**Answer:**
```go
func reverse(s string) string {
    runes := []rune(s)
    for i, j := 0, len(runes)-1; i < j; i, j = i+1, j-1 {
        runes[i], runes[j] = runes[j], runes[i]
    }
    return string(runes)
}

func main() {
    str := "GoLang"
    fmt.Println(reverse(str))
}
```

---

### 1.9 `if-else`, `switch`, `for loop`
- No parentheses around conditions.
- `switch` supports ranges and does not fall through by default.

**Example:**
```go
if x := 10; x > 5 {
    fmt.Println("x is greater than 5")
}
```

**Practice Question:**
1. Write a program using `switch` with ranges.

**Answer:**
```go
func main() {
    score := 75
    switch {
    case score >= 90:
        fmt.Println("Grade: A")
    case score >= 80:
        fmt.Println("Grade: B")
    case score >= 70:
        fmt.Println("Grade: C")
    default:
        fmt.Println("Grade: F")
    }
}
```

---

### 1.10 Iterations
- `for` is the only looping construct.
- Supports:
  1. C-style: `for i := 0; i < 10; i++`
  2. Range: `for index, value := range slice`

**Practice Question:**
1. Write a `for` loop to compute the sum of an array.

**Answer:**
```go
func main() {
    nums := []int{1, 2, 3, 4, 5}
    sum := 0
    for _, num := range nums {
        sum += num
    }
    fmt.Println("Sum:", sum)
}
```

---

### 1.11 Using `break` and `continue`
- `break`: Exits the loop.
- `continue`: Skips the current iteration.

**Example:**
```go
for i := 0; i < 10; i++ {
    if i%2 == 0 {
        continue
    }
    fmt.Println(i)
}
```

**Practice Question:**
1. Use `break` to exit a loop upon finding a specific value in an array.

**Answer:**
```go
func main() {
    nums := []int{1, 2, 3, 4, 5}
    target := 3
    for _, num := range nums {
        if num == target {
            fmt.Println("Found target:", num)
            break
        }
    }
}
```

---

## Note by Author - Stuti
This unit introduces fundamental Go concepts while drawing parallels to C for familiarity. Complete the practice questions and experiment with code 
