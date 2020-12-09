# Arrays
`var a [3]int`
`var q [3]int = [3]int{1, 2, 3}`
`p := [...]int{1, 2, 3, 4}`
`symbol := [...]string{USD: '$', EUR: '€'}`
`r := [...]int{99: -1}`

```go
for i, v := range a {
  fmt.Println(i, v)
}
```

## passing array to function
array is passed as coppy, not the original -> *it is inefficient*. I have to pass pointer if I want change array within function.
```go
func zero(ptr *[32]byte) {
  for i := range ptr {
    ptr[i] = 0
  }
}
// you cannot pass *[16]byte
```

# Slices
Variable-length esquence whose elements all have the same type
has components: 
* pointer
* length `len()`
* capacity `cap()`

`s := []int{}`
`make([]T, len)`
`make([]T, len, cap)`

Slice contains a pointer to an element so **passing slice to a function allows to modify underlying elements**.
Copying a slice creates an alias for the underlying array.

Slices are not comparable.

## appending items
```go
var runes []rune
for _, r := range "Hello" {
  runes = append(runes, r)
}
```

# Maps
It is an unordered collection of key/value pairs. `map[K]V`

Map is a erference to a hash table.
`ages := make(map[string]int)`
`ages := map[string]int{}`
`delete(ages, "alice")`


```go
// or
ages := map[string]int {
  "alice": 31,
  "charlie": 34,
}

for name, age := range ages {
  fmt.Printf("%s\t%d\n", name, age)
}

ages["alice"] = 32
fmt.Println(ages["alice"])
delete(ages, "alice")
```

# Structs
Groups together zero or more named values of arbitraty types as a single entry. Each value is called a field.

A named struct type S can't declare a field of the same type S (an aggregate value cannot contain itself)

```go
type Employee struct {
  ID int
  Name string
  Address string
}
peter := Employee{
		ID:   123456,
    Name: "AHOJ",
    Address: "Prague"
	}
```

## Field tags
```go
Year int `json:"released"`
Color bool `json:"color,omitempty"`
```

## Methods
* Methids are done with **methods receiver**
* Go doesn't use *this* or *self*
* I call method with a selector (it selects the appropriate method from the receiver)
* We can define methods for any type

```go
func (p Point) Distance(q Point) float64 {
  return math.Hypot(q.X - p.X, q.Y-p.Y)
}
```

To update receiver variable, attach receiver to pointer type. If any method takes a pointer, all methods of that receiver should do so.
```go
func (p *Point) ScaleBy(factor float64) {
  p.X *= factor
  p.Y *= factor
}

r := &Point{1, 2}
r.ScaleBy(2)

p := Point{1, 2}
pptr := &p
pptr.ScaleBy(2)

q := Point{1, 2}
(&p).ScaleBy(2)
```

### Constructor
```go
type Thing struct {...}

func NewThing(someParameter string) *Thing {
  p := new(Thing)
  p.something = someParameter
  return p
}
```