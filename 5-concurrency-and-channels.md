### ✅ **Section 5: Concurrency & Channels**

Go’s concurrency model is one of its strongest features, built around **goroutines** and **channels**. Let’s break down the key concepts:

***

#### **1. Goroutines**

**What:** Lightweight threads managed by the Go runtime.
**Why:** Efficient concurrency without manual thread management.
**How:**

```go
package main
import (
    "fmt"
    "time"
)

func say(msg string) {
    fmt.Println(msg)
}

func main() {
    go say("Hello") // Run concurrently
    time.Sleep(time.Second) // Wait for goroutine
}
```

**Where:** Parallel tasks, background jobs.
**Alternatives (TypeScript):**

```typescript
async function say(msg: string) {
    console.log(msg);
}
say("Hello"); // Runs asynchronously
```

**Pitfalls:** Goroutines don’t return values directly—use channels or sync primitives.

***

#### **2. Channels**

**What:** Typed conduits for communication between goroutines.
**Why:** Safe data sharing without explicit locks.
**How:**

```go
ch := make(chan string)
go func() { ch <- "Hello" }()
msg := <-ch
fmt.Println(msg)
```

**Where:** Producer-consumer patterns.
**Alternatives (TypeScript):**
TypeScript lacks built-in channels; use Promises or Observables.
**Pitfalls:** Unbuffered channels block until both sender and receiver are ready.

***

#### **3. Channel Buffering**

**What:** Channels with capacity.
**Why:** Reduce blocking when sending multiple values.
**How:**

```go
ch := make(chan int, 2)
ch <- 1
ch <- 2
fmt.Println(<-ch, <-ch)
```

**Pitfalls:** Sending beyond capacity blocks until space frees.

***

#### **4. Channel Synchronisation**

**What:** Use channels to signal completion.
**Why:** Coordinate goroutines.
**How:**

```go
done := make(chan bool)
go func() {
    fmt.Println("Working...")
    done <- true
}()
<-done
```

***

#### **5. Channel Directions**

**What:** Restrict channel usage in function signatures.
**Why:** Enforce send-only or receive-only semantics.
**How:**

```go
func send(ch chan<- int) { ch <- 1 }
func receive(ch <-chan int) { fmt.Println(<-ch) }
```

***

#### **6. Select**

**What:** Wait on multiple channel operations.
**Why:** Multiplex communication.
**How:**

```go
select {
case msg := <-ch1:
    fmt.Println("Received", msg)
case <-time.After(time.Second):
    fmt.Println("Timeout")
}
```

**Pitfalls:** `select` chooses a random ready case if multiple are ready.

***

#### **7. Timeouts**

**What:** Use `time.After` with `select`.
**Why:** Avoid blocking forever.
**How:**

```go
select {
case msg := <-ch:
    fmt.Println(msg)
case <-time.After(2 * time.Second):
    fmt.Println("Timeout")
}
```

***

#### **8. Non-Blocking Channel Operations**

**What:** Use `select` with `default`.
**Why:** Avoid blocking when channel isn’t ready.
**How:**

```go
select {
case ch <- 1:
    fmt.Println("Sent")
default:
    fmt.Println("Skipped")
}
```

***

#### **9. Closing Channels**

**What:** Signal no more values will be sent.
**Why:** Graceful termination.
**How:**

```go
close(ch)
```

**Pitfalls:** Don’t close from receiver side; only sender should close.

***

#### **10. Range over Channels**

**What:** Iterate until channel closes.
**How:**

```go
for v := range ch {
    fmt.Println(v)
}
```

***

#### **11. Timers & Tickers**

**What:** Schedule tasks.
**Why:** Delays and periodic execution.
**How:**

```go
timer := time.NewTimer(2 * time.Second)
<-timer.C // Wait for timer
ticker := time.NewTicker(time.Second)
for t := range ticker.C {
    fmt.Println("Tick at", t)
}
```

***

#### **12. Worker Pools**

**What:** Limit concurrency.
**Why:** Efficient resource usage.
**How:**

```go
jobs := make(chan int, 5)
results := make(chan int, 5)

for w := 1; w <= 3; w++ {
    go func(id int) {
        for j := range jobs {
            results <- j * 2
        }
    }(w)
}
```

***

#### **13. WaitGroups**

**What:** Wait for multiple goroutines to finish.
**How:**

```go
var wg sync.WaitGroup
wg.Add(2)
go func() { defer wg.Done(); fmt.Println("Task 1") }()
go func() { defer wg.Done(); fmt.Println("Task 2") }()
wg.Wait()
```

***

#### **14. Rate Limiting**

**What:** Control throughput.
**How:** Use `time.Tick` or buffered channels.

***

#### **15. Atomic Counters & Mutexes**

**What:** Safe shared state.
**How:**

```go
var count int32
atomic.AddInt32(&count, 1)
```

Or:

```go
var mu sync.Mutex
mu.Lock()
count++
mu.Unlock()
```

***

#### **16. Stateful Goroutines**

**What:** Encapsulate state in a goroutine.
**Why:** Avoid locks.
**How:**

```go
go func() {
    state := make(map[string]int)
    for {
        // handle requests via channels
    }
}()
```

***

### ✅ **Mini Comparison Table (Concurrency)**

| Feature   | Go Syntax                   | TypeScript Equivalent       |
| --------- | --------------------------- | --------------------------- |
| Goroutine | `go func() {}`              | `async/await`               |
| Channel   | `ch := make(chan int)`      | `Promise`, RxJS Observable  |
| Select    | `select { case <-ch: ... }` | `Promise.race()`            |
| WaitGroup | `sync.WaitGroup`            | `Promise.all()`             |
| Mutex     | `sync.Mutex`                | Manual locking (rare in JS) |

***
