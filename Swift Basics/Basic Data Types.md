## Overview

Swift has several built-in data types for storing different kinds of values. Understanding these types is crucial for writing efficient and type-safe code.

---

## Integers

### Int

The standard integer type. Use this for whole numbers in most cases.

```swift
let age: Int = 25
let temperature: Int = -5
let count: Int = 1000
```

### Int Variants

Swift provides specific-sized integers when you need precise control over memory:

```swift
let smallNumber: Int8 = 127        // -128 to 127
let mediumNumber: Int16 = 32767    // -32,768 to 32,767
let largeNumber: Int32 = 2147483647
let veryLarge: Int64 = 9223372036854775807
```

### Unsigned Integers

For positive numbers only (no negative values):

```swift
let positiveOnly: UInt = 100
let byte: UInt8 = 255             // 0 to 255
```

---

## Floating-Point Numbers

### Double

64-bit floating-point number. This is the default for decimal numbers.

```swift
let pi: Double = 3.14159265359
let price: Double = 99.99
```

- **Precision**: 15 decimal digits
- **Use when**: You need high precision or don't have a specific reason to use Float

### Float

32-bit floating-point number. Less precise but uses less memory.

```swift
let temperature: Float = 36.6
let ratio: Float = 0.75
```

- **Precision**: 6 decimal digits
- **Use when**: Memory efficiency is critical

---

## Boolean

Represents true or false values.

```swift
let isLoggedIn: Bool = true
let hasPermission: Bool = false
let isValid: Bool = true
```

Commonly used in conditional statements and logic:

```swift
let isAdult = age >= 18
let canVote = isAdult && hasCitizenship
```

---

## String

Used for text values. Strings in Swift are powerful and Unicode-compliant.

### Basic Strings

```swift
let name: String = "John Doe"
let message: String = "Hello, World!"
let emoji: String = "😊🎉"
```

### Multiline Strings

```swift
let poem = """
Roses are red,
Violets are blue,
Swift is awesome,
And so are you!
"""
```

### String Properties

```swift
let text = "Swift"
let length = text.count           // 5
let isEmpty = text.isEmpty        // false
```

### String Methods

```swift
let greeting = "Hello, World!"

greeting.uppercased()             // "HELLO, WORLD!"
greeting.lowercased()             // "hello, world!"
greeting.hasPrefix("Hello")       // true
greeting.hasSuffix("!")           // true
greeting.contains("World")        // true
```

### String Interpolation

```swift
let name = "Alice"
let age = 30
let message = "My name is \(name) and I'm \(age) years old."
```

---

## Character

Represents a single character.

```swift
let letter: Character = "A"
let symbol: Character = "$"
let emoji: Character = "🎈"
```

You can iterate through a string's characters:

```swift
let word = "Swift"
for char in word {
    print(char)
}
```

---

## Type Conversion

Swift requires explicit type conversion between different types.

### Number Conversions

```swift
let integer: Int = 42
let double: Double = Double(integer)      // 42.0
let float: Float = Float(integer)         // 42.0

let decimal: Double = 3.14
let rounded: Int = Int(decimal)           // 3 (truncates)
```

### String Conversions

```swift
let number = 42
let numberString = String(number)         // "42"

let text = "123"
let value = Int(text)                     // Optional(123)
```

### Boolean Conversions

```swift
let isTrue = true
let boolString = String(isTrue)           // "true"
```

---

## Type Aliases

Create custom names for existing types to make code more readable.

```swift
typealias Distance = Double
typealias UserID = Int

let marathonDistance: Distance = 42.195
let currentUser: UserID = 12345
```

---

## Numeric Literals

Swift supports different number formats:

### Integer Literals

```swift
let decimal = 17
let binary = 0b10001          // 17 in binary
let octal = 0o21              // 17 in octal
let hexadecimal = 0x11        // 17 in hexadecimal
```

### Floating-Point Literals

```swift
let standard = 12.5
let exponential = 1.25e1      // 12.5
let hexFloat = 0xC.8p0        // 12.5 in hexadecimal
```

### Readable Numbers

Use underscores to make large numbers more readable:

```swift
let million = 1_000_000
let billion = 1_000_000_000
let creditCard = 1234_5678_9012_3456
```

---

## Min and Max Values

Every numeric type has min and max values:

```swift
let minInt = Int.min          // Smallest Int value
let maxInt = Int.max          // Largest Int value

let minInt8 = Int8.min        // -128
let maxInt8 = Int8.max        // 127

let minUInt = UInt.min        // 0
let maxUInt = UInt.max        // Largest UInt value
```

---

## Quick Reference

✅ **Use `Int` for integers** - unless you have a specific reason for sized variants

✅ **Use `Double` for decimals** - it's the default floating-point type

✅ **Strings are Unicode-compliant** - they handle emojis and international characters

✅ **Swift requires explicit type conversion** - no automatic conversion between types

✅ **Use underscores in large numbers** - for better readability