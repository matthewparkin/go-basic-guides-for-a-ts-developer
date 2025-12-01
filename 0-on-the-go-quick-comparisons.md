# ✅ **GO - basics guide with examples and syntactic comparisons to typescript**

This is a concise guide to Go programming basics, complete with code examples and comparisons to TypeScript syntax for easier understanding.

Each section covers a fundamental concept in Go, explaining what it is, why it's used, how to implement it, where it's applicable, TypeScript alternatives, and common pitfalls to avoid. Typescript is used as that is my background, and I find it helpful to see parallels when learning a new language.

## Go by Example – Quick Reference Table

| Concept | What | Go Example | TypeScript Equivalent | Pitfalls |
|---------|------|------------|------------------------|----------|
| Hello World | Basic program output | `fmt.Println("Hello, World!")` | `console.log("Hello, World!")` | Must import `fmt` |
| Values | Basic literals | `fmt.Println(42, "Hi", true)` | `console.log(42, "Hi", true)` | Strong typing, no coercion |
| Variables | Named storage | `x := 10` | `let x = 10` | `:=` only inside functions |
| Constants | Immutable values | `const Pi = 3.14` | `const Pi = 3.14` | Compile-time only |
| For | Looping | `for i:=0; i<5; i++ {}` | `for (let i=0; i<5; i++) {}` | No `while` keyword |
| If/Else | Conditional | `if x>5 {}` | `if (x>5) {}` | No ternary operator |
| Switch | Multi-branch | `switch x {case 1:}` | `switch(x){case 1:}` | No `break` needed |
| Arrays | Fixed-size list | `var arr [3]int` | `let arr:number[]=[1,2,3]` | Size is part of type |
| Slices | Dynamic list | `nums := []int{1,2}` | `let nums:number[]=[1,2]` | Shared underlying array |
| Maps | Key-value store | `map[string]int{"a":1}` | `Record<string,number>` | Missing key returns zero |
| Functions | Reusable logic | `func add(a,b int) int` | `function add(a:number,b:number):number` | Explicit return types |
| Multiple Return Values | Return tuple | `(int,error)` | `[number,string|null]` | Always check error |
| Variadic Functions | Flexible args | `func sum(nums ...int)` | `function sum(...nums:number[])` | Must be last param |
| Closures | Capture state | `func adder() func(int) int` | `function adder(): (x:number)=>number` | Persistent state |
| Recursion | Self-call | `func fact(n int) int` | `function fact(n:number):number` | No tail recursion optimisation |
| Range over Built-in Types | Iterate | `for i,v := range slice` | `array.forEach((v,i)=>{})` | Map iteration order random |
| Pointers | Memory address | `p := &x; *p` | N/A | No pointer arithmetic |
| Strings and Runes | Text handling | `len(s)` | `s.length` | `len` counts bytes |
| Structs | Composite type | `type Person struct{Name string}` | `interface Person{Name:string}` | No inheritance |
| Methods | Behaviour on type | `func (p Person) Greet()` | `class Person { Greet() }` | Value vs pointer receiver |
| Interfaces | Behaviour contract | `type Greeter interface{Greet()}` | `interface Greeter{Greet():string}` | Implicit implementation |
| Enums | Fixed set | `const(Red=iota)` | `enum Color{Red,Green}` | `iota` resets per block |
| Struct Embedding | Composition | `type Person struct{Address}` | `interface Person extends Address` | Field conflicts |
| Generics | Type params | `func Print[T any](val T)` | `function Print<T>(val:T)` | Constraints required |
| Errors | Error handling | `errors.New("msg")` | `throw new Error("msg")` | Must check error |
| Custom Errors | Rich error | `type MyError struct{}` | `class MyError extends Error` | Implement `Error()` |
| Goroutines | Concurrency | `go func(){}` | `async/await` | No direct return |
| Channels | Communication | `ch := make(chan int)` | N/A | Blocking behaviour |
| Select | Multiplex | `select{case <-ch:}` | `Promise.race()` | Random ready case |
| Timeout | Limit wait | `time.After(2*time.Second)` | `AbortController` | Must use `select` |
| Mutex | Locking | `sync.Mutex` | Manual lock (rare) | Deadlocks possible |
| JSON | Encode/decode | `json.Marshal(obj)` | `JSON.stringify(obj)` | Use struct tags |
| XML | Encode/decode | `xml.Marshal(obj)` | Use XML libs | Tag mismatch errors |
| Time | Current time | `time.Now()` | `new Date()` | Layout magic date |
| Random Numbers | Generate | `rand.Intn(100)` | `Math.random()*100` | Seed for randomness |
| URL Parsing | Parse URL | `url.Parse("https://...")` | `new URL("https://...")` | Handle errors |
| SHA256 | Hash | `sha256.Sum256([]byte("hi"))` | `crypto.createHash("sha256")` | Use hex encoding |
| Base64 | Encode | `base64.StdEncoding.EncodeToString()` | `Buffer.from().toString("base64")` | Correct encoding |
| File Read | Read file | `os.ReadFile("file.txt")` | `fs.readFileSync()` | Handle errors |
| File Write | Write file | `os.WriteFile("file.txt",data,0644)` | `fs.writeFileSync()` | Permissions matter |
| Testing | Unit tests | `go test` | Jest/Mocha | `_test.go` suffix required |
| HTTP Client | Request | `http.Get("url")` | `fetch("url")` | Close response body |
| HTTP Server | Serve | `http.ListenAndServe(":8080",nil)` | `express.listen(8080)` | Blocks main thread |
| TCP Server | Socket | `net.Listen("tcp",":9000")` | `net.createServer()` | Manual protocol handling |
| Context | Cancellation | `context.WithTimeout()` | `AbortController` | Must propagate context |
| Signals | OS signals | `signal.Notify()` | `process.on("SIGINT")` | Graceful shutdown |
| Exit | Terminate | `os.Exit(1)` | `process.exit(1)` | Deferred funcs won't run |

***
