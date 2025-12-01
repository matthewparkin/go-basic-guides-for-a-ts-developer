# ✅ **Section 6: Errors & Panic Handling**

Error handling in Go is explicit and forms a core part of its design philosophy. Unlike TypeScript (or JavaScript), Go does not use exceptions for normal errors—errors are values.

***

#### **1. Errors**

**What:** Built-in `error` type represents failure conditions.
**Why:** Explicit error handling improves reliability.
**How:**

```go
package main
import (
    "errors"
    "fmt"
)

func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}

func main() {
    result, err := divide(10, 0)
    if err != nil {
        fmt.Println("Error:", err)
    } else {
        fmt.Println("Result:", result)
    }
}
```

**Where:** File I/O, network calls, parsing.
**Alternatives (TypeScript):**

```typescript
function divide(a: number, b: number): number {
    if (b === 0) throw new Error("division by zero");
    return a / b;
}
```

**Pitfalls:** Always check `err`—ignoring it is a common bug.

***

#### **2. Custom Errors**

**What:** Implement `error` interface for richer error types.
**Why:** Add context or structured data.
**How:**

```go
type MyError struct {
    Code int
    Msg  string
}

func (e MyError) Error() string {
    return fmt.Sprintf("Code %d: %s", e.Code, e.Msg)
}

func main() {
    err := MyError{Code: 404, Msg: "Not Found"}
    fmt.Println(err)
}
```

**Alternatives (TypeScript):**

```typescript
class MyError extends Error {
    constructor(public code: number, message: string) {
        super(message);
    }
}
```

**Pitfalls:** Ensure `Error()` returns a string—required by `error` interface.

***

#### **3. Panic**

**What:** Stops normal execution and unwinds the stack.
**Why:** For unrecoverable errors (e.g., corrupted state).
**How:**

```go
func main() {
    panic("Something went terribly wrong")
}
```

**Alternatives (TypeScript):**
Throwing an error:

```typescript
throw new Error("Something went terribly wrong");
```

**Pitfalls:** Use sparingly—panic is not for normal error handling.

***

#### **4. Defer**

**What:** Schedule a function to run after the current function completes.
**Why:** Resource cleanup (like `finally` in TS).
**How:**

```go
func main() {
    defer fmt.Println("Cleanup")
    fmt.Println("Doing work")
}
```

**Alternatives (TypeScript):**
Use `try/finally`:

```typescript
try {
    console.log("Doing work");
} finally {
    console.log("Cleanup");
}
```

**Pitfalls:** Deferred calls run even if panic occurs.

***

#### **5. Recover**

**What:** Regain control after a panic.
**Why:** Graceful shutdown.
**How:**

```go
func safe() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Recovered:", r)
        }
    }()
    panic("Oops!")
}

func main() {
    safe()
    fmt.Println("Continuing execution")
}
```

**Alternatives (TypeScript):**
No direct equivalent—use `try/catch`.
**Pitfalls:** Only works inside deferred functions.

***

### ✅ **Mini Comparison Table (Errors & Panic)**

| Feature      | Go Syntax                                   | TypeScript Syntax                   |
| ------------ | ------------------------------------------- | ----------------------------------- |
| Error        | `errors.New("msg")`                         | `throw new Error("msg")`            |
| Custom Error | `type MyError struct {}` + `Error()` method | `class MyError extends Error`       |
| Panic        | `panic("msg")`                              | `throw new Error("msg")`            |
| Defer        | `defer cleanup()`                           | `try { ... } finally { cleanup() }` |
| Recover      | `recover()` inside `defer`                  | `try/catch`                         |

***
