## Overview

Operators are special symbols that perform operations on values and variables. Swift supports arithmetic, comparison, logical, and other types of operators.

---

## Arithmetic Operators

Basic math operations on numbers.

```swift
let a = 10
let b = 3

let sum = a + b        // 13 (Addition)
let difference = a - b // 7  (Subtraction)
let product = a * b    // 30 (Multiplication)
let quotient = a / b   // 3  (Division)
let remainder = a % b  // 1  (Modulo/Remainder)
```

**Note:** Division with integers returns an integer (truncated).

```swift
let result = 10 / 3    // 3 (not 3.333...)
let precise = 10.0 / 3.0  // 3.333... (Double division)
```

---

## Compound Assignment Operators

Shorthand for modifying a variable using an operation.

```swift
var score = 10

score += 5   // score = score + 5  → 15
score -= 3   // score = score - 3  → 12
score *= 2   // score = score * 2  → 24
score /= 4   // score = score / 4  → 6
score %= 4   // score = score % 4  → 2
```

---

## Comparison Operators

Compare two values and return a `Bool` result.

|Operator|Meaning|Example|
|---|---|---|
|`==`|Equal to|`5 == 5` → `true`|
|`!=`|Not equal to|`5 != 3` → `true`|
|`>`|Greater than|`5 > 3` → `true`|
|`<`|Less than|`3 < 5` → `true`|
|`>=`|Greater than or equal|`5 >= 5` → `true`|
|`<=`|Less than or equal|`3 <= 5` → `true`|

```swift
let age = 18
let isAdult = age >= 18  // true
```

---

## Logical Operators

Combine or invert boolean values.

### AND Operator (`&&`)

Returns `true` only if **both** conditions are true.

```swift
let hasTicket = true
let hasID = true
let canEnter = hasTicket && hasID  // true
```

### OR Operator (`||`)

Returns `true` if **at least one** condition is true.

```swift
let isWeekend = false
let isHoliday = true
let canRelax = isWeekend || isHoliday  // true
```

### NOT Operator (`!`)

Inverts a boolean value.

```swift
let isRaining = false
let isSunny = !isRaining  // true
```

---

## Range Operators

Create ranges of values (useful for loops, which you'll learn later).

### Closed Range (`...`)

Includes both start and end values.

```swift
let range = 1...5  // 1, 2, 3, 4, 5
```

### Half-Open Range (`..<`)

Includes start but excludes end value.

```swift
let range = 1..<5  // 1, 2, 3, 4
```

---

## Ternary Conditional Operator

A shorthand for `if-else` statements (you'll learn these soon).

**Syntax:** `condition ? valueIfTrue : valueIfFalse`

```swift
let age = 20
let status = age >= 18 ? "Adult" : "Minor"  // "Adult"
```

This is equivalent to:

```swift
let status: String
if age >= 18 {
    status = "Adult"
} else {
    status = "Minor"
}
```

---

## Nil-Coalescing Operator (`??`)

Provides a default value for optionals (you'll learn about optionals soon).

```swift
let nickname: String? = nil
let displayName = nickname ?? "Guest"  // "Guest"
```

If `nickname` is `nil`, use `"Guest"` instead.

---

## Operator Precedence

Swift follows standard mathematical order of operations.

```swift
let result = 2 + 3 * 4  // 14 (not 20)
// Multiplication happens first: 3 * 4 = 12, then 2 + 12 = 14
```

Use parentheses to override precedence:

```swift
let result = (2 + 3) * 4  // 20
```

---

## String Operators

### Concatenation (`+`)

```swift
let greeting = "Hello, " + "World!"  // "Hello, World!"
```

### String Comparison

```swift
let name1 = "Alice"
let name2 = "Bob"
let isEqual = name1 == name2  // false
```

Remember: String interpolation `\(variable)` is preferred over concatenation.

---

## Quick Reference

✅ **Arithmetic:** `+`, `-`, `*`, `/`, `%`  
✅ **Compound Assignment:** `+=`, `-=`, `*=`, `/=`  
✅ **Comparison:** `==`, `!=`, `>`, `<`, `>=`, `<=`  
✅ **Logical:** `&&` (AND), `||` (OR), `!` (NOT)  
✅ **Ternary:** `condition ? true : false`  
✅ **Use parentheses** to control operator precedence