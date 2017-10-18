+ Math.Round()实现中国式四舍五入

    C#中的Math.Round()并不是使用的"四舍五入"法。其实在VB、VBScript、C#、J#、T-SQL中Round函数都是采用Banker's rounding（银行家算法），即：`四舍六入五取偶`。事实上这也是IEEE的规范，因此所有符合IEEE标准的语言都应该采用这样的算法。

    Math.Round 方法提供了一个枚举选项 `MidpointRounding.AwayFromZero` 可以用来实现传统意义上的"四舍五入"。即： 
    ```csharp
    Math.Round(4.5, MidpointRounding.AwayFromZero) = 5
    ```

    用这个计算小数的话,须使用如下重载方法：
    ```csharp
    decimal Round(decimal d, int decimals, MidpointRounding mode)

    Math.Round(526.925, 2,MidpointRounding.AwayFromZero)  # 输出 526.92
    ```