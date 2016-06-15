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
        ```
//还可以使用"_"来只匹配元组中的一部分
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
