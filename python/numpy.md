
1. `linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None)` 

## Numpy数组

```python
a = array([1, 2, 3, 4])
```
数组中要求所有元素的 dtype 是一样的
+ 数组中的数据类型:   `a.dtype`   

+ 查看每个元素所占的字节:    `a.itemsize`    

+ 查看形状，会返回一个元组，每个元素代表这一维的元素数目: `a.shape` or `numpy.shape(a)`

+ 查看元素数目: `a.size` or `numpy.size(a)`

+ 查看所有元素所占的空间: `a.nbytes`

+ 查看数组维数: `a.ndim`

## Numpy 类型

基本类型|可用的Numpy类型|备注        
--|--|--
布尔型|	bool|	占1个字节
整型|	int8, int16, int32, int64, int128, int|	int 跟C语言中的 long 一样大
无符号整型	|uint8, uint16, uint32, uint64, uint128, uint	|uint 跟C语言中的 unsigned long 一样大
浮点数|	float16, float32, float64, float, longfloat |	默认为双精度 float64 ，longfloat 精度大小与系统有关
复数|	complex64, complex128, complex, longcomplex	|默认为 complex128 ，即实部虚部都为双精度
字符串	|string, unicode	|可以使用 dtype=S4 表示一个4字节字符串的数组
对象|	object	|数组中可以使用任意值
Records	|void	|
时间	|datetime64, timedelta64| 
|--|--|--|






 







1.  where 语句        
    `where(array)` where 函数会返回所有非零元素的索引。    
    where 的返回值是一个 **元组**。  
    ```python
    a = array([0, 12, 5, 20])
    where(a > 10) #数组中所有大于10的元素的索引位置

    #输出: (array([1, 3]),)
    ```

2. arange 函数产生等差数组。

    `arange([start,] stop[, step,], dtype=None)`
    ```python
    a = arange(0, 80, 10)
    # 输出: array([ 0, 10, 20, 30, 40, 50, 60, 70])
    ```



