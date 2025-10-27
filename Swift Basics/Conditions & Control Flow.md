## Overview

Control flow statements allow you to control the order in which your code executes. Swift provides several ways to make decisions and branch your code based on conditions.

---

## If Statements

The most basic form of conditional logic. Execute code only if a condition is true.

### Basic If

```swift
let temperature = 25

if temperature > 30 {
    print("It's hot!")
}
```

### If-Else

```swift
let age = 16

if age >= 18 {
    print("You can vote")
} else {
    print("You cannot vote yet")
}
```

### If-Else If-Else

Chain multiple conditions together.

```swift
let score = 85

if score >= 90 {
    print("Grade: A")
} else if score >= 80 {
    print("Grade: B")
} else if score >= 70 {
    print("Grade: C")
} else if score >= 60 {
    print("Grade: D")
} else {
    print("Grade: F")
}
```

### Multiple Conditions

Use logical operators to combine conditions.

```swift
let age = 25
let hasLicense = true

// AND operator (&&) - both must be true
if age >= 18 && hasLicense {
    print("You can drive")
}

// OR operator (||) - at least one must be true
let isWeekend = false
let isHoliday = true

if isWeekend || isHoliday {
    print("Time to relax!")
}

// NOT operator (!) - inverts the condition
let isRaining = false

if !isRaining {
    print("Let's go outside!")
}
```

### Nested If Statements

Place if statements inside other if statements.

```swift
let hasTicket = true
let hasID = true
let age = 20

if hasTicket {
    if hasID {
        if age >= 18 {
            print("Welcome to the venue!")
        } else {
            print("Sorry, you must be 18+")
        }
    } else {
        print("ID required")
    }
} else {
    print("Please purchase a ticket")
}
```

**Better approach using &&:**

```swift
if hasTicket && hasID && age >= 18 {
    print("Welcome to the venue!")
} else if !hasTicket {
    print("Please purchase a ticket")
} else if !hasID {
    print("ID required")
} else {
    print("Sorry, you must be 18+")
}
```

---

## Guard Statements

Used for early exits. Must include an `else` clause that exits the current scope.

### Basic Guard

```swift
func checkAge(age: Int?) {
    guard let userAge = age else {
        print("Age is required")
        return
    }
    
    // userAge is available for the rest of the function
    print("User is \(userAge) years old")
}

checkAge(age: 25)  // "User is 25 years old"
checkAge(age: nil) // "Age is required"
```

### Guard vs If Let

```swift
// Using if let (more nesting)
func processUser1(name: String?) {
    if let userName = name {
        // userName only available in this block
        print("Processing \(userName)")
        print("Validating \(userName)")
        print("Saving \(userName)")
    } else {
        print("Name required")
    }
}

// Using guard (cleaner, less nesting)
func processUser2(name: String?) {
    guard let userName = name else {
        print("Name required")
        return
    }
    
    // userName available for entire function
    print("Processing \(userName)")
    print("Validating \(userName)")
    print("Saving \(userName)")
}
```

### Multiple Guards

```swift
func createAccount(username: String?, email: String?, age: Int?) {
    guard let user = username else {
        print("Username required")
        return
    }
    
    guard let userEmail = email else {
        print("Email required")
        return
    }
    
    guard let userAge = age, userAge >= 18 else {
        print("Must be 18 or older")
        return
    }
    
    print("Creating account for \(user)")
    print("Email: \(userEmail)")
    print("Age: \(userAge)")
}
```

### Guard with Multiple Conditions

```swift
func processPayment(amount: Double?, balance: Double?) {
    guard let paymentAmount = amount,
          let accountBalance = balance,
          paymentAmount > 0,
          accountBalance >= paymentAmount else {
        print("Invalid payment")
        return
    }
    
    print("Processing payment of $\(paymentAmount)")
}
```

---

## Switch Statements

A powerful alternative to if-else chains. Matches a value against multiple possible patterns.

### Basic Switch

```swift
let dayOfWeek = 3

switch dayOfWeek {
case 1:
    print("Monday")
case 2:
    print("Tuesday")
case 3:
    print("Wednesday")
case 4:
    print("Thursday")
case 5:
    print("Friday")
case 6:
    print("Saturday")
case 7:
    print("Sunday")
default:
    print("Invalid day")
}
```

