For every type T, the conversion operation T(x) converts value x to type T if the conversion is allowed.

# Integers
* `int8`, `int16`, `int32`, `int64`
* `uint8`, `uint16`, `uint32`, `uint64`
* int, uint (both either 32 or 64)
* `rune` is synonym for `int32`
* `byte` is synomym for `uint8`
* `uintptr` hold all the bits of a pointer value

int8 is -128 to 127
uint8 is 0 to 255

% applies only to integers, (-5%3 is same as -5%-3)

```go
var u uint8 = 255
fmt.Println(u, u+1, u*u) // 255 0 1
var i int8 = 127
fmt.Println(i, i+1, i*i) // 127 -128 1
```

# Floating numbers
`float32` or `float64`
`const e = 2.71828`
`const Avogadro = 6.02214129e23`
`const Planck = 6.62606957e-34`

# Strings
**immutable** sequence of bytes
`s[i:j]`, `s[:5]`, `s[7:]`, `s[:]`
`c := s[len(s)]`
Strings can be compared with == and <. It is done byte by byte -> natural lexicographic ordering.

Immutability: it is safe for two copies to share same underlying memory -> **cheap** for memory. If I make new copy `s[7:]` it shares the memory with s (new memory allocated).

*string literal* is a sequence of bytes enclosed in double quotes `"Hello"`

# fmt
integers `%d`, `%o`, `%x`
`[1]` use the first operand over and over again
`#` emit a 0
```go
o := 0600
fmt.Printf("%d %[1]o %#[1]o\n", o)  // 438 666 0666
x = int64(0xdeadbeef)
fmt.Printf("%d %[1]x %#[1]x %#[1]X/n", x)  // 3735928559 deadbeef 0xdeadbeef 0XDEADBEEF
```

runes `%c` and `%q`
floats `%g` `%e` `%f`
types `%t, %T`

# Strings and Byte Slice
mainly packages: `bytes`, `strings`, `strconv`, `unicode`

Because strings are immutable, building up strings incrementally takes a *lot of allocation and copying*. Thus it is more efficient to use the **bytes**.

```go
// strings with []byte conversions
s := "abc"
b := []byte(s)
s2 := string(b)
```

## buffer type
The *bytes* package provides the *Buffer type* for the efficient manipulation of byte slices.
The buffer starts empty but grows as data of types like `string`, `byte` and `[]byte`
```go
var buf bytes.Buffer
buf.WriteByte('[')
fmt.Fprintf(&buf, "%d", 10)
buf.WriteString(", ")
fmt.Fprintf(&buf, "%d", 20)
buf.WriteByte(']')  // [10, 20]
```

# Constants
Are expressions whose value is known to the compiler and whose evaluation is guaranteed to occur at compile time, not at run time.

**iota** begins with zero and increments by one for each item in the sequence