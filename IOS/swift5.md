## 数组

1. 初始化一个空的数组：

   ```swift
   let emptyArray = [String]() 
   shoppingList = [] //如果类型信息可以被推断出来，你可以用 [] 来创建空字典——比如，在给变量赋新值或者给函数传参数的时候
   ```

   

## 字典

1. 初始化一个空的字典：

   ```swift
   let emptyDictionary = [String: Float]()
   occupations = [:] //如果类型信息可以被推断出来，可以用 [:] 来创建空字典——比如，在给变量赋新值或者给函数传参数的时候
   ```



## 控制流

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

