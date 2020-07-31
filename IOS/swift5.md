## 字符串和字符

### 扩展字符串分隔符

可以将字符串文字放在扩展分隔符中，这样字符串中的特殊字符将会被直接包含而非转义后的效果。将字符串放在引号（`"`）中并用数字符号（`#`）括起来。例如，打印字符串文字 `#"Line 1 \nLine 2"#` 会打印换行符转义序列（`\n`）而不是给文字换行。

如果需要字符串文字中字符的特殊效果，请匹配转义字符（`\`）后面添加与起始位置个数相匹配的 `#` 符。 例如，如果字符串是 `#"Line 1 \nLine 2"#` 并且您想要换行，则可以使用 `#"Line 1 \#nLine 2"#` 来代替。 同样，`###"Line1 \###nLine2"###` 也可以实现换行效果。

扩展分隔符创建的字符串文字也可以是多行字符串文字。 可以使用扩展分隔符在多行字符串中包含文本 `"""`，覆盖原有的结束文字的默认行为。

```swift
let threeMoreDoubleQuotationMarks = #"""
Here are three more double quotes: """
"""#
```



### 字符串是值类型

创建了一个新的字符串，那么当其进行常量、变量赋值操作，或在函数/方法中传递时，会进行值拷贝。

在实际编译时，Swift 编译器会优化字符串的使用，使实际的复制只发生在绝对必要的情况下，这意味着将字符串作为值类型的同时可以获得极高的性能。



## 集合类型

### 数组

1. 初始化一个空的数组：

   ```swift
   let emptyArray = [String]() 
   shoppingList = [] //如果类型信息可以被推断出来，你可以用 [] 来创建空字典——比如，在给变量赋新值或者给函数传参数的时候
   ```

2. 创建一个带有默认值的数组

   ```swift
   var threeDoubles = Array(repeating: 0.0, count: 3)
   ```



### 集合

一个类型为了存储在集合中，该类型必须是*可哈希化*的。

遵循 `Hashable` 协议的类型需要提供一个类型为 `Int` 的可读属性 `hashValue`。因为 `Hashable` 协议遵循 `Equatable` 协议，所以遵循该协议的类型也必须提供一个“是否相等”运算符（`==`）的实现。



创建和构造一个空的集合：

```swift
var letters = Set<Character>()
```



### 字典

其所有键的值需要是相同的类型，所有值的类型也需要相同。

1. 初始化一个空的字典：

   ```swift
   let emptyDictionary = [String: Float]()
   occupations = [:] //如果类型信息可以被推断出来，可以用 [:] 来创建空字典——比如，在给变量赋新值或者给函数传参数的时候
   ```

2. `updateValue(_:forKey:)` 方法在这个键不存在对应值的时候会设置新值或者在存在时更新已存在的值。和下标的方式不同，`updateValue(_:forKey:)` 这个方法返回更新值之前的*原值*。

```swift
//updateValue(_:forKey:) 方法会返回对应值类型的可选类型。
if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") {
    print("The old value for DUB was \(oldValue).")
}
```

3. 因为有可能请求的键没有对应的值存在，字典的下标访问会返回对应值类型的可选类型。如果这个字典包含请求键所对应的值，下标会返回一个包含这个存在值的可选类型，否则将返回 `nil`：

   ```swift
   if let airportName = airports["DUB"] {
       print("The name of the airport is \(airportName).")
   } else {
       print("That airport is not in the airports dictionary.")
   }
   // 打印“The name of the airport is Dublin Airport.”
   ```

4. 可以使用下标语法通过将某个键的对应值赋值为 `nil` 来从字典里移除一个键值对：

   ```swift
   airports["APL"] = "Apple Internation"
   // “Apple Internation”不是真的 APL 机场，删除它
   airports["APL"] = nil
   // APL 现在被移除了
   ```

5. `removeValue(forKey:)` 方法也可以用来在字典中移除键值对。这个方法在键值对存在的情况下会移除该键值对并且返回被移除的值或者在没有对应值的情况下返回 `nil`：

   ```swift
   if let removedValue = airports.removeValue(forKey: "DUB") {
       print("The removed airport's name is \(removedValue).")
   } else {
       print("The airports dictionary does not contain a value for DUB.")
   }
   // 打印“The removed airport's name is Dublin Airport.”
   ```



## 控制流

For-In循环、While循环、Repeat-While循环。

使用 `..<` 创建的范围不包含上界，如果想包含的话需要使用 `...` 。

### if

使用 `if` 和 `switch` 来进行条件操作，使用 `for-in`、`while` 和 `repeat-while` 来进行循环。包裹条件和循环变量的括号可以省略，但是语句体的大括号是必须的。

