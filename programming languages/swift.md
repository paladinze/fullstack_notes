# Swift

## what
- A statically typed
- lanauge for the Apple ecosystem

## variables
```swift
var myVariable = 42 // var for re-assigable value
myVariable = 50
let implicitInteger = 70 // let for constant value
let implicitDouble = 70.0
let explicitDouble: Double = 70
let appleSummary = "I have \(apples) apples." // string interpolation
let quotation = """
some foo
some bar
""" // multiline strings
```

## collections
```swift
let emptyArray = [String]() // use [] if type can be inferred
let fooArr = [1, 2, 3]
foo[0] // 1
foo.append(4)

let emptyMap = [String: Float]() // use [:] if type can be inferred
let fooMap = [
    "k1": "v1",
    "k2": "v2",
]
```

## Null safety
```swift
let foo: String? = "Hello" // nullable foo
print(foo == nil) // nil
let bar = foo ?? "default str" // default value
```

## Control flow
```swift
// array for in
let fooArr = [1, 2, 3, 4, 5]
for num in fooArr {
    if (num > 3) {
        print(num)
    } else {
        print("else")
    }
}

// map for in
let map = ["a": 1, "b": 2]
for (key, val) in map {
    print("\(key):\(val)")
}

// while
while true {}
repeat() {} while true

// range
for i in 1...10 {} // 1 to 10
for i in 1..<10 {} // 1 to 9

```


## Function
```swift

// basic function
func sum(num1: Int, num2: Int) -> Int {
    return num1 + num2;
}

sum(num1: 1, num2: 2)

// use tuple to return multiple values
func reportScores(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    return (1, 2, 3)
}
reportScores(scores: [1,2,3])


// fp: return function
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()

// fp: function as parameter
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)


// fp: mapping values
// `{}` is needed for anonymous function
// `in` seperates args & function body
let nums = [1, 2, 3]
let mappedNums = nums.map({ num in 3 * num }) // [3, 6, 9]
```

## Object & Classes
```swift
class Shape {
    var numberOfSides = 0
    var name: String

    init(name: String) {
        self.name = name
    }

    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}

var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()


```

## Protocol (aka. Protocol)
- Classes, enumerations, and structs can all adopt protocols.

```swift
protocol ExampleProtocol {
    var simpleDescription: String { get }
    mutating func adjust()
}

class SimpleClass: ExampleProtocol {
    var simpleDescription: String = "A very simple class."
    var anotherProperty: Int = 69105
    func adjust() {
        simpleDescription += "  Now 100% adjusted."
    }
}
var a = SimpleClass()
a.adjust()
let aDescription = a.simpleDescription

```

## Error Handling
- error is anything that implements the `Error` protocol
- `throws` labels the function as throwable

```swift
enum PrinterError: Error {
    case outOfPaper
    case noToner
    case onFire
}

func send(job: Int, toPrinter printerName: String) throws -> String {
    if printerName == "Never Has Toner" {
        throw PrinterError.noToner
    }
    return "Job sent"
}

do {
    let printerResponse = try send(job: 1440, toPrinter: "Gutenberg")
    print(printerResponse)
} catch PrinterError.onFire {
    print("I'll just put this over here, with the rest of the fire.")
} catch let printerError as PrinterError {
    print("Printer error: \(printerError).")
} catch {
    print(error)
}
```

## Generic
```swift
func makeArray<Item>(repeating item: Item, numberOfTimes: Int) -> [Item] {
    var result = [Item]()
    for _ in 0..<numberOfTimes {
        result.append(item)
    }
    return result
}
makeArray(repeating: "knock", numberOfTimes: 4)
```