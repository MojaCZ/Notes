* a function declaration has a name, a list of parameters, an optional list of results, and a body
* Go has no concept of default parameter values

```go
func name(parameter-list) (result-lsit) {
  body
}
```

# Function Values
A function value may be called like any other function.
```go
func square(n int) int { return n * n }
f := square
fmt.Println(f(3))
```

# Anonimous Functions
A function literal is written like a function declaration. but without a name following the func keyword.
Function defined in this way have access to the entire lexical environment (inner function can refer to variables from the enclosing functoion)
```go
func squares() func() int {
  var x int
  return func() int {
    x++
    return x * x
  }

}
```

# Variadic Functions
Can be called with varying numbers of arguments.

```go
func sum(vals ...int) int {
  total := 0
  for _, val := range vals {
    total += val
  }
  return total
}
```

# Panic
During a typical panic, normal execution stops all deferred function calls in **that gorutine** are executed, and the program crashes with a log message.
`panic(fmt.Sprintf("invalid suit %q", s))`

# Recover
A web server that encounters an unexpected problem could close the connection rather than leave the client hanging.

**Recover** function is called within a deferred function and the function containing the **defer** statement is panicking, recover ends the current state of panic and returns the panic value.

```go
func Parse(input string) (s *Syntax, err error) {
  defer func() {
    if p := recover(); p != nil {
      err = fmt.Errorf("internal error: %v", p)
    }
  }()
}
```
