I LIKE:
* NO unused variables - forces me to write clean code without unused variables.
* forces me to handle errors
* field tags of structures (for JSON, database, ...) `Year int \`json:release\``

I DISLIKE:
* long errors handling
```go
// this is not possible
if l, err := ..., err != nil {
//...
}
```
* doesn't check if I reassigned variable or not. (two same variables different scope)
```go
var cwd string;
func init() {
  cwd, err := os.Getwd() // wrong, created new scope wariable cwd, package level cwd not changed
  if err...
}

func init() {
  var err error
  cwd, err = os.Getwd() // right, I just set cwd and err variables to new values, not created new one
  if err ...
}
```

SPECIAL
```go
if f, err := os.Open("some_file.txt"); err != nil { // error: unused: f
  return err
}
f.Start() // error: undefined f
f.Close() // error: undefined f
```