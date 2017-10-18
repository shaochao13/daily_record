+ Math 中的 round 方法

    它表示“四舍五入”，算法为 `Math.floor(x+0.5)` ，即将原来的数字加上0.5后再向下取整。
    所有符合IEEE标准的语言都采用 `四舍六入五取偶` 这样的算法
    ```java
    Math.round(-1.5) = -1
    Math.round(-1.6) = -2
    ```