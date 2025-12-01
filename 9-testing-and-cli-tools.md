# ✅ **Section 9: Testing & CLI Tools**

This section covers **testing**, **benchmarking**, and **command-line utilities** in Go.

***

#### **1. Testing**

**What:** Go has a built-in testing framework in the `testing` package.
**Why:** Validate code correctness.
**How:**
Create a file `math_test.go`:

```go
package main
import "testing"

func Add(a, b int) int { return a + b }

func TestAdd(t *testing.T) {
    got := Add(2, 3)
    want := 5
    if got != want {
        t.Errorf("got %d, want %d", got, want)
    }
}
```

Run:

```bash
go test
```

**Alternatives (TypeScript):**
Use Jest or Mocha:

```typescript
test("Add", () => {
    expect(2 + 3).toBe(5);
});
```

**Pitfalls:** Test files must end with `_test.go`.

***

#### **2. Benchmarking**

**What:** Measure performance.
**How:**

```go
func BenchmarkAdd(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Add(2, 3)
    }
}
```

Run:

```bash
go test -bench=.
```

***

#### **3. Command-Line Arguments**

**What:** Access arguments passed to the program.
**How:**

```go
import (
    "fmt"
    "os"
)

func main() {
    fmt.Println(os.Args) // ["program", "arg1", "arg2"]
}
```

**Alternatives (TypeScript):**
Node.js:

```typescript
console.log(process.argv);
```

***

#### **4. Command-Line Flags**

**What:** Parse named options.
**How:**

```go
import "flag"

var name = flag.String("name", "Guest", "Your name")
flag.Parse()
fmt.Println("Hello,", *name)
```

Run:

```bash
go run main.go --name Alice
```

**Alternatives (TypeScript):**
Use `yargs` or `commander`.

***

#### **5. Command-Line Subcommands**

**What:** Support multiple commands.
**How:** Use `flag.NewFlagSet` for each subcommand.

```go
startCmd := flag.NewFlagSet("start", flag.ExitOnError)
stopCmd := flag.NewFlagSet("stop", flag.ExitOnError)
```

***

#### **6. Environment Variables**

**What:** Read system environment variables.
**How:**

```go
val := os.Getenv("HOME")
fmt.Println(val)
```

**Alternatives (TypeScript):**

```typescript
console.log(process.env.HOME);
```

***

#### **7. Logging**

**What:** Use `log` package for structured output.
**How:**

```go
import "log"
log.Println("Info message")
log.Fatal("Fatal error") // exits
```

**Alternatives (TypeScript):**

```typescript
console.log("Info message");
```

**Pitfalls:** `log.Fatal` terminates the program immediately.

***

### ✅ **Mini Comparison Table (Testing & CLI)**

| Feature       | Go Syntax                             | TypeScript Syntax      |
| ------------- | ------------------------------------- | ---------------------- |
| Testing       | `go test` with `_test.go` files       | Jest/Mocha             |
| Benchmarking  | `func BenchmarkX(b *testing.B)`       | `console.time()`       |
| CLI Args      | `os.Args`                             | `process.argv`         |
| Flags         | `flag.String("name", "Guest", "...")` | `yargs` or `commander` |
| Env Variables | `os.Getenv("HOME")`                   | `process.env.HOME`     |
| Logging       | `log.Println("msg")`                  | `console.log("msg")`   |

***
