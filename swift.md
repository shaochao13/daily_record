1. 不能进行自动类型转换。必须显式地进行类型转换。  
```swift
let x :UInt16 = 100
let y :UInt8 = 20
x+y //这里是不能进行成功操作的。
if 1{
    print("a")
} //这个语句也是不正确的。因为 “1”不能自动转换成Bool类型。
```

2. 多行注释中间还能插入多行注释。

3. 区间运算符：
    + [a,b] -----> a...b
    + [a,b) -----> ***a..<b***

4. do while 在swift 中 使用 repeat while

5. switch 用法
    + 可以使用fallthrough 跳转到下一个case语句块中, 但 当case 中有let 解包时，不能 使用fallthrough
    + case 中可以使用区间运算符：      
    ```swift
    let score = 90
    switch score{
    case 0:
        print("You got an egg!")
    case 1..<60:
        print("You failed.")
    case 60:
        print("Just passed.")
    case 61..<80:
        print("Just so-so")
    case 80..<90:
        print("Good")
    case 90..<100:
        print("Great")
    case 100:
        print("Perfect!")
    default:
        print("Error score.")
    }
    ```
    + case 可以使用元组Tuple：     
    ```swift
    let vector = (1,1)
    switch vector{
    case (0,0):
        print("It's origin!")
    case (1,0):
        print("It an unit vector on the positive x-axis.")
    case (-1,0):
        print("It an unit vector on the gegative x-axis.")
    case (0,1):
        print("It an unit vector on the positive y-axis.")
    case (0,-1):
        print("It an unit vector on the negative y-axis.")
    default:
        print("It's just an ordinary vector.")
    }        
    ```
    还可以使用"_"来只匹配元组中的一部分     
    ```swift
    let point = (1,1)
    switch point{
    case (0,0):
        print("It's origin.")
    case(_,0):
        print("It on the x-axis.")
    case(0,_):
        print("It on the y-axis.")
    case (-2...2,-2...2)://还能使用带区间的元组
        print("It's near the origin.")
    default:
        print("It's just an ordinary point.")
    }
    ```
    + 解包：       
    ```swift
    let point = (0,0)
    switch point{
    case (0,0):
        print("It's origin.")
    case(let x,0):
        print("It on the x-axis.")
        print("The x value is \(x)")
    case(0,let y):
        print("It on the y-axis.")
        print("The y value is \(y)")
    case (let x, let y):
        print("It's near the origin.")
        print("The point is (\(x), \(y))")
    }
    ```
    + 使用where：      
    ```swift
    let point = (1,1)
    switch point{
    case let (x,y) where x == y:
        print("It's on the line x == y!")
    case let(x,y) where x == -y:
        print("It's on the line x == -y!")
    case let (x,y):
        print("It's just an ordinary point.")
        print("The point is (\(x), \(y))")
    }
    ```

6. case where 组合的一些用法：      
    ```swift
    let age = 19
    if age >= 10 && age <= 19{
        print("You're a teenager.")
    }
    ```
    可使用如下语句替换       
    ```swift
    if case 10...19 = age{
        print("You're a teenager.")
    }   
    ```     
    ```swift
    if age >= 10 && age <= 19 && age >= 18{
        print("You're a teeenage and in a college.")
    }
    ```
    可使用如下语句替换       
    ```swift
    if case 10...19 = age where age >= 18{
        print("You're a teeenage and in a college.")
    }
    ```     
    ```swift
    let vector = (4,0)
    if case (let x , 0) = vector where x > 2 && x < 5 {
        print("It's the vector.")
    }
    ```     
    ```swift
    for i in 1...100{
        if i%3 == 0{
            print(i)
        }
    }
    ```
    可使用如下语句替换       
    ```swift
    for case let i in 1...100 where i%3==0 {
        print(i)
    }
    ```

7. guard 关键字的使用     
    ```swift
    func buy(money:Int, price:Int, capacity:Int, volume: Int){
        if money >= price{
            if capacity >= volume{
                print("I can by it!")
                print("\(money-price) Yuan left.")
                print("\(capacity-volume) cubic meters left.")
            }
            else{
                print("Not enough capacity")
            }
        }
        else{
            print("Not enough money")
        }
    }
    ```
    可使用如下语句替换   
    ```swift
    func buy2(money:Int, price:Int, capacity:Int, volume: Int){
        guard money >= price else{
            print("Not enough money")
            return
        }
        guard capacity >= volume else{
            print("Not enough capacity")
            return
        }
        print("I can by it!")
        print("\(money-price) Yuan left.")
        print("\(capacity-volume) cubic meters left.")
    }
    //这样的写法，条理很清晰。先把一些边界情况判断完，再进行主体的编写。
    ```

8. "??" 运算符
    对于可选类型Optional可以使用“??”类型来简化代码：      
    ```swift
    var errorMessage: String? = nil

    let message:String
    //第一个种方式
    if let errorMessage = errorMessage{
        message = errorMessage
    }
    else{
        message = "No Error"
    }
    //第二种方式
    let message2 = errorMessage == nil ? "No Error" : errorMessage
    //第三种方式 ，这种 方式简化也代码
    let message3 = errorMessage ?? "No Error"
    ```

9. 按引用转值
    在方法如果想要按引用转值，参数需要使用inout：    
    ```swift
    func swapTwoInts(inout a: Int, inout _ b: Int) {
        (a,b) = (b,a) //使用元组交换两值，跟python很相似。
    }

    var x:Int = 1
    var y:Int = 2
    swapTwoInts(&x, &y)//传参数的地址
    ```

10. 在swift中，方法中传递的数组、集合、字典都是按值类型进行传入的。

