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

   