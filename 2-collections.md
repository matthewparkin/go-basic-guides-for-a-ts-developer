# ✅ **Section 2: Collections**

#### **Overview**
**What:** Data structures to hold multiple values.  
**Why:** Essential for managing groups of related data.
**Types Covered:** Arrays, Slices, Maps, Range iteration.

#### **1. Arrays**

**What:** Fixed-size sequence of elements of the same type.
**Why:** Useful when the size is known and does not change.
**How:**

```go
package main
import "fmt"

func main() {
    var arr [3]int = [3]int{1, 2, 3}
    fmt.Println(arr)
}
```

**Where:** Low-level operations, predictable memory usage.
**Alternatives (TypeScript):**

```typescript
let arr: number[] = [1, 2, 3];
console.log(arr);
```

**Pitfalls:** Size is part of the type in Go. `[3]int` ≠ `[4]int`.

***

#### **2. Slices**

**What:** Dynamic, flexible view into arrays.
**Why:** Preferred for most list operations in Go.
**How:**

```go
nums := []int{1, 2, 3}
nums = append(nums, 4)
fmt.Println(nums)
```

**Where:** Everywhere you need dynamic lists.
**Alternatives (TypeScript):**

```typescript
let nums: number[] = [1, 2, 3];
nums.push(4);
console.log(nums);
```

**Pitfalls:** Slices share underlying array—modifying one can affect others.

***

#### **3. Maps**

**What:** Key-value pairs.
**Why:** For fast lookups and associations.
**How:**

```go
m := map[string]int{"Alice": 25, "Bob": 30}
m["Charlie"] = 35
fmt.Println(m)
```

**Where:** Dictionaries, caches, configurations.
**Alternatives (TypeScript):**

```typescript
let m: Record<string, number> = { Alice: 25, Bob: 30 };
m["Charlie"] = 35;
console.log(m);
```

**Pitfalls:** Accessing a missing key returns zero value, not an error. Use `val, ok := m["key"]`.

***

#### **4. Range over Built-in Types**

**What:** Iterate over arrays, slices, maps, strings.
**Why:** Cleaner iteration.
**How:**

```go
nums := []int{1, 2, 3}
for i, v := range nums {
    fmt.Println(i, v)
}
```

**Where:** Loops over collections.
**Alternatives (TypeScript):**

```typescript
let nums = [1, 2, 3];
nums.forEach((v, i) => console.log(i, v));
```

**Pitfalls:** For maps, iteration order is random. For strings, `range` iterates runes, not bytes.

***

### ✅ **Mini Comparison Table (Collections)**

| Feature | Go Syntax               | TypeScript Syntax            |
| ------- | ----------------------- | ---------------------------- |
| Array   | `var arr [3]int`        | `let arr: number[]`          |
| Slice   | `nums := []int{1,2}`    | `let nums: number[] = [1,2]` |
| Map     | `map[string]int{"a":1}` | `Record<string, number>`     |
| Range   | `for i,v := range nums` | `nums.forEach((v,i)=>{})`    |

