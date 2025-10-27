## Overview

In Swift, you declare values using `var` for variables (mutable) and `let` for constants (immutable). Swift encourages immutability, so use `let` whenever possible.

---

## Constants (`let`)

Constants are values that cannot be changed after being set. Use `let` whenever possible - Swift encourages immutability.

```swift
let name = "John"
let age = 25
let pi = 3.14159
```

Once a constant is set, attempting to change it will result in a compilation error.

---

## Variables (`var`)

Variables can be changed after being set.

```swift
var score = 0
score = 10
score = score + 5  // score is now 15
```

---

## Type Annotations

Swift is a strongly-typed language. While it can infer types, you can explicitly declare them.

### Type Inference (Swift figures it out)

```swift
let city = "New York"  // Swift infers this is a String
let count = 42         // Swift infers this is an Int
```

### Explicit Type Annotations

```swift
let city: String = "New York"
let count: Int = 42
let price: Double = 19.99
let isActive: Bool = true
```

---

## Common Data Types

|Swift Type|Description|Example|
|---|---|---|
|`String`|Text values|`"Hello"`|
|`Int`|Whole numbers|`42`|
|`Double`|Decimal numbers (high precision)|`3.14159`|
|`Bool`|Boolean values|`true` / `false`|
|`Float`|Decimal numbers (lower precision)|`3.14`|

---

## Type Safety

Swift won't let you mix types without explicit conversion.

```swift
let age = 25
let message = "I am " + String(age) + " years old"
// Must convert Int to String explicitly
```

You cannot assign a value of one type to a variable of another type without explicit conversion.

---

## String Interpolation

A cleaner way to embed values in strings using `\(variable)` syntax.

```swift
let name = "Sarah"
let age = 28
let greeting = "Hello, \(name)! You are \(age) years old."
```

String interpolation is preferred over string concatenation as it's more readable and works with any type.

---

## Multiple Variable Declaration

```swift
let x = 10, y = 20, z = 30
var a = 1, b = 2, c = 3
```

---

## Naming Conventions

- Use **camelCase** for variable and constant names
- Start with lowercase letter
- Use descriptive names

```swift
let firstName = "John"
let userAge = 25
let isLoggedIn = true
```

---

## Quick Reference

✅ **Use `let` by default** - only use `var` when you know the value will change

✅ **Swift is type-safe** - you can't change types after declaration

✅ **Use string interpolation** `\(variable)` instead of concatenation

✅ **Semicolons are optional** - Swift doesn't require them