# Program Structure

Constants: `true` `false` `iota` `nil`

Types:
* `int` `int8` `int16` `int32` `int64`
* `uint` `uint8` `uint16` `uint32` `uint64` `uintptr`
* `float32` `float64` `complex128` `complex64`
* `bool` `byte` `rune` `string` `error`

Functions:
* `make` `len` `cap` `new` `append` `copy` `close` `delete`
* `complex` `real` `imag`
* `panic` `recover`

Declarations: `var` `const` `type` `func`

## Variables
A `var` declaration creates a variable of a particular tyle, attaches a name to it and sets its initial value
```go
// declar single variable
var name type = expression

// declar set of variables
var b, f, s = true, 2.3, "four"

// short hand notation
i, j := 0, 1
i := 26 // int
var f float64 = 26 // float64

// swap values
i, j := j, i
```

## Pointers
A pointer value is the address of a variable.

If a variable is declared `var x int`, the `&x` yields a pointer to an integer variable, that is, a value of type *int. The variable to which p points is written *p. The *p yields a value of that variable. Id *p is on the left side of assignment, the assignment updates the variable.

```go
x := 1 
p := &x // p, of type *int, points to x
fmt.Println(*p) // 1
*p = 2 // equivalent to x = 2
fmt.Println(x)  // 2

```