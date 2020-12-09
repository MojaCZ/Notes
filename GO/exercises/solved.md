# Basic
1) declare single empty variable `a`
2) declare a set of variables `b`
3) swap values `a` `b`
4) create pointer variable `pb` pointing to `b` (print pointer + value pointer is pointing)
5) change variable b with pointer (print new variable)
6) create new variable `p` with `new` and print its value

# Basic types
1) create uint2 and int8 and let it overflow (in print)
2) create string variable and the second which will be part of it
3) what is Immutability?
4) var `o := 0600`  fmt.Printf %d, %o, %x, %X, [1], #
5) create string and a variable of type slice of byte, pass the string to slice of bytes and than back

# Arrays
1) create empty array len 3 and assign values `1, 2, 3` (with var)
2) shorthand assign array (not specified len) and assign `1, 2, 3, 4`
3) as 2 but assign key values `USD = '$', EUR = '€'`
4) as 2 but item on 99 will be -1
5) print all items in array
6) create function and pass array so you can set all items to `1`
  
# Slices
1) what are components of slices
2) create new slice of ints
3) create new slice of type T with specific length
4) 3) and specific capacity
5) print out pointer, length and cappacity of slice
6) create function, pass slice and change all its items to 1
7) add one item to slice

# Maps
1) init ages map (string number) with make 
2) init ages map with map keyword
3) init ages map with map and add first two people
4) remove one name from ages map

# Structs
1) create Employee type (ID, Name, Address) and assign some variable
2) add Method to print Employee
3) add Method so you can modifie Employee
4) create constructor for employee

# Function
1) write function that will run at init of package
2) create a variable and a function, pass this variable to function and change it within body (print before and after)
3) create a function, assign it to variable and run
4) create a function and run it straight away
5) create function that can take an varying number of arguments
6) use panic to exit main and write a message
7) use recover to escape panic

# Concurrency basic
1) create new go rutine
2) create wait group and run one go rutine twice, main will wate

# Channels
1) What is it mean that channel is blocking operation
2) write a function count which will except string and channel, loop 5 times and each time return string, in main read one value and print it
3) show deadlock in simple main without gorutines
4) keep receiving from count and print all from channel, close connection when counting done
5) use range to do the same from 4)
6) create channel as buffer strinig 2, write two values and than read two values
7) write two channels, two gorutines (one will write 500ms second 2000ms), in main create infinite loop, read and print connections
8) do the 7) with select without blocking

# Worker pools
1) create buffer channels int 100
2) create worker (will process value)
3) create two gorutines workers
4) loop trough 100 and put something to jobs
5) close jobs
6) get results from channel and print them

# Fan-out
1) function will take input and two output channels
2) receive In untill closed (channels 5)
3) disperse work between workers

# Turn-out
1) function will take two In, two Out
2) infinite loop, select from Inputs
3) if channel closed return
4) select fron first select and fan out


# Repeate this:
1) multi variable declaration
2) create pointer and change value it is pointing
3) function takes a pointer and change value
4) array fixed len, len by assigned values, set one value of any len
5) loop array
6) shorthand slice, make slice of given len and cap
7) create map, delete from map
8) structure employee, create object employee, function to set employee name
9) constructor for employee
10) defer recover

...
1) `var a, b, c string`
2) `p := &a`, `*p = 10`
3) `func incr(p *int) { *p = 10 }`
4) `var a [5]int` `a:=[...]{1, 2, 3}` `r := [...]int{99: -1}`
5) `for i, v := range a {}`
6) `s := []int{}` `make([]int, len, cap)`
7) `m := map[string]int{name: 10}` `delete(m, "name")`
8) `type Employee struct {}` `peter := Employee{}` `func (e *Employee) SetName(name string) {}`
9) `func newEmployee(id, name string) *Employee {... return E}`
* 
```go
func Parse() {
  defer func() {
    if p := recover(): p != nil {
      err = fmt.Errorf("internal error: %v", p)
    }
  }
}
```

Concurrency
1) create variable of wait group, add, wait, done
2) create go rutine
3) create chan, create buffered chan
4) assign to function input and output channel
5) get values in loop

...
1) `var wg sync.WaitGroup` `defer wg.Done()` `wg.Add(1)` `wg.Wait()`
2) `go func(){}()`
3) `c := make(chan string)` `cBuf := make(chan string, 3)`
4) `func(Out chan<- string, In <-chan string){}`
* 
```go
select() {
  case msg1, ok := <- c1:
    if ! ok { return }
    fmt.Println("msg1", msg1)
  case msg2, ok := <- c1:
    if ! ok { return }
    fmt.Println("msg2", msg2)
}
```