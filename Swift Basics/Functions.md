## Overview

Functions are self-contained blocks of code that perform a specific task. They help organize code, make it reusable, and improve readability. Functions can take inputs (parameters), perform operations, and return outputs.

---

## Basic Function Syntax

### Function Declaration

```swift
func functionName() {
    // Code to execute
}
```

### Calling a Function

```swift
func greet() {
    print("Hello, World!")
}

greet()  // Output: "Hello, World!"
```

---

## Functions with Parameters

Parameters allow you to pass values into a function.

### Single Parameter

```swift
func greet(name: String) {
    print("Hello, \(name)!")
}

greet(name: "Alice")  // Output: "Hello, Alice!"
```

### Multiple Parameters

```swift
func greet(name: String, age: Int) {
    print("Hello, \(name)! You are \(age) years old.")
}

greet(name: "Bob", age: 25)
// Output: "Hello, Bob! You are 25 years old."
```

### Parameters with Default Values

```swift
func greet(name: String = "Guest") {
    print("Hello, \(name)!")
}

greet()              // Output: "Hello, Guest!"
greet(name: "Alice") // Output: "Hello, Alice!"
```

Multiple defaults:

```swift
func makeBooking(tickets: Int = 1, class: String = "Economy") {
    print("Booking \(tickets) ticket(s) in \(class)")
}

makeBooking()                           // Uses both defaults
makeBooking(tickets: 2)                 // Custom tickets, default class
makeBooking(tickets: 3, class: "First") // Both custom
```

---

## Return Values

Functions can return values using the `->` syntax.

### Basic Return

```swift
func add(a: Int, b: Int) -> Int {
    return a + b
}

let result = add(a: 5, b: 3)  // 8
```

### Implicit Return

For single-expression functions, you can omit the `return` keyword.

```swift
func multiply(a: Int, b: Int) -> Int {
    a * b  // Implicit return
}

let result = multiply(a: 4, b: 5)  // 20
```

### Returning Multiple Values (Tuples)

```swift
func getMinMax(numbers: [Int]) -> (min: Int, max: Int) {
    var minimum = numbers[0]
    var maximum = numbers[0]
    
    for number in numbers {
        if number < minimum {
            minimum = number
        }
        if number > maximum {
            maximum = number
        }
    }
    
    return (minimum, maximum)
}

let result = getMinMax(numbers: [3, 1, 8, 2, 9])
print("Min: \(result.min), Max: \(result.max)")
// Output: "Min: 1, Max: 9"

// Can also destructure
let (min, max) = getMinMax(numbers: [3, 1, 8, 2, 9])
print("Min: \(min), Max: \(max)")
```

### Optional Return Values

```swift
func findUser(id: Int) -> String? {
    if id == 1 {
        return "Alice"
    }
    return nil
}

if let user = findUser(id: 1) {
    print("Found user: \(user)")
} else {
    print("User not found")
}
```

### Returning Early

```swift
func checkAge(age: Int) -> String {
    if age < 0 {
        return "Invalid age"
    }
    
    if age < 18 {
        return "Minor"
    }
    
    return "Adult"
}
```

---

## Function Parameter Labels

### Argument Labels

By default, parameter names are used as argument labels when calling the function.

```swift
func greet(name: String, from hometown: String) {
    print("Hello, \(name) from \(hometown)!")
}

greet(name: "Alice", from: "New York")
```

Here, `name` and `from` are argument labels, while `name` and `hometown` are parameter names used inside the function.

### Omitting Argument Labels

Use an underscore `_` to omit the argument label.

```swift
func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}

add(5, 3)  // No labels needed
```

### Custom Argument Labels

```swift
func greet(person name: String) {
    print("Hello, \(name)!")
}

greet(person: "Bob")
// 'person' is the external label, 'name' is used internally
```

### When to Use What

```swift
// No label - for obvious operations
func sum(_ a: Int, _ b: Int) -> Int { a + b }
sum(5, 3)

// Same label and parameter name - clear and simple
func greet(name: String) { print("Hello, \(name)") }
greet(name: "Alice")

// Different labels - improves readability at call site
func send(message: String, to recipient: String) {
    print("Sending '\(message)' to \(recipient)")
}
send(message: "Hi!", to: "Bob")
```

---

## Variadic Parameters

Accept zero or more values of a specified type.

```swift
func sum(_ numbers: Int...) -> Int {
    var total = 0
    for number in numbers {
        total += number
    }
    return total
}

sum(1, 2, 3)        // 6
sum(10, 20, 30, 40) // 100
sum()               // 0
```

Another example:

```swift
func printNames(_ names: String...) {
    for name in names {
        print("Hello, \(name)!")
    }
}

printNames("Alice", "Bob", "Charlie")
```

**Note:** A function can have at most one variadic parameter.

---

## In-Out Parameters

By default, parameters are constants. Use `inout` to modify parameter values.

```swift
func incrementByTen(_ number: inout Int) {
    number += 10
}

var score = 50
incrementByTen(&score)  // Use & when passing
print(score)  // 60
```

**Important:** You must use `&` when passing a variable to an inout parameter.

