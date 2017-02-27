## 1. 环境变量
```
+ $GOROOT 表示 Go 在你的电脑上的安装位置，它的值一般都是 $HOME/go，当然，你也可以安装在别的地方。
+ $GOARCH 表示目标机器的处理器架构，它的值可以是 386、amd64 或 arm。
+ $GOOS 表示目标机器的操作系统，它的值可以是 darwin、freebsd、linux 或 windows。
+ $GOBIN 表示编译器和链接器的安装位置，默认是 $GOROOT/bin，如果你使用的是 Go 1.0.3 及以后的版本，一般情况下你可以将它的值设置为空，Go 将会使用前面提到的默认值。
+ $GOPATH 默认采用和 $GOROOT 一样的值，但从 Go 1.1 版本开始，你必须修改为其它路径。它可以包含多个包含 Go 语言源码文件、包文件和可执行文件的路径，而这些路径下又必须分别包含三个规定的目录：src、pkg 和 bin，这三个目录分别用于存放源码文件、包文件和可执行文件。
+ $GOARM 专门针对基于 arm 架构的处理器，它的值可以是 5 或 6，默认为 6。
+ $GOMAXPROCS 用于设置应用程序可使用的处理器个数与核数
```     
        为了区分本地机器和目标机器，你可以使用 $GOHOSTOS 和 $GOHOSTARCH 设置目标机器的参数，这两个变量只有在进行交叉编译的时候才会用到，如果你不进行显示设置，他们的值会和本地机器（$GOOS 和 $GOARCH）一样。       


1. Go语言不存在隐式类型转换，因此所有的转换都必须显式说明。
2. 常量使用关键字const定义，存储在常量中的数据类型只可以是布尔型、数字型（整数型、浮点型和复数）和字符串型。常量的值必须是能够在编译时就能确定的。
3. 值类型：int、float、bool、string、array数组、struct结构。 引用类型：指针、slices、maps、channel。
4. 局部变量使用“:=”进行初始化声明。全局变量不能使用":="。 局部变量不允许只声明而不使用，而全局变量是允许声明但不使用的。
5. ****Go语言中没有float类型****。float32 精确到小数点后 7 位，float64 精确到小数点后 15 位。
6. 位左移 "<<":
    ```golang
    1 << 10 // 等于 1 KB
    1 << 20 // 等于 1 MB
    1 << 30 // 等于 1 GB
    ```
    使用位左移与 iota 计数配合可优雅地实现存储单位的常量枚举：
    ```golang
    type ByteSize float64
    const (
        _ = iota // 通过赋值给空白标识符来忽略值
        KB ByteSize = 1<<(10*iota)
        MB
        GB
        TB
        PB
        EB
        ZB
        YB
    )
    ```
7. 随机数 (rand包)  
    函数 rand.Float32 和 rand.Float64 返回介于 [0.0, 1.0) 之间的伪随机数，其中包括 0.0 但不包括 1.0。   
    函数 rand.Intn 返回介于 [0, n) 之间的伪随机数。   
    可以使用 Seed(value) 函数来提供伪随机数的生成种子，一般情况下都会使用当前时间的纳秒级数字。
    ```golang
    for i := 0; i < 10; i++ {
        a := rand.Int()
        fmt.Printf("%d / ", a)
    }
    for i := 0; i < 5; i++ {
        r := rand.Intn(8)
        fmt.Printf("%d / ", r)
    }
    fmt.Println()
    timens := int64(time.Now().Nanosecond())
    rand.Seed(timens)
    for i := 0; i < 10; i++ {
        fmt.Printf("%2.2f / ", 100*rand.Float32())
    }
    ```
8. 字符类型     
    包 unicode 包含了一些针对测试字符的非常有用的函数（其中 ch 代表字符）:  
    ```golang
    unicode.IsLetter(ch) //判断是否为字母
    unicode.IsDigit(ch) //判断是否为数字
    unicode.IsSpace(ch) //判断是否为空白符号
    ```
9. [字符串操作](https://github.com/Unknwon/the-way-to-go_ZH_CN/blob/master/eBook/04.7.md)    
    主要用到 ***strings*** 和 ***strconv*** 两个包。
10. 时间和日期(time包)    
    time 包提供了一个数据类型time.Time （作为值使用）以及显示和测量时间和日期的功能函数。  
    time.Now()可以获取当前时间。 
    Duration 类型表示两个连续时刻所相差的***纳秒数***，类型为int64。      
    ```golang
    week = 60 * 60 * 24 * 7 * 1e9 // 获取一周的时间，能获取纳秒数级的
     ```
     Location 类型映射某个时区的时间:  
     ```golang
     t := time.Now().Location()
     ```
     UTC 表示通用协调世界时间:    
     ```golang
     t := time.Now().UTC()
     ```