### No Implicit Fallthrough

Unlike some languages, Swift doesn't fall through to the next case automatically.

```swift
let number = 1

switch number {
case 1:
    print("One")
    // Automatically breaks here
case 2:
    print("Two")
default:
    print("Other")
}
// Output: "One"
```

### Multiple Values in a Case

```swift
let character = "a"

switch character {
case "a", "e", "i", "o", "u":
    print("Vowel")
case "b", "c", "d", "f", "g", "h":
    print("Consonant")
default:
    print("Other character")
}
```

### Range Matching

```swift
let score = 85

switch score {
case 0..<60:
    print("Grade: F")
case 60..<70:
    print("Grade: D")
case 70..<80:
    print("Grade: C")
case 80..<90:
    print("Grade: B")
case 90...100:
    print("Grade: A")
default:
    print("Invalid score")
}
```

### Tuple Matching

```swift
let point = (1, 1)

switch point {
case (0, 0):
    print("Origin")
case (_, 0):
    print("On the x-axis")
case (0, _):
    print("On the y-axis")
case (-2...2, -2...2):
    print("Inside the box")
default:
    print("Outside the box")
}
```

The underscore `_` matches any value.

### Value Binding

Bind matched values to temporary constants or variables.

```swift
let point = (2, 0)

switch point {
case (let x, 0):
    print("On the x-axis at x = \(x)")
case (0, let y):
    print("On the y-axis at y = \(y)")
case (let x, let y):
    print("At (\(x), \(y))")
}
// Output: "On the x-axis at x = 2"
```

Shorthand when binding both values:

```swift
case let (x, y):
    print("At (\(x), \(y))")
```

### Where Clause

Add additional conditions to cases.

```swift
let point = (1, -1)

switch point {
case let (x, y) where x == y:
    print("On the line x == y")
case let (x, y) where x == -y:
    print("On the line x == -y")
case let (x, y):
    print("Just at (\(x), \(y))")
}
// Output: "On the line x == -y"
```

Another example:

```swift
let temperature = 72

switch temperature {
case let temp where temp < 32:
    print("Freezing: \(temp)°F")
case let temp where temp < 60:
    print("Cold: \(temp)°F")
case let temp where temp < 80:
    print("Nice: \(temp)°F")
case let temp:
    print("Hot: \(temp)°F")
}
```

### Compound Cases

Multiple patterns in one case, separated by commas.

```swift
let character: Character = "e"

switch character {
case "a", "e", "i", "o", "u":
    print("Vowel")
default:
    print("Not a vowel")
}
```

### Fallthrough

Explicitly fall through to the next case (rare usage).

```swift
let number = 5

switch number {
case 5:
    print("Five")
    fallthrough
case 4:
    print("Four or less than six")
default:
    print("Other")
}
// Output:
// Five
// Four or less than six
```

### Switch with Enums

