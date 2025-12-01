# ✅ **Section 8: Time & Utilities**

This section covers **time operations**, **random numbers**, **URL parsing**, and other handy utilities in Go.

***

#### **1. Time**

**What:** Go’s `time` package handles dates, durations, and clocks.
**Why:** Scheduling, timestamps, formatting.
**How:**

```go
package main
import (
    "fmt"
    "time"
)

func main() {
    now := time.Now()
    fmt.Println("Current time:", now)
}
```

**Alternatives (TypeScript):**

```typescript
console.log("Current time:", new Date());
```

**Pitfalls:** `time.Now()` returns local time; use `UTC()` if needed.

***

#### **2. Epoch**

**What:** Seconds since 1970-01-01 UTC.
**Why:** Common timestamp format.
**How:**

```go
epoch := time.Now().Unix()
fmt.Println(epoch)
```

**Alternatives (TypeScript):**

```typescript
console.log(Math.floor(Date.now() / 1000));
```

***

#### **3. Time Formatting / Parsing**

**What:** Convert time to string and back.
**Why:** Display and interpret dates.
**How:**

```go
layout := "2006-01-02 15:04:05" // Go's reference time
str := time.Now().Format(layout)
fmt.Println(str)

t, _ := time.Parse(layout, "2025-12-01 11:00:00")
fmt.Println(t)
```

**Alternatives (TypeScript):**

```typescript
let now = new Date();
console.log(now.toISOString());
```

**Pitfalls:** Go uses a **magic reference date** `2006-01-02 15:04:05` for layouts.

***

#### **4. Random Numbers**

**What:** Generate pseudo-random numbers.
**Why:** Simulations, sampling.
**How:**

```go
import (
    "fmt"
    "math/rand"
    "time"
)

func main() {
    rand.Seed(time.Now().UnixNano())
    fmt.Println(rand.Intn(100)) // 0–99
}
```

**Alternatives (TypeScript):**

```typescript
console.log(Math.floor(Math.random() * 100));
```

**Pitfalls:** Always seed with `time.Now().UnixNano()` for non-repeating sequences.

***

#### **5. Number Parsing**

**What:** Convert strings to numbers.
**How:**

```go
import "strconv"
n, _ := strconv.Atoi("42")
fmt.Println(n)
```

**Alternatives (TypeScript):**

```typescript
let n = parseInt("42");
```

**Pitfalls:** Handle errors when parsing invalid input.

***

#### **6. URL Parsing**

**What:** Parse and manipulate URLs.
**How:**

```go
import "net/url"
u, _ := url.Parse("https://example.com/path?query=1")
fmt.Println(u.Host, u.Path, u.Query())
```

**Alternatives (TypeScript):**

```typescript
let u = new URL("https://example.com/path?query=1");
console.log(u.host, u.pathname, u.searchParams);
```

***

#### **7. SHA256 Hashes**

**How:**

```go
import (
    "crypto/sha256"
    "fmt"
)
sum := sha256.Sum256([]byte("hello"))
fmt.Printf("%x\n", sum)
```

**Alternatives (TypeScript):**
Use Node.js `crypto`:

```typescript
import { createHash } from "crypto";
console.log(createHash("sha256").update("hello").digest("hex"));
```

***

#### **8. Base64 Encoding**

**How:**

```go
import "encoding/base64"
encoded := base64.StdEncoding.EncodeToString([]byte("hello"))
fmt.Println(encoded)
```

**Alternatives (TypeScript):**

```typescript
console.log(Buffer.from("hello").toString("base64"));
```

***

### ✅ **Mini Comparison Table (Time & Utilities)**

| Feature      | Go Syntax                                   | TypeScript Syntax                         |
| ------------ | ------------------------------------------- | ----------------------------------------- |
| Current Time | `time.Now()`                                | `new Date()`                              |
| Epoch        | `time.Now().Unix()`                         | `Date.now() / 1000`                       |
| Format       | `t.Format("2006-01-02")`                    | `date.toISOString()`                      |
| Random       | `rand.Intn(100)`                            | `Math.random() * 100`                     |
| Parse Int    | `strconv.Atoi("42")`                        | `parseInt("42")`                          |
| URL Parse    | `url.Parse("https://...")`                  | `new URL("https://...")`                  |
| SHA256       | `sha256.Sum256([]byte("hello"))`            | `crypto.createHash("sha256")`             |
| Base64       | `base64.StdEncoding.EncodeToString([]byte)` | `Buffer.from("hello").toString("base64")` |

***

