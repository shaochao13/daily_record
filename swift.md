1. 不能进行自动类型转换。必须显式地进行类型转换。
```
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
    ```
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
    ```
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
    ```
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
    ```
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
    ```
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
    ```
    let age = 19
    if age >= 10 && age <= 19{
        print("You're a teenager.")
    }
    ```
    可使用如下语句替换
    ```
    if case 10...19 = age{
        print("You're a teenager.")
    }   
    ```
    ```
    if age >= 10 && age <= 19 && age >= 18{
        print("You're a teeenage and in a college.")
    }
    ```
    可使用如下语句替换
    ```
    if case 10...19 = age where age >= 18{
        print("You're a teeenage and in a college.")
    }
    ```
    ```
    let vector = (4,0)
    if case (let x , 0) = vector where x > 2 && x < 5 {
        print("It's the vector.")
    }
    ```
    ```
    for i in 1...100{
        if i%3 == 0{
            print(i)
        }
    }
    ```
    可使用如下语句替换
    ```
    for case let i in 1...100 where i%3==0 {
        print(i)
    }
    ```

7. guard 关键字的使用
    ```
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
    ```
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
    ```
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