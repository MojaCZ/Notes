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

```go
// with the pointers, I can change variable in function
func incr(p *int) int {
  *p++ // increments what p points to; does not change p
  return *p
}
v := 1
incr(&v)  // v is now 2
fmt.Println(incr(&v)) // "3" and v is now 3
```

## New
Another way to create a variable. The expression `new(T)` creates an unnamed variable of type T, initializes it to zero value of T, and returns its address, which is a variable of type *T.
```go
p := new(int) // p, of type *int, points to an unnamed int variable
fmt.Println(*p) // "0"
*p = 2  // sets the unnamed variable int to 2
fmt.Println(*p) // "2"
```

## Variable lifetime
Is the interval of time in which it exists as the program executes. The package-level variable lives the entire execution of the program. The local variable lives untill it becomes *unreachable*, then it's storage may be recycled. The GO decides if the variable will be in stack or heap.

**stack**
* stores temporary variables created by function
* is a linear data structure
* can't be resized

**heap**
* stores global variables
* is a hierarchical data structure
* can be resized

## Type declarations
Defines a new named type that has the same underlying type as an existing type. Provides a way to seperate different and incompatible uses of underlying type so thay can't be mixed unintentionaly.

```go
type Celsius float64
type Fahrenheit float64
```

## Package initialization
1) package-level variables in the order thay are declared (dependencies first). In case of multiple files they are initialized in the orderin which thay are given to compiler.
2) init functions presented in files (in the order thay are declared) `func init() {...}`
3) packages are initilaized one by one from back (I need package to be init before using it)

## Scope
```go
if x := f(a); x == 0 {
  // do something
}
fmt.Println(x)  // x is undefined here
```

## escape loop
```go
for{break}

someName:
for {
  for{
    break someName
  }
}
```