***
# ✅ **Section 1: Basics**



#### **1. Values**

**What:** Basic literals like numbers, strings, booleans.
**Why:** Foundation for all operations.
**How:**

```go
package main
import "fmt"

func main() {
    fmt.Println("Hello")       // String
    fmt.Println(42)            // Integer
    fmt.Println(3.14)          // Float
    fmt.Println(true, false)   // Booleans
}
```

**Where:** Everywhere—variables, constants, function arguments.
**Alternatives (TypeScript):**

```typescript
console.log("Hello");
console.log(42);
console.log(3.14);
console.log(true, false);
```

**Pitfalls:** Go is strongly typed—no implicit type coercion like JS/TS.

***

#### **2. Variables**

**What:** Named storage for values.
**Why:** To reuse and manipulate data.
**How:**

```go
var name string = "Alice"
age := 30 // Short declaration
fmt.Println(name, age)
```

**Where:** Inside functions or globally.
**Alternatives (TypeScript):**

```typescript
let name: string = "Alice";
let age = 30;
```

**Pitfalls:** `:=` only works inside functions. Use `var` for package-level variables.

***

#### **3. Constants**

**What:** Immutable values.
**Why:** For fixed values like Pi or configuration.
**How:**

```go
const Pi = 3.14
```

**Where:** Anywhere you need a fixed value.
**Alternatives (TypeScript):**

```typescript
const Pi = 3.14;
```

**Pitfalls:** Cannot use `:=` for constants. Must assign at compile time.

***

#### **4. For**

**What:** The only looping construct in Go.
**Why:** Iteration over ranges, conditions.
**How:**

```go
for i := 0; i < 5; i++ {
    fmt.Println(i)
}
```

**Where:** Loops, ranges.
**Alternatives (TypeScript):**

```typescript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

**Pitfalls:** No `while` keyword—use `for` for everything.

***

#### **5. If/Else**

**What:** Conditional branching.
**Why:** Decision-making.
**How:**

```go
if x := 10; x > 5 {
    fmt.Println("Greater")
} else {
    fmt.Println("Smaller")
}
```

**Where:** Anywhere you need logic.
**Alternatives (TypeScript):**

```typescript
if (10 > 5) {
    console.log("Greater");
} else {
    console.log("Smaller");
}
```

**Pitfalls:** No ternary operator in Go.

***

#### **6. Switch**

**What:** Multi-way branching.
**Why:** Cleaner than multiple `if` statements.
**How:**

```go
switch day := "Mon"; day {
case "Mon":
    fmt.Println("Start of week")
default:
    fmt.Println("Other day")
}
```

**Where:** Handling enums, states.
**Alternatives (TypeScript):**

```typescript
switch ("Mon") {
    case "Mon":
        console.log("Start of week");
        break;
    default:
        console.log("Other day");
}
```

**Pitfalls:** Go `switch` does not require `break`—it stops automatically.

***