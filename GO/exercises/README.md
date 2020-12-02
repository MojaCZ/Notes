# Arrays
loop array
```go
for i, v := range a {
  fmt.Println(i, v)
}
```

pass pointer to function
```go
func zero(ptr *[32]byte) {
  for i := range ptr {
    ptr[i] = 0
  }
}
```