在 `if` 语句中，条件必须是一个布尔表达式——这意味着像 `if score { ... }` 这样的代码将报错，而不会隐形地与 0 做对比。

可以一起使用 `if` 和 `let` 一起来处理值缺失的情况。

```swift
var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}

//另一种处理可选值的方法是通过使用 ?? 操作符来提供一个默认值。
let nickName: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickName ?? fullName)"
```



### switch

`switch` 支持任意类型的数据以及各种比较操作——不仅仅是整数以及测试相等。

```swift
let vegetable = "red pepper"
switch vegetable {
case "celery":
    print("Add some raisins and make ants on a log.")
case "cucumber", "watercress":
    print("That would make a good tea sandwich.")
case let x where x.hasSuffix("pepper"):
    print("Is it a spicy \(x)?")
default:
    print("Everything tastes good in soup.")
}
```

运行 `switch` 中匹配到的 `case` 语句之后，程序会退出 `switch` 语句，并不会继续向下运行，所以不需要在每个子句结尾写 `break`。

#### 区间匹配

```swift
let approximateCount = 62
let countedThings = "moons orbiting Saturn"
let naturalCount: String
switch approximateCount {
case 0:
    naturalCount = "no"
case 1..<5:
    naturalCount = "a few"
case 5..<12:
    naturalCount = "several"
case 12..<100:
    naturalCount = "dozens of"
case 100..<1000:
    naturalCount = "hundreds of"
default:
    naturalCount = "many"
}
print("There are \(naturalCount) \(countedThings).")
// 输出“There are dozens of moons orbiting Saturn.”
```

#### 元组

```swift
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
    print("\(somePoint) is at the origin")
case (_, 0):
    print("\(somePoint) is on the x-axis")
case (0, _):
    print("\(somePoint) is on the y-axis")
case (-2...2, -2...2):
    print("\(somePoint) is inside the box")
default:
    print("\(somePoint) is outside of the box")
}
// 输出“(1, 1) is inside the box”
```

#### 值绑定（Value Bindings）

```swift
let anotherPoint = (2, 0)
switch anotherPoint {
case (let x, 0):
    print("on the x-axis with an x value of \(x)")
case (0, let y):
    print("on the y-axis with a y value of \(y)")
case let (x, y):
    print("somewhere else at (\(x), \(y))")
}
// 输出“on the x-axis with an x value of 2”
```

#### Where

```swift
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    print("(\(x), \(y)) is on the line x == y")
case let (x, y) where x == -y:
    print("(\(x), \(y)) is on the line x == -y")
case let (x, y):
    print("(\(x), \(y)) is just some arbitrary point")
}
// 输出“(1, -1) is on the line x == -y”
```



### guard 提前退出

使用 `guard` 语句来要求条件必须为真时，以执行 `guard` 语句后的代码。不同于 `if` 语句，一个 `guard` 语句总是有一个 `else` 从句，如果条件不为真则执行 `else` 从句中的代码。

```swift
func greet(person: [String: String]) {
    guard let name = person["name"] else {
        return
    }

    print("Hello \(name)!")

    guard let location = person["location"] else {
        print("I hope the weather is nice near you.")
        return
    }

    print("I hope the weather is nice in \(location).")
}

greet(person: ["name": "John"])
// 输出“Hello John!”
// 输出“I hope the weather is nice near you.”
greet(person: ["name": "Jane", "location": "Cupertino"])
// 输出“Hello Jane!”
// 输出“I hope the weather is nice in Cupertino.”
```





## 闭包

1. 可以使用 `{}` 来创建一个匿名闭包。使用 `in` 将参数和返回值类型的声明与闭包函数体进行分离。

   ```swift
   numbers.map({
       (number: Int) -> Int in
       let result = 3 * number
       return result
   })
   ```

2. 如果一个闭包的类型已知，比如作为一个代理的回调，你可以忽略参数，返回值，甚至两个都忽略。单个语句闭包会把它语句的值当做结果返回。

   ```swift
   let mappedNumbers = numbers.map({ number in 3 * number })
   print(mappedNumbers)
   ```

3. 可以通过参数位置而不是参数名字来引用参数——这个方法在非常短的闭包中非常有用。当一个闭包作为最后一个参数传给一个函数的时候，它可以直接跟在圆括号后面。当一个闭包是传给函数的唯一参数，你可以完全忽略圆括号。

   ```swift
   let sortedNumbers = numbers.sorted { $0 > $1 }
   print(sortedNumbers)
   ```

   

## 对象与类

