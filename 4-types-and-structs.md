# ✅ **Section 4: Types & Structs**

***

#### **1. Pointers**

**What:** Variables that store memory addresses of other variables.
**Why:** Efficient memory usage, avoid copying large structs.
**How:**

```go
package main
import "fmt"

func main() {
    x := 10
    p := &x
    fmt.Println(*p) // Dereference
    *p = 20
    fmt.Println(x)  // 20
}
```

**Where:** Passing large data to functions, modifying state.
**Alternatives (TypeScript):**  
TypeScript does not have pointers; everything is reference by default for objects.
**Pitfalls:** No pointer arithmetic in Go; safe by design.

***

#### **2. Strings and Runes**

**What:** Strings are UTF-8 sequences; runes represent Unicode code points.
**Why:** Proper handling of text and characters.
**How:**

```go
s := "Hello"
fmt.Println(len(s))        // Bytes count
for i, r := range s {
    fmt.Printf("%d %c\n", i, r) // Rune iteration
}
```

**Where:** Text processing.
**Alternatives (TypeScript):**

```typescript
let s = "Hello";
console.log(s.length);
for (let c of s) console.log(c);
```

**Pitfalls:** `len(s)` returns bytes, not characters. Use `utf8.RuneCountInString`.

***

#### **3. Structs**

**What:** Custom composite types.
**Why:** Group related data.
**How:**

```go
type Person struct {
    Name string
    Age  int
}

func main() {
    p := Person{Name: "Alice", Age: 30}
    fmt.Println(p)
}
```

**Where:** Models, configurations.
**Alternatives (TypeScript):**

```typescript
interface Person {
    Name: string;
    Age: number;
}
let p: Person = { Name: "Alice", Age: 30 };
```

**Pitfalls:** No inheritance; use composition.

***

#### **4. Methods**

**What:** Functions with a receiver.
**Why:** Attach behaviour to types.
**How:**

```go
func (p Person) Greet() string {
    return "Hello, " + p.Name
}
```

**Where:** Object-like behaviour.
**Alternatives (TypeScript):**

```typescript
class Person {
    constructor(public Name: string) {}
    Greet() { return "Hello, " + this.Name; }
}
```

**Pitfalls:** Value receiver vs pointer receiver matters for mutability.

***

#### **5. Interfaces**

**What:** Define behaviour, not data.
**Why:** Polymorphism without inheritance.
**How:**

```go
type Greeter interface {
    Greet() string
}
```

**Where:** Dependency injection, abstractions.
**Alternatives (TypeScript):**

```typescript
interface Greeter { Greet(): string; }
```

**Pitfalls:** Implicit implementation—no `implements` keyword.

***

#### **6. Enums**

**What:** Go lacks native enums; use `const` + `iota`.
**Why:** Represent fixed sets.
**How:**

```go
const (
    Red = iota
    Green
    Blue
)
```

**Where:** States, options.
**Alternatives (TypeScript):**

```typescript
enum Color { Red, Green, Blue }
```

**Pitfalls:** `iota` resets in each `const` block.

***

#### **7. Struct Embedding**

**What:** Composition for reuse.
**Why:** Share fields and methods.
**How:**

```go
type Address struct { City string }
type Person struct {
    Name string
    Address
}
```

**Where:** Hierarchical data.
**Alternatives (TypeScript):**

```typescript
interface Address { City: string; }
interface Person extends Address { Name: string; }
```

**Pitfalls:** Field name conflicts require explicit qualification.

***

#### **8. Generics**

**What:** Type parameters introduced in Go 1.18.
**Why:** Write reusable code without sacrificing type safety.
**How:**

```go
func Printval T {
    fmt.Println(val)
}
```

**Where:** Collections, utilities.
**Alternatives (TypeScript):**

```typescript
function Print<T>(val: T): void {
    console.log(val);
}
```

**Pitfalls:** Constraints matter; avoid overcomplicating.

***

### ✅ **Mini Comparison Table (Types & Structs)**

| Feature   | Go Syntax                            | TypeScript Syntax                       |
| --------- | ------------------------------------ | --------------------------------------- |
| Pointer   | `p := &x; *p`                        | Not applicable                          |
| Struct    | `type Person struct { Name string }` | `interface Person { Name: string }`     |
| Method    | `func (p Person) Greet() string`     | `class Person { Greet(): string }`      |
| Interface | `type Greeter interface { Greet() }` | `interface Greeter { Greet(): string }` |
| Enum      | `const (Red = iota)`                 | `enum Color { Red, Green }`             |
| Generics  | `func Printval T`                    | `function Print<T>(val: T)`             |

***
