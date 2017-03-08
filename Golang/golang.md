## 1. 环境变量
>
+ $GOROOT 表示 Go 在你的电脑上的安装位置，它的值一般都是 $HOME/go，当然，你也可以安装在别的地方。
+ $GOARCH 表示目标机器的处理器架构，它的值可以是 386、amd64 或 arm。
+ $GOOS 表示目标机器的操作系统，它的值可以是 darwin、freebsd、linux 或 windows。
+ $GOBIN 表示编译器和链接器的安装位置，默认是 $GOROOT/bin，如果你使用的是 Go 1.0.3 及以后的版本，一般情况下你可以将它的值设置为空，Go 将会使用前面提到的默认值。
+ $GOPATH 默认采用和 $GOROOT 一样的值，但从 Go 1.1 版本开始，你必须修改为其它路径。它可以包含多个包含 Go 语言源码文件、包文件和可执行文件的路径，而这些路径下又必须分别包含三个规定的目录：src、pkg 和 bin，这三个目录分别用于存放源码文件、包文件和可执行文件。
+ $GOARM 专门针对基于 arm 架构的处理器，它的值可以是 5 或 6，默认为 6。
+ $GOMAXPROCS 用于设置应用程序可使用的处理器个数与核数
        
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
     t := time.Location()
     ```
     UTC 表示通用协调世界时间:    
     ```golang
     t := time.Now().UTC()
     ```
11. 在 Go 里面函数重载是不被允许的。  
    在函数调用时，像切片（slice）、字典（map）、接口（interface）、通道（channel）这样的引用类型都是默认使用引用传递（即使没有显式的指出指针）。
12. make() 与 new() 区别      
    + ***new(T)*** 为每个新的类型T分配一片内存，初始化为 0 并且返回类型为*T的内存地址：这种方法 返回一个指向类型为 T，值为 0 的地址的指针，它适用于值类型如数组和结构体（参见第 10 章）；它相当于 &T{}。        
    + ***make(T)*** 返回一个类型为 T 的初始值，它只适用于3种内建的引用类型：***切片slice、字典map 和 channel*** 。
13. 可以通过unsafe 包下的Sizeof 方法得到一个变量或者对象占用了多少***内存***.
    ```
    size := unsafe.Sizeof(T{})
    ```
14. struct 结构体  
    1. 如果File是一个结构体类型，那么 表达式`new(File)` 和 `&File{}` 是等价的。
    2. 常常通过工厂方法来返回一个指向结构体实体的指针： 

        ```golang
        type File struct{
            fd int 
            name string
        }

        func NewFile(fd int, name string) *File{
            if fd < 0 {
                return nil
            }
            return &File(fd, name)
        }
        ```
    3. 强制使用工厂方法： 可以把struct体定义成小写的，再定义一个工厂方法对外公开。  

        ```golang
        type matrix struct{
            ...
        }

        func NewMatrix(params) *matrix{
            m := new(matrix)  // or m := &matrix{}
            return m
        }
        ```
        这样在外界只能通过 `right := matrix.NewMatrix(...)` 来实例化matrix。  
        而不能通过`wrong := new(matrix.matrix)` ，编译失败。   
    4. struct中的 ***标签*** ,它是一个附属字段的字符串，可以是文档或其他的重要标记，标签的内容不可以在一般的编程中使用，只有包 ***reflect*** 能获取它。

        ```golang
        import (
            "fmt"
            "reflect"
        )

        type TagType struct { // tags
            field1 bool   "An important answer"
            field2 string "The name of the thing"
            field3 int    "How much there are"
        }

        func main() {
            tt := TagType{true, "Barak Obama", 1}
            for i := 0; i < 3; i++ {
                refTag(tt, i)
            }
        }

        func refTag(tt TagType, ix int) {
            ttType := reflect.TypeOf(tt)
            ixField := ttType.Field(ix)
            fmt.Printf("%v\n", ixField.Tag)
        }
        ``` 
        输出： 
        ```
        An important answer
        The name of the thing
        How much there are
        ```

15. String()    
    > 不要在String() 方法里调用涉及String()方法的方法。         
   
     ```golang
     //比如下面的例子，它导致了一个无限迭代（递归）调用（TT.String() 调用 fmt.Sprintf，而 fmt.Sprintf 又会反过来调用 TT.String()...），很快就会导致内存溢出
     type TT float64

     func (t TT) String() string {
         return fmt.Sprintf("%v", t)
     }
     t. String()
     ```
    > 格式化描述符 ***%T*** 会给出类型的完全规格，**%#v** 会给出实例的完整输出，包括它的字段（在程序自动生成 Go 代码时也很有用） 

    ```golang
    import (
    "fmt"
    "strconv"
    )

    type TwoInts struct {
        a int
        b int
    }

    func main() {
        two1 := new(TwoInts)
        two1.a = 12
        two1.b = 10 
        fmt.Printf("two1 is: %T\n", two1)
        fmt.Printf("two1 is: %#v\n", two1)
    }

    func (tn *TwoInts) String() string {
        return "(" + strconv.Itoa(tn.a) + "/" + strconv.Itoa(tn.b) + ")"
    }
    ```     
    输出:     
    ```
    two1 is: *main.TwoInts
    two1 is: &main.TwoInts{a:12, b:10}
    ```
16. 类型判断： ***type-switch***       (type-switch 不允许有 fallthrough)       
    
    ```golang
    func classifier(items ...interface{}) {
        for i, x := range items {
            switch x.(type) { //也可以使用 switch t := areaIntf.(type)  变量 t 得到了 areaIntf 的值和类型
            case bool:
                fmt.Printf("Param #%d is a bool \n", i)
            case float64:
                fmt.Printf("Param #%d is a float64 \n", i)
            case int, int64:
                fmt.Printf("Param #%d is a int \n", i)
            case nil:
                fmt.Printf("Param #%d is a nil\n", i)
            case complex64, complex128:
                fmt.Printf("Param #%d is a complex\n", i)
            case string:
                fmt.Printf("Param #%d is a string\n", i)
            default:
                fmt.Printf("Param #%d is unknown\n", i)
            }
        }
    }
    ``` 

17. 测试一个值是否实现了某个接口： 

    ```golang
    type Stringer interface {
        String() string
    }

    if sv, ok := v.(Stringer); ok {
        fmt.Printf("v implements String(): %s\n", sv.String()) // note: sv, not v
    }
    ```

18. ***接口方法集的调用规则***：     
    + 类型 *T 的可调用方法集包含接受者为 *T 或 T 的所有方法集
    + 类型 T 的可调用方法集包含接受者为 T 的所有方法
    + 类型 T 的可调用方法集不包含接受者为 *T 的方法