- 使用 `init` 来创建一个构造器。

- 使用 `deinit` 创建一个析构函数。

- 类的构造器执行:

  1. 设置子类声明的属性值
  2. 调用父类的构造器
  3. 改变父类定义的属性值。其他的工作比如调用方法、getters 和 setters 也可以在这个阶段完成。

- 使用 `willSet` 和 `didSet`。写入的代码会在属性值发生改变时调用，**但不包含构造器中发生值改变的情况**。

- 处理变量的可选值时，你可以在操作（比如方法、属性和子脚本）之前加 `?`。如果 `?` 之前的值是 `nil`，`?` 后面的东西都会被忽略，并且整个表达式返回 `nil`。否则，可选值会被解包，之后的所有代码都会按照解包后的值运行。在这两种情况下，整个表达式的值也是一个可选值。

  ```swift
  let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
  let sideLength = optionalSquare?.sideLength
  ```



## 枚举和结构体

- 默认情况下，Swift 按照从 0 开始每次加 1 的方式为原始值进行赋值。

- 使用 `rawValue` 属性来访问一个枚举成员的原始值。

- 使用 `init?(rawValue:)` 初始化构造器来从原始值创建一个枚举实例。如果存在与原始值相应的枚举成员就返回该枚举成员，否则就返回 `nil`。

  ```swift
  if let convertedRank = Rank(rawValue: 3) {
      let threeDescription = convertedRank.simpleDescription()
  }
  ```

- 枚举的关联值是实际值，并不是原始值的另一种表达方法。

  ```swift
  enum ServerResponse {
      case result(String, String)
      case failure(String)
  }
  
  let success = ServerResponse.result("6:00 am", "8:09 pm")
  let failure = ServerResponse.failure("Out of cheese.")
  
  switch success {
  case let .result(sunrise, sunset):
      print("Sunrise is at \(sunrise) and sunset is at \(sunset)")
  case let .failure(message):
      print("Failure...  \(message)")
  }
  ```

- 结构体是传值，类是传引用。



## 协议和扩展

类、枚举和结构体都可以遵循协议。

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

struct SimpleStructure: ExampleProtocol {
    var simpleDescription: String = "A simple structure"
    mutating func adjust() {  // mutating 关键字用来标记一个会修改结构体的方法。SimpleClass 的声明不需要标记任何方法，因为类中的方法通常可以修改类属性（类的性质）
        simpleDescription += " (adjusted)"
    }
}
var b = SimpleStructure()
b.adjust()
let bDescription = b.simpleDescription
```

使用 `extension` 来为现有的类型添加功能，比如新的方法和计算属性。

```swift
extension Int: ExampleProtocol { //给Int类型对 ExampleProtocol协议 的扩展
    var simpleDescription: String {
        return "The number \(self)"
    }
    mutating func adjust() {
        self += 42
    }
}
print(7.simpleDescription)


extension Double {
    var abs :String { //给Double类型添加一个abs属性的扩展
        return "abs"
    }
}
```



## 错误处理

使用 `throw` 来抛出一个错误和使用 `throws` 来表示一个可以抛出错误的函数。

```swift
func send(job: Int, toPrinter printerName: String) throws -> String {
    if printerName == "Never Has Toner" {
        throw PrinterError.noToner
    }
    return "Job sent"
}
```

错误处理方式：

1. 使用 `do-catch`

   ```swift
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

   

2. 使用 `try?` 将结果转换为可选的。如果函数抛出错误，该错误会被抛弃并且结果为 `nil`。否则，结果会是一个包含函数返回值的可选值。

   ```swift
   let printerSuccess = try? send(job: 1884, toPrinter: "Mergenthaler")
   let printerFailure = try? send(job: 1885, toPrinter: "Never Has Toner")
   ```



使用 `defer` 代码块来表示在函数返回前，函数中最后执行的代码。无论函数是否会抛出错误，这段代码都将执行。



## 泛型

在尖括号里写一个名字来创建一个泛型函数或者类型。创建泛型函数、方法、类、枚举和结构体。

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



在类型名后面使用 `where` 来指定对类型的一系列需求，比如，限定类型实现某一个协议，限定两个类型是相同的，或者限定某个类必须有一个特定的父类。

```swift
func anyCommonElements<T: Sequence, U: Sequence>(_ lhs: T, _ rhs: U) -> Bool
    where T.Element: Equatable, T.Element == U.Element
{
    for lhsItem in lhs {
        for rhsItem in rhs {
            if lhsItem == rhsItem {
                return true
            }
        }
    }
    return false
}
anyCommonElements([1, 2, 3], [3])
```

