# ✅ **Section 7: Data Handling & I/O**

This section covers working with **structured data (JSON, XML)**, **files**, **templates**, and **text processing** in Go.

***

#### **1. JSON**

**What:** JavaScript Object Notation—common data format.
**Why:** APIs and data exchange.
**How:**

```go
package main
import (
    "encoding/json"
    "fmt"
)

type Person struct {
    Name string `json:"name"`
    Age  int    `json:"age"`
}

func main() {
    p := Person{Name: "Alice", Age: 30}
    data, _ := json.Marshal(p) // Encode
    fmt.Println(string(data))

    var p2 Person
    json.Unmarshal(data, &p2) // Decode
    fmt.Println(p2)
}
```

**Alternatives (TypeScript):**

```typescript
let p = { name: "Alice", age: 30 };
let data = JSON.stringify(p);
let p2 = JSON.parse(data);
```

**Pitfalls:** Always check `err` when marshalling/unmarshalling. Use struct tags for field names.

***

#### **2. XML**

**What:** Extensible Markup Language.
**Why:** Legacy systems, configuration.
**How:**

```go
import "encoding/xml"

type Note struct {
    To   string `xml:"to"`
    From string `xml:"from"`
}

data, _ := xml.Marshal(Note{To: "Alice", From: "Bob"})
fmt.Println(string(data))
```

**Pitfalls:** XML tags must match struct fields.

***

#### **3. Reading Files**

**What:** Read file contents into memory.
**How:**

```go
import "os"
content, err := os.ReadFile("file.txt")
fmt.Println(string(content))
```

**Alternatives (TypeScript):**
Node.js:

```typescript
import { readFileSync } from "fs";
let content = readFileSync("file.txt", "utf8");
```

**Pitfalls:** Handle errors and large files carefully.

***

#### **4. Writing Files**

**How:**

```go
os.WriteFile("file.txt", []byte("Hello"), 0644)
```

**Pitfalls:** Permissions matter (`0644` for read/write).

***

#### **5. Line Filters**

**What:** Process file line by line.
**How:**

```go
file, _ := os.Open("file.txt")
scanner := bufio.NewScanner(file)
for scanner.Scan() {
    fmt.Println(scanner.Text())
}
```

***

#### **6. File Paths & Directories**

**How:**

```go
import "path/filepath"
fmt.Println(filepath.Join("dir", "file.txt"))
```

***

#### **7. Temporary Files & Directories**

**How:**

```go
tmpFile, _ := os.CreateTemp("", "example")
fmt.Println(tmpFile.Name())
```

***

#### **8. Text Templates**

**What:** Generate text with dynamic data.
**How:**

```go
import "text/template"
tmpl := template.Must(template.New("msg").Parse("Hello, {{.Name}}"))
tmpl.Execute(os.Stdout, map[string]string{"Name": "Alice"})
```

**Alternatives (TypeScript):**
Use template literals:

```typescript
let name = "Alice";
console.log(`Hello, ${name}`);
```

***

#### **9. Regular Expressions**

**How:**

```go
import "regexp"
re := regexp.MustCompile(`\d+`)
fmt.Println(re.FindString("abc123"))
```

**Pitfalls:** Always validate regex compilation.

***

#### **10. Base64 Encoding**

**How:**

```go
import "encoding/base64"
encoded := base64.StdEncoding.EncodeToString([]byte("hello"))
fmt.Println(encoded)
```

***

#### **11. SHA256 Hashes**

**How:**

```go
import (
    "crypto/sha256"
    "fmt"
)
sum := sha256.Sum256([]byte("hello"))
fmt.Printf("%x\n", sum)
```

***

### ✅ **Mini Comparison Table (Data Handling)**

| Feature     | Go Syntax                                  | TypeScript Syntax             |
| ----------- | ------------------------------------------ | ----------------------------- |
| JSON Encode | `json.Marshal(obj)`                        | `JSON.stringify(obj)`         |
| JSON Decode | `json.Unmarshal(data, &obj)`               | `JSON.parse(data)`            |
| File Read   | `os.ReadFile("file.txt")`                  | `fs.readFileSync("file.txt")` |
| Template    | `template.New("msg").Parse("Hello {{.}}")` | `` `Hello ${name}` ``         |
| Regex       | `regexp.MustCompile("\\d+")`               | `/\d+/`                       |

***