Switch is especially powerful with enums (you'll learn these later).

```swift
enum Weather {
    case sunny
    case cloudy
    case rainy
    case snowy
}

let today = Weather.sunny

switch today {
case .sunny:
    print("Wear sunglasses")
case .cloudy:
    print("Might rain")
case .rainy:
    print("Bring an umbrella")
case .snowy:
    print("Wear a coat")
}
```

### Switch Must Be Exhaustive

Every possible value must be handled. Use `default` if you don't want to handle all cases explicitly.

```swift
let number = 5

switch number {
case 1:
    print("One")
case 2:
    print("Two")
// ❌ ERROR: Switch must be exhaustive
}

// ✅ Fixed with default
switch number {
case 1:
    print("One")
case 2:
    print("Two")
default:
    print("Other number")
}
```

---

## Ternary Conditional Operator

A shorthand for simple if-else statements.

### Basic Syntax

```swift
// condition ? valueIfTrue : valueIfFalse

let age = 20
let status = age >= 18 ? "Adult" : "Minor"
print(status)  // "Adult"
```

### When to Use

Good for simple value assignments:

```swift
let score = 85
let passed = score >= 60 ? true : false

let temperature = 75
let weather = temperature > 80 ? "Hot" : "Nice"
```

### When Not to Use

Avoid for complex conditions (use if-else instead):

```swift
// ❌ Hard to read
let result = score >= 90 ? "A" : score >= 80 ? "B" : score >= 70 ? "C" : "F"

// ✅ Better with if-else
let grade: String
if score >= 90 {
    grade = "A"
} else if score >= 80 {
    grade = "B"
} else if score >= 70 {
    grade = "C"
} else {
    grade = "F"
}
```

---

## Combining Conditions

### Complex Logical Expressions

```swift
let age = 25
let hasLicense = true
let hasCar = true
let hasInsurance = false

if (age >= 18 && hasLicense) && (hasCar && hasInsurance) {
    print("Can drive legally")
} else {
    print("Cannot drive")
}

// Using grouping for clarity
let canDriveLegally = age >= 18 && hasLicense
let hasValidVehicle = hasCar && hasInsurance

if canDriveLegally && hasValidVehicle {
    print("Can drive legally")
}
```

### Short-Circuit Evaluation

Swift evaluates conditions from left to right and stops as soon as the result is determined.

```swift
// With AND (&&) - stops at first false
let age = 15
let hasLicense = true

if age >= 18 && hasLicense {  // age >= 18 is false, hasLicense never checked
    print("Can drive")
}

// With OR (||) - stops at first true
let isWeekend = true
let isHoliday = false

if isWeekend || isHoliday {  // isWeekend is true, isHoliday never checked
    print("Day off!")
}
```

---

## Pattern Matching with If Case

Use pattern matching without a full switch statement.

```swift
let age: Int? = 25

// Instead of:
if let unwrappedAge = age, unwrappedAge >= 18 {
    print("Adult")
}

// You can use if case:
if case let unwrappedAge? = age, unwrappedAge >= 18 {
    print("Adult")
}

// With ranges:
let score = 85

if case 80...100 = score {
    print("Great score!")
}
```

---

## Common Patterns

### Validation Pattern

```swift
func validateUser(age: Int?, email: String?) -> Bool {
    guard let userAge = age, userAge >= 18 else {
        print("Must be 18 or older")
        return false
    }
    
    guard let userEmail = email, userEmail.contains("@") else {
        print("Invalid email")
        return false
    }
    
    return true
}
```

### Configuration Pattern

```swift
let environment = "production"

switch environment {
case "development":
    print("Using dev database")
case "staging":
    print("Using staging database")
case "production":
    print("Using production database")
default:
    print("Unknown environment")
}
```

### Range Checking Pattern

```swift
let age = 25

switch age {
case 0..<13:
    print("Child")
case 13..<20:
    print("Teenager")
case 20..<65:
    print("Adult")
case 65...:
    print("Senior")
default:
    print("Invalid age")
}
```

---

## Best Practices

### ✅ DO:

- Use `guard` for early exits and to reduce nesting
- Use `switch` for multiple specific value checks
- Keep conditions simple and readable
- Use logical operators to combine related conditions
- Handle all possible cases in switch statements
- Use ranges in switch for number categorization

### ❌ DON'T:

- Don't use deeply nested if statements (use guard or combine conditions)
- Don't use ternary operator for complex logic
- Don't forget the `default` case in switch (unless using enums with all cases covered)
- Avoid redundant conditions
- Don't use force unwrapping in conditions when you can use optional binding

---

## Quick Reference

✅ **If statement:** `if condition { }`  
✅ **If-else:** `if condition { } else { }`  
✅ **If-else if:** `if condition1 { } else if condition2 { } else { }`  
✅ **Guard:** `guard condition else { return }`  
✅ **Switch:** `switch value { case pattern: code }`  
✅ **Ternary:** `condition ? true : false`  
✅ **Logical AND:** `condition1 && condition2`  
✅ **Logical OR:** `condition1 || condition2`  
✅ **Logical NOT:** `!condition`

---

## Key Takeaways

1. **If statements** are for simple conditional branching
2. **Guard statements** reduce nesting and make code cleaner
3. **Switch statements** are powerful for pattern matching and multiple cases
4. **Switch must be exhaustive** - handle all possible values
5. **Use logical operators** to combine multiple conditions
6. **Ternary operator** is great for simple value assignments
7. **Pattern matching** in switch is more powerful than simple value checking