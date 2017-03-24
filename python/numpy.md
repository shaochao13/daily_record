
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

任意类型的数组：    
```python
a = array([1,1.2,'hello', [10,20,30]], dtype=object)
```
乘法： 
```python
a * 2
#输出：array([2, 2.4, 'hellohello', [10, 20, 30, 10, 20, 30]], dtype=object)
```

### 类型转换
1. `asarray` 函数：
    + asarray 不会修改原来数组的值
    + 当类型相同的时候，asarray 并不会产生新的对象，而是使用同一个引用。`有些时候为了保证我们的输入值是数组，我们需要将其使用 asarray 转化，当它已经是数组的时候，并不会产生新的对象，这样保证了效率` 
    ```python
    a = array([1.5, -3],dtype=float32)   # array([ 1.5, -3. ], dtype=float32)
    asarray(a, dtype=float64) # 转换类型float32 --> float64
    ```

2. `astype` 函数: 
    + astype也不会改变原来数组的值 
    + astype 总是返回原来数组的一份`复制`，即使转换的类型是相同的    
    ```python 
    a.astype(float64)
    ```

## 方法

1. 求和: `sum()`
    ```python
    a = array([[1,2,3],[4,5,6]])
    sum(a)
    a.sum()
    sum(a, axis=0) # 指定求和的维度  输出：array([5, 7, 9])
    a.sum(axis=-1) # 最后一维求和
    ```

2. 求积 `prod()`
    ```python
    a = array([[1,2,3],[4,5,6]])
    a.prod()    # 输出720
    prod(a, axis=0) #按维度 输出：array([ 4, 10, 18])
    ```

3. 求最大值`max()` 最小值`min()`   
    ```python
    a = array([[ 0.444,  0.06 ,  0.668,  0.02 ],
       [ 0.793,  0.302,  0.81 ,  0.381],
       [ 0.296,  0.182,  0.345,  0.686]])

    a.min()
    a.min(axis=0) #按维度  输出：array([ 0.296,  0.06 ,  0.345,  0.02 ])

    a.max()
    a.max(axis=-1)
    ```

4. 最大值的位置`argmax()` 最小值的位置`argmin()`
    ```python
     a = array([[ 0.444,  0.06 ,  0.668,  0.02 ],
       [ 0.793,  0.302,  0.81 ,  0.381],
       [ 0.296,  0.182,  0.345,  0.686]])

    a.argmin()  # out: 3
    a.argmin(axis=0)  # 按维度 out: array([2, 0, 2, 0])
    ```

5. 均值 `mean()` or `average()`   

    `average 函数还支持 加权平均`
    ```python
    a = array([[1,2,3],[4,5,6]])
    a.mean()  # out: 3.5

    a.mean(axis=-1)  # 按维度 out: array([ 2.,  5.])
    ```

    ```python
    a = array([[1,2,3],[4,5,6]])

    average(a)
    average(a, axis = 0)

    # average 函数还支持 加权平均
    average(a, axis = 0, weights=[1,2])     #out:array([ 3.,  4.,  5.])
    ```

6. 标准差 `std()` , 方差 `var()`  

    ```python
    a = array([[1,2,3],[4,5,6]])
    std(a, axis=1)
    a.std(axis=1) # out:array([ 0.816,  0.816])
    ```

    ```python
    a.var(axis=1)
    var(a, axis=1)  # out:array([ 0.667,  0.667])
    ```

 7. 数值限制在某个范围 `clip()`  

    ```python
    a = array([[1, 2, 3],[4, 5, 6]]) 
    a.clip(3,5) # 小于3的变成3，大于5的变成5   out: array([[3, 3, 3],[4, 5, 5]])
    ```
8. 计算最大值和最小值之差 `ptp()`  

    ```python
    a = array([[1,2,3],[4,5,6]])
    a.ptp(axis=1)  # out: array([2,2])
    a.ptp() # @ out:5
    ```
5. 四舍五入 `round()`   

    `.5的近似规则为近似到偶数值`
    ```python
    a = array([1.35, 2.5, 1.5])
    a.round()  # out: array([ 1.,  2.,  2.])
    a.round(decimals=1) # 保留一位小数 out: array([ 1.4,  2.5,  1.5])  
    ```




---

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