Swapping values:

```swift
func swap(_ a: inout Int, _ b: inout Int) {
    let temp = a
    a = b
    b = temp
}

var x = 5
var y = 10
swap(&x, &y)
print("x: \(x), y: \(y)")  // x: 10, y: 5
```

**Note:** You cannot pass constants or literals to inout parameters.

---

## Function Types

Functions have types based on their parameter and return types.

```swift
func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}

// Function type: (Int, Int) -> Int
```

### Storing Functions in Variables

```swift
func multiply(_ a: Int, _ b: Int) -> Int {
    return a * b
}

let mathOperation: (Int, Int) -> Int = multiply
let result = mathOperation(4, 5)  // 20
```

### Functions as Parameters

Pass functions to other functions.

```swift
func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}

func subtract(_ a: Int, _ b: Int) -> Int {
    return a - b
}

func performOperation(_ a: Int, _ b: Int, operation: (Int, Int) -> Int) -> Int {
    return operation(a, b)
}

let sum = performOperation(10, 5, operation: add)      // 15
let diff = performOperation(10, 5, operation: subtract) // 5
```

### Functions as Return Types

Return a function from another function.

```swift
func makeIncrementer(incrementAmount: Int) -> (Int) -> Int {
    func incrementer(number: Int) -> Int {
        return number + incrementAmount
    }
    return incrementer
}

let incrementByFive = makeIncrementer(incrementAmount: 5)
let result = incrementByFive(10)  // 15
```

---

## Nested Functions

Functions can be defined inside other functions.

```swift
func calculateTotal(price: Double, quantity: Int) -> Double {
    func applyTax(amount: Double) -> Double {
        return amount * 1.08
    }
    
    let subtotal = price * Double(quantity)
    return applyTax(amount: subtotal)
}

let total = calculateTotal(price: 10.0, quantity: 3)  // 32.4
```

**Benefits:**

- Encapsulation - nested functions are only visible within the outer function
- Organization - keeps helper functions close to where they're used

---

## Closures (Brief Introduction)

Closures are self-contained blocks of code that can be passed around. Functions are actually special cases of closures.

### Basic Closure Syntax

```swift
let greet = { (name: String) -> String in
    return "Hello, \(name)!"
}

print(greet("Alice"))  // "Hello, Alice!"
```

### Closure as Function Parameter

```swift
let numbers = [1, 2, 3, 4, 5]

// Using a closure with map
let doubled = numbers.map { $0 * 2 }
print(doubled)  // [2, 4, 6, 8, 10]

// Using a closure with filter
let evenNumbers = numbers.filter { $0 % 2 == 0 }
print(evenNumbers)  // [2, 4]
```

### Trailing Closure Syntax

When a closure is the last parameter, you can write it outside the parentheses.

```swift
func performOperation(numbers: [Int], operation: (Int) -> Int) -> [Int] {
    var result: [Int] = []
    for number in numbers {
        result.append(operation(number))
    }
    return result
}

// Without trailing closure
let doubled1 = performOperation(numbers: [1, 2, 3], operation: { $0 * 2 })

// With trailing closure
let doubled2 = performOperation(numbers: [1, 2, 3]) { $0 * 2 }
```

---

## Guard in Functions

Use `guard` for early exits and input validation.

```swift
func greetUser(name: String?) {
    guard let userName = name else {
        print("No name provided")
        return
    }
    
    print("Hello, \(userName)!")
}

greetUser(name: "Alice")  // "Hello, Alice!"
greetUser(name: nil)      // "No name provided"
```

Multiple guards:

```swift
func processPayment(amount: Double?, accountBalance: Double?) {
    guard let paymentAmount = amount else {
        print("Invalid payment amount")
        return
    }
    
    guard let balance = accountBalance else {
        print("Unable to retrieve balance")
        return
    }
    
    guard balance >= paymentAmount else {
        print("Insufficient funds")
        return
    }
    
    print("Payment of $\(paymentAmount) processed")
}
```

---

## Throwing Functions

Functions that can throw errors must be marked with `throws`.

```swift
enum ValidationError: Error {
    case tooShort
    case tooLong
    case noUppercase
}

func validatePassword(_ password: String) throws -> Bool {
    guard password.count >= 8 else {
        throw ValidationError.tooShort
    }
    
    guard password.count <= 20 else {
        throw ValidationError.tooLong
    }
    
    return true
}

// Calling a throwing function
do {
    try validatePassword("abc")
    print("Password is valid")
} catch ValidationError.tooShort {
    print("Password is too short")
} catch ValidationError.tooLong {
    print("Password is too long")
} catch {
    print("Unknown error")
}
```

---

## Function Overloading

Multiple functions with the same name but different parameters.

```swift
func display(_ value: Int) {
    print("Integer: \(value)")
}

func display(_ value: String) {
    print("String: \(value)")
}

func display(_ value: Double) {
    print("Double: \(value)")
}

display(42)      // "Integer: 42"
display("Hello") // "String: Hello"
display(3.14)    // "Double: 3.14"
```

---

## Recursion

A function that calls itself.

