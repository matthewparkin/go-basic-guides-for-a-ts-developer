# ✅ **Section 3: Functions**

***

#### **1. Functions**

**What:** Named blocks of code that perform tasks.
**Why:** Reusability and modularity.
**How:**

```go
package main
import "fmt"

func greet(name string) string {
    return "Hello, " + name
}

func main() {
    fmt.Println(greet("Alice"))
}
```

**Where:** Everywhere—business logic, helpers.
**Alternatives (TypeScript):**

```typescript
function greet(name: string): string {
    return "Hello, " + name;
}
console.log(greet("Alice"));
```

**Pitfalls:** Go requires explicit return types; no default arguments.

***

#### **2. Multiple Return Values**

**What:** Functions can return more than one value.
**Why:** Common for returning result + error.
**How:**

```go
func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, fmt.Errorf("division by zero")
    }
    return a / b, nil
}

func main() {
    result, err := divide(10, 2)
    fmt.Println(result, err)
}
```

**Where:** File operations, network calls.
**Alternatives (TypeScript):**

```typescript
function divide(a: number, b: number): [number, string | null] {
    if (b === 0) return [0, "division by zero"];
    return [a / b, null];
}
```

**Pitfalls:** Always handle the second return value (error) in Go.

***

#### **3. Variadic Functions**

**What:** Functions that accept variable number of arguments.
**Why:** Flexible APIs.
**How:**

```go
func sum(nums ...int) int {
    total := 0
    for _, n := range nums {
        total += n
    }
    return total
}

func main() {
    fmt.Println(sum(1, 2, 3, 4))
}
```

**Where:** Logging, aggregation.
**Alternatives (TypeScript):**

```typescript
function sum(...nums: number[]): number {
    return nums.reduce((a, b) => a + b, 0);
}
```

**Pitfalls:** Variadic args must be last in Go.

***

#### **4. Closures**

**What:** Functions that capture variables from their environment.
**Why:** Useful for stateful functions.
**How:**

```go
func adder() func(int) int {
    sum := 0
    return func(x int) int {
        sum += x
        return sum
    }
}

func main() {
    add := adder()
    fmt.Println(add(1)) // 1
    fmt.Println(add(2)) // 3
}
```

**Where:** Counters, callbacks.
**Alternatives (TypeScript):**

```typescript
function adder(): (x: number) => number {
    let sum = 0;
    return (x) => (sum += x);
}
```

**Pitfalls:** Captured variables persist across calls—be mindful of concurrency.

***

#### **5. Recursion**

**What:** Function calling itself.
**Why:** Solving problems like factorial, tree traversal.
**How:**

```go
func factorial(n int) int {
    if n == 0 {
        return 1
    }
    return n * factorial(n-1)
}

func main() {
    fmt.Println(factorial(5)) // 120
}
```

**Where:** Algorithms, parsing.
**Alternatives (TypeScript):**

```typescript
function factorial(n: number): number {
    return n === 0 ? 1 : n * factorial(n - 1);
}
```

**Pitfalls:** Go does not optimise tail recursion—avoid deep recursion for large inputs.

***

### ✅ **Mini Comparison Table (Functions)**

| Feature          | Go Syntax                        | TypeScript Syntax                         |         |
| ---------------- | -------------------------------- | ----------------------------------------- | ------- |
| Basic Function   | `func greet(name string) string` | `function greet(name: string): string`    |         |
| Multiple Returns | `(float64, error)`               | \`\[number, string                        | null]\` |
| Variadic         | `func sum(nums ...int)`          | `function sum(...nums: number[])`         |         |
| Closure          | `func adder() func(int) int`     | `function adder(): (x: number) => number` |         |
| Recursion        | `func factorial(n int) int`      | `function factorial(n: number): number`   |         |

***
