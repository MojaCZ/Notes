# Concurrency
not equal parallel

=> Breaking up the program into independently executable tascs whitch can run at the same time.

ex.1. I have clock and I want to send to client each second time. If client requests connection I can process this concurrently so all clients can receive time


**gorutine** `go functionName()`
* will not wait for function to finish, run it at background and continue executin next line
* main function is also a gorutine, when it finishes, program will stop all gorutins init
```go
func main() {
  go count("people")
} // -> will do nothing because count will dies with the main
```

## sync.WaitGroup
```go
var wg sync.WaitGroup
go func() {
  functionName()
  wg.Done() // when function ends, decrease counter by 1
} ()
wg.Wait() // when wg counter at 0
```

## Channels
Like a pipe in whitch you can send or receiving a message.
Sending and receiving are **blocking** operations, one have to wait for another.
I can declare if chain should be sending or recieving with `<-chan`, `chan<-`

```go
func count(thing string, c chan string) {
  for i:=1; i<=5; i++ {
    c <- thing  // send thing to channel
  }
}

func main() {
  c := make(chan string)
  go count("sheep", c);
  msg := <- c // will receive one message and continue next line
  fmt.Println(msg);
}
```

Channels can be used for syncronizing gorutines (both sending and recieving side will wait for the opossite one)

gorutine1 gorutine2
...           ...
...           c <- "hi"
...           ...
msg := <- c   ...
...           ...
...           ...

### deadlock
runtime fatal error.
One of gorutines has finished while another is waiting for message from channel -> it will wait forever
```go
func main() {
  c := make (chan string, 2)
  c <- "hello"  // nothing to receive on the other side (yet), stops here
  msg := <- c
  fmt.Println(msg)
}
```

### close
`close(c)` - let the receiver know all is done.
Connection should not be closed by reciever (usually)
Closing **always** create a message
close message -> 0, false (0 for int as null value, opened? false)

- closing and then sending message -> PANIC
- closing twice -> PANIC

```go
msg, open := <- c // reciever finds this way all is done
if !open { break; }
```

```go
for msg := range c {  // nicer way to do this
  fmt.Println(msg)
}
```

### buffer
```go
c := make(chan string, 2)
c <- "Hallo"
c <- "World"
// c <- "Lukas" // this would cause deadlock
msg := <- c
fmt.Println(msg)
msg := <- c
fmt.Println(msg)
```

### Select
* first operation that is non blocking will be chosen
* if all cases are blocking, default executes
* select is like routing data
```go
func main() {
  c1 := make(chan string)
  c2 := make(chan string)
  go func() {
    for {
      c1 <- "Every 500ms"
      time.sleep(time.Milliseconds * 500)
    }
  }()
  go func() {
    for {
      c2 <- "Every two seconds"
      time.sleep(time.Second * 2)
    }
  }()
  for {
    fmt.Println(<- c1)  // even though c1 is ready sooner, it will block and wait for c2
    fmt.Println(<- c2)
  }
  for {
    select {  // nothing is blocking here
      case msg1 := <- c1:
        fmt.Println(msg1)
      case msg1 := <- c2:
        fmt.Println(msg2)
    }
  }
}
```

### Worker Pools
is pattern
```go
// values will be buffered, workers will be processing values one by one
func main() {
  jobs := make(chan int, 100)
  result := make(chan int, 100)
  go worker(jobs, result)
  go worker(jobs, result)
  for i:=0; i<100; i++ {
    jobs <- i
  }
  close(jobs)
  for j:=0; j<100; j++ {
    fmt.Println(<- result)
  }
  func worker(jobs <-chan int, result ->chan int) {
    for n:=range jobs {
      result <- fib(n)
    }
  }
  func fib(n int) {
    if n <= 1 {
      return n
    }
    return fib(n-1) + fib(n-2)
  }
}
```

### Patterns
#### Fan-out
like a load balance between workers
```go
func FanOut(In <-chan int, OutA, OutB chan int) {
  for data := range In {  // recieve untill closed
    select {  // send to first non blocking channel
      case OutA <- data:
      case OutB <- data:
    }
  }
}
```

#### Turn-out
```go
func TurnOur(InA, InB <-chan int, OutA, OutB chan<- int) {
  for{
    select {  // receive from first non-blocking
      case data, more = <- InA:
      case data, more = <- InB:
    }
    if !more {
      //...?
      return;
    }
    select{
      // FanOut here
    }
  }
}
// !!! if one of (InA, InB) are closed, select end here and not continue to another worker
// This could be solved with quit channels
```

### Quit Channel
```go
func TurnOut(Quit <-chan int, InA, InB <-chan int, OutA, OutB chan<- int){
  for {
    select {
      case data = <- InA:
      case data = <- InB:
      case <- Quit:
        close(InA)
        close(InB)
        FanOut(InA, OutA, OutB) // flush remainding data
        FanOut(InB, OutA, OutB)
        return
    }
  }
}
```

