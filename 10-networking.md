### ✅ **Section 10: Networking & Processes**

This section covers **HTTP servers/clients**, **TCP**, **context for cancellations**, and **process management** in Go.

***

#### **1. HTTP Client**

**What:** Make HTTP requests using `net/http`.
**Why:** Consume APIs.
**How:**

```go
package main
import (
    "fmt"
    "net/http"
    "io/ioutil"
)

func main() {
    resp, err := http.Get("https://example.com")
    if err != nil {
        panic(err)
    }
    defer resp.Body.Close()
    body, _ := ioutil.ReadAll(resp.Body)
    fmt.Println(string(body))
}
```

**Alternatives (TypeScript):**

```typescript
const res = await fetch("https://example.com");
const body = await res.text();
console.log(body);
```

**Pitfalls:** Always `defer resp.Body.Close()` to avoid leaks.

***

#### **2. HTTP Server**

**What:** Serve HTTP requests.
**Why:** Build APIs and web apps.
**How:**

```go
import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "Hello, World!")
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}
```

**Alternatives (TypeScript):**
Express.js:

```typescript
import express from "express";
const app = express();
app.get("/", (req, res) => res.send("Hello, World!"));
app.listen(8080);
```

**Pitfalls:** `ListenAndServe` blocks; run in goroutine if needed.

***

#### **3. TCP Server**

**What:** Low-level networking.
**Why:** Custom protocols, streaming.
**How:**

```go
import (
    "net"
    "fmt"
)

func main() {
    ln, _ := net.Listen("tcp", ":9000")
    for {
        conn, _ := ln.Accept()
        go func(c net.Conn) {
            fmt.Fprintln(c, "Hello TCP")
            c.Close()
        }(conn)
    }
}
```

**Alternatives (TypeScript):**
Node.js `net` module:

```typescript
import net from "net";
net.createServer(socket => socket.write("Hello TCP")).listen(9000);
```

***

#### **4. Context**

**What:** Manage cancellations and timeouts.
**Why:** Graceful shutdowns, request deadlines.
**How:**

```go
import (
    "context"
    "time"
    "fmt"
)

func main() {
    ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
    defer cancel()
    select {
    case <-ctx.Done():
        fmt.Println("Timeout:", ctx.Err())
    }
}
```

**Alternatives (TypeScript):**
AbortController:

```typescript
const controller = new AbortController();
setTimeout(() => controller.abort(), 2000);
```

***

#### **5. Spawning Processes**

**What:** Run external commands.
**How:**

```go
import (
    "os/exec"
    "fmt"
)

func main() {
    out, _ := exec.Command("echo", "Hello").Output()
    fmt.Println(string(out))
}
```

**Alternatives (TypeScript):**
Node.js `child_process`:

```typescript
import { execSync } from "child_process";
console.log(execSync("echo Hello").toString());
```

***

#### **6. Exec’ing Processes**

**What:** Replace current process.
**How:**

```go
exec.Command("ls").Run()
```

***

#### **7. Signals**

**What:** Handle OS signals (e.g., SIGINT).
**How:**

```go
import (
    "os"
    "os/signal"
    "fmt"
)

func main() {
    sigs := make(chan os.Signal, 1)
    signal.Notify(sigs, os.Interrupt)
    <-sigs
    fmt.Println("Received interrupt")
}
```

**Alternatives (TypeScript):**

```typescript
process.on("SIGINT", () => console.log("Received interrupt"));
```

***

#### **8. Exit**

**What:** Terminate program.
**How:**

```go
os.Exit(1)
```

**Alternatives (TypeScript):**

```typescript
process.exit(1);
```

***

### ✅ **Mini Comparison Table (Networking & Processes)**

| Feature       | Go Syntax                           | TypeScript Syntax               |
| ------------- | ----------------------------------- | ------------------------------- |
| HTTP Client   | `http.Get("url")`                   | `fetch("url")`                  |
| HTTP Server   | `http.HandleFunc("/", handler)`     | `express.get("/", handler)`     |
| TCP Server    | `net.Listen("tcp", ":9000")`        | `net.createServer()`            |
| Context       | `context.WithTimeout()`             | `AbortController`               |
| Spawn Process | `exec.Command("cmd").Output()`      | `child_process.execSync("cmd")` |
| Signals       | `signal.Notify(sigs, os.Interrupt)` | `process.on("SIGINT", ...)`     |

***