```swift
func factorial(_ n: Int) -> Int {
    if n <= 1 {
        return 1
    }
    return n * factorial(n - 1)
}

print(factorial(5))  // 120 (5 × 4 × 3 × 2 × 1)
```

Fibonacci sequence:

```swift
func fibonacci(_ n: Int) -> Int {
    if n <= 1 {
        return n
    }
    return fibonacci(n - 1) + fibonacci(n - 2)
}

print(fibonacci(6))  // 8 (0, 1, 1, 2, 3, 5, 8)
```

**Caution:** Recursion can be memory-intensive. Use carefully and ensure there's a base case to stop the recursion.

---

## Common Patterns

### Validation Pattern

```swift
func createUser(name: String?, email: String?, age: Int?) -> Bool {
    guard let userName = name, !userName.isEmpty else {
        print("Name is required")
        return false
    }
    
    guard let userEmail = email, userEmail.contains("@") else {
        print("Valid email is required")
        return false
    }
    
    guard let userAge = age, userAge >= 18 else {
        print("Must be 18 or older")
        return false
    }
    
    print("User created: \(userName)")
    return true
}
```

### Transformation Pattern

```swift
func convertTemperature(celsius: Double, to unit: String) -> Double? {
    switch unit.lowercased() {
    case "fahrenheit":
        return celsius * 9/5 + 32
    case "kelvin":
        return celsius + 273.15
    default:
        return nil
    }
}

if let fahrenheit = convertTemperature(celsius: 100, to: "Fahrenheit") {
    print("\(fahrenheit)°F")
}
```

### Factory Pattern

```swift
func makeGreeting(for timeOfDay: String) -> String {
    switch timeOfDay {
    case "morning":
        return "Good morning!"
    case "afternoon":
        return "Good afternoon!"
    case "evening":
        return "Good evening!"
    default:
        return "Hello!"
    }
}

let greeting = makeGreeting(for: "morning")
```

### Calculator Pattern

```swift
func calculate(_ operation: String, _ a: Double, _ b: Double) -> Double? {
    switch operation {
    case "+":
        return a + b
    case "-":
        return a - b
    case "*":
        return a * b
    case "/":
        return b != 0 ? a / b : nil
    default:
        return nil
    }
}

if let result = calculate("+", 10, 5) {
    print(result)  // 15.0
}
```

---

## Documentation Comments

Use documentation comments to describe your functions.

```swift
/// Calculates the area of a rectangle
/// - Parameters:
///   - width: The width of the rectangle
///   - height: The height of the rectangle
/// - Returns: The area as a Double
func calculateArea(width: Double, height: Double) -> Double {
    return width * height
}
```

---

## Best Practices

### ✅ DO:

- Give functions clear, descriptive names that indicate what they do
- Keep functions focused on a single task
- Use parameters instead of global variables
- Use `guard` for early validation and exits
- Return early when possible to reduce nesting
- Use meaningful parameter names
- Document complex functions
- Use default parameter values to simplify function calls

### ❌ DON'T:

- Don't make functions too long (keep them concise)
- Don't use too many parameters (consider using a struct/tuple if needed)
- Don't modify global state within functions when possible
- Don't use `inout` parameters unless necessary
- Avoid deeply nested function calls
- Don't ignore return values that indicate errors

---

## Naming Conventions

### Function Names

Use **verb phrases** in camelCase:

```swift
func calculateTotal() { }
func sendMessage() { }
func validateInput() { }
func getUserData() { }
```

### Boolean Functions

Start with words like `is`, `has`, `should`, `can`:

```swift
func isValid() -> Bool { }
func hasPermission() -> Bool { }
func shouldUpdate() -> Bool { }
func canProceed() -> Bool { }
```

### Parameter Names

```swift
// ✅ Good - clear and descriptive
func send(message: String, to recipient: String) { }
func calculate(price: Double, with discount: Double) { }

// ❌ Bad - unclear
func send(msg: String, rec: String) { }
func calc(p: Double, d: Double) { }
```

---

## Quick Reference

✅ **Basic function:** `func name() { }`  
✅ **With parameters:** `func name(param: Type) { }`  
✅ **With return:** `func name() -> Type { return value }`  
✅ **Default parameters:** `func name(param: Type = default) { }`  
✅ **Multiple returns:** `func name() -> (Type, Type) { }`  
✅ **Omit label:** `func name(_ param: Type) { }`  
✅ **Custom label:** `func name(label param: Type) { }`  
✅ **Variadic:** `func name(_ params: Type...) { }`  
✅ **Inout:** `func name(_ param: inout Type) { }`  
✅ **Throwing:** `func name() throws -> Type { }`

---

## Key Takeaways

1. **Functions organize and reuse code** - write once, use many times
2. **Parameters make functions flexible** - pass different values for different results
3. **Return values provide results** - functions can give back data
4. **Use guard for validation** - check requirements early and exit if needed
5. **Argument labels improve readability** - make function calls clear at the call site
6. **Functions are first-class citizens** - can be stored, passed, and returned
7. **Keep functions focused** - each function should do one thing well
8. **Default parameters simplify calls** - provide sensible defaults when appropriate