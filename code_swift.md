
# Example of Swift Code
```swift
import Foundation // Import a module

// MARK: - Variables and Constants
var mutableVariable: Int = 10 // Mutable variable
let immutableConstant: Double = 3.14 // Immutable constant

// MARK: - Functions
func greet(name: String) -> String {
    return "Hello, \(name)!" // String interpolation
}

// MARK: - Classes and Inheritance
class Animal {
    var name: String
    
    init(name: String) {
        self.name = name
    }
    
    func makeSound() {
        print("\(name) makes a sound")
    }
}

class Dog: Animal {
    override func makeSound() {
        print("\(name) says: Woof!")
    }
}

// MARK: - Structs
struct Point {
    var x: Int
    var y: Int
    
    func distance(to point: Point) -> Double {
        let dx = x - point.x
        let dy = y - point.y
        return sqrt(Double(dx * dx + dy * dy)) // Math functions
    }
}

// MARK: - Enums
enum Direction {
    case north, south, east, west
    
    func description() -> String {
        switch self {
        case .north: return "North"
        case .south: return "South"
        case .east: return "East"
        case .west: return "West"
        }
    }
}

// MARK: - Error Handling
enum CustomError: Error {
    case invalidInput
}

func validateInput(input: Int) throws {
    guard input > 0 else {
        throw CustomError.invalidInput
    }
}

// MARK: - Generics
func swapValues<T>(_ a: inout T, _ b: inout T) {
    let temp = a
    a = b
    b = temp
}

// MARK: - Example Usage
var dog = Dog(name: "Buddy")
dog.makeSound()

let point1 = Point(x: 0, y: 0)
let point2 = Point(x: 3, y: 4)
print("Distance: \(point1.distance(to: point2))")

let direction = Direction.east
print("Direction: \(direction.description())")

do {
    try validateInput(input: -5)
} catch {
    print("Error: \(error)")
}

var a = 5
```

# Specific Subjects
## Structs, Classes, and Enums
| Feature      | Struct               | Class               | Enum                |
|--------------|----------------------|---------------------|---------------------|
| Type         | Value type           | Reference type      | Value type          |
| Memory       | Stored on stack      | Stored on heap      | Stored on stack     |
| Inheritance  | No inheritance       | Supports inheritance| No inheritance      |
| Mutability   | Must use mutating to modify | Can modify directly| Cannot modify (immutable)|
| Use Case     | Simple, immutable objects | Complex, shared objects | Represents a fixed set of values (often used for state or choices) |