11. 函数和闭包是引用类型

12. 枚举enum
    - 原始值Raw Value:
    ```swift
    enum Coin:Int{
    case Penny = 1
    case Nickel = 5
    case Dime = 10
    case Quarter = 25
    }
    //可以使用rawValue来得到原始值 
    Coin.Penny.rawValue 可以得到 1
    ``` 
    - 关联值Associate Value:   
    ```swift
    enum Shape{
        case Square(side: Double)
        case Rectangle(width: Double, height: Double)
        case Circle(centerx: Double, centery: Double, radius: Double)
        case Point
    }
    let square = Shape.Square(side: 10)
    let rectange = Shape.Rectangle(width: 20, height: 30)
    let circle = Shape.Circle(centerx: 0, centery: 0, radius: 15)
    let point = Shape.Point
    func area(shape: Shape) -> Double {
        switch shape {
            case let Shape.Square(side)://可以使用 let 来对enum中的值 进行解包出来，从而使用其值
                return side * side
            case let Shape.Rectangle(width, height):
                return width * height
            case let Shape.Circle(_, _, radius)://使用“_“忽略没需要使用的参数
                return M_PI * radius
            default:
                return 0
        }
    }
    ```     
    Raw Value 与 Associate Value 不能同时出来在一个enum中。

    - Optional 可选型实际就是enum

    - enum 中对自我的引用 ，使用indirect  
        ```swift
        enum ArithmeticExpression {
            case Numer(Int)
            indirect case Addtion(ArithmeticExpression, ArithmeticExpression) //可以indirect 可以实现在enum内部对自身的引用
            indirect case Multiplication(ArithmeticExpression, ArithmeticExpression)
        }
        // (5 + 4) * 2
        let five = ArithmeticExpression.Numer(5)
        let four = ArithmeticExpression.Numer(4)
        let sum = ArithmeticExpression.Addtion(five, four)
        let two = ArithmeticExpression.Numer(2)
        let product = ArithmeticExpression.Multiplication(sum, two)
        //计算
        func evaluate(expression: ArithmeticExpression) -> Int {
            switch expression {
                case let ArithmeticExpression.Numer(value):
                    return value
                case let ArithmeticExpression.Addtion(left, right):
                    return evaluate(left)+evaluate(right)
                case let ArithmeticExpression.Multiplication(left, right):
                    return evaluate(right) * evaluate(left)
            }
        }
        ```
    - enum 也可以包括方法：    
        ```swift
        enum Shape{
            case Square(side: Double)
            case Rectangle(width: Double, height: Double)
            case Circle(centerx: Double, centery: Double, radius: Double)
            case Point
            
            func area() -> Double {
                switch self {
                case let .Square(side):
                    return side*side
                case let .Rectangle(width, height):
                    return width*height
                case let .Circle(_,_,r):
                    return M_PI * r * r
                case .Point:
                    return 0
                    
                }
            }
        } 
        ```
13. 值类型如何在其内部通过方法的形式修改其自身的数据 ***mutating***：       
    ```swift
    enum Switch{
        case On
        case Off
        //使用mutating 作用于func之前，可以让值类型的类型在其内部可以修改其自身的值。
        mutating func click(){
            switch self {
            case .On:
                self = .Off
            case .Off:
                self = .On
            }
        }
    }

    struct Location {
        var x = 0
        var y = 0
        //使用mutating 作用于func之前，可以让值类型的类型在其内部可以修改其自身的值。
        mutating func goEast(){
            self.x += 1
        }
    }
    ```

14. "==","!=" & "===","!==":   
    "==","!=" 是进行值的比较，不能直接用在引用类型身上.   
    “===”,"!==" 用于引用类型的比较，即地址是否相同。    

15. 属性观查器 didSet willSet     
    ```swift
    class LightBulb{
        static let maxCurrent = 30
        var current = 0 {
            //执行顺序 willSet --> didSet
            //willSet中能通过newValue 得到新赋的值
            //didSet中能通过oldValue 得到赋值之前的值
            
            willSet{
                print("The new value is \(newValue)")
            }
            
            didSet{
                print("The old value is \(oldValue)")
                print("The current is \(current)")
                
                if current == LightBulb.maxCurrent {
                    print("Pay attention, the current value get to the maximum point.")
                }
                else if current > LightBulb.maxCurrent{
                    print("Current too high")
                    current = oldValue
                }
            }
        }
    }
    ```
    #### 注意事项：
    属性观查器的方法，在init方法中是不会被执行的，也就是说在init方法中对属性进行赋值，是不会被执行的；
    在声明时赋值，此时也是不会被执行的。如：
        var current = 0 { didSet{....}} ,当赋值为0时，此时的didSet是不会被执行的。

16. 延迟属性Lazy Property   
    ```swift
    class Web{
        let url: String
        lazy var html: String? = {
            //从网络读取url对应的html
            return nil
        }()
        
        init(url:String){
            self.url = url
        }
    }
    ```
    延迟属性也可以看作是闭包的一种使用。

17. 扩展extension
    - 扩展属性(扩展只能添加新的计算属性，不能添加存储属性，也不能向已有的属性添加属性观察器。)
        ```swift
        extension Double{
            var cm: Double {
                return self / 100.0
            }
            
            var km: Double{
                return self * 1000.0
            }
            
            var m:Double{
                return self
            }
        }
        ```
    - 扩展下标脚本
        ```swift
        extension Int{
            subscript(index:Int) -> Int{
                var decimal = 1
                for _ in 1...index{
                    decimal *= 10
                }
                return (self/decimal) % 10
            }
        }
        ```
