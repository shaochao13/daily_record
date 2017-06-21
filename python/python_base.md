### import的原理机制  
import modu 语句将 寻找合适的文件，即调用目录下的 modu.py 文件（如果该文件存在）。如果没有 找到这份文件，Python解释器递归地在 “PYTHONPATH” 环境变量中查找该文件，如果仍没 有找到，将抛出ImportError异常。    

### 整数与不同进制的字符串的转化   
+ 十进制 --> 十六进制: 
```python
hex(255)    //'0xff'
```
+ 十六进制 --> 十进制:
```python
int('FF', 16)   //255
```
+ 十进制 --> 八进制:  
```python
oct(255)    //'0377'
```
+ 八进制 --> 十进制:
```python
int('377', 8)   //255
```
+ 十进制 --> 二进制:  
```python
bin(255)    //0b11111111
```
+ 二进制 --> 十进制:
```python
int('11111111', 2)   //255
```

### 集合(set)
并(union):

    两个集合的并，返回包含两个集合所有元素的集合（去除重复）。可以用方法 a.union(b) 或者操作 a | b 实现。

交(intersection):

    两个集合的交，返回包含两个集合共有元素的集合。可以用方法 a.intersection(b) 或者操作 a & b 实现。

差(difference): 
    
    a 和 b 的差集，返回只在 a 不在 b 的元素组成的集合,可以用方法 a.difference(b) 或者操作 a - b 实现。

对称差(symmetric_difference):

    a 和b 的对称差集，返回在 a 或在 b 中，但是不同时在 a 和 b 中的元素组成的集合。可以用方法 a.symmetric_difference(b) 或者操作 a ^ b 实现（异或操作符）。

包含关系(issubset):

    要判断 b 是不是 a 的子集，可以用 b.issubset(a) 方法，或者更简单的用操作 b <= a 

add 方法向集合添加单个元素

update 方法向集合添加多个元素

remove 方法移除单个元素 (从集合s中移除元素ob，如果不存在会报错)

discard 方法移除单个元素 (但是当元素在集合中不存在的时候不会报错)

pop方法弹出元素   (pop 方法删除并返回集合中任意一个元素，如果集合中没有元素会报错)

#### 不可变集合(frozen set)

不可变集合的一个主要应用是用来作为字典的键，例如用一个字典来记录两个城市之间的距离。  

```python
flight_distance = {}
city_pair = frozenset(['Los Angeles', 'New York'])
flight_distance[city_pair] = 2498
flight_distance[frozenset(['Austin', 'Los Angeles'])] = 1233
flight_distance[frozenset(['Austin', 'New York'])] = 1515
```

不可变集合也是不分顺序的，所以如下两种取到同一值：
```python
flight_distance[frozenset(['New York','Austin'])]
flight_distance[frozenset(['Austin','New York'])]
```


------

1. while 和 for 循环后跟else语句：
    + 要和break一起连用。
    + 当循环正常结束时，循环条件不满足，else被执行。
    + 当循环被break结束时，循环条件仍然满足，else不执行。

    ```python
    # 不执行else
    values = [7, 6, 4, 7, 19, 2, 1]
    for x in values:
        if x <= 10:
            print 'Found:', x
            break
    else:
        print 'All values greater than 10'
    ```

    ```python
    # 执行else
    values = [11, 12, 13, 100]
    for x in values:
        if x <= 10:
            print 'Found:', x
            break
    else:
        print 'All values greater than 10'
    ```

2. map 方法

    其用法为：
    `map(aFun, aSeq)`

    将函数 aFun 应用到序列 aSeq 上的每一个元素上，返回一个列表，不管这个序列原来是什么类型。

    ```python
    def sqr(x): 
        return x ** 2

    a = [2,3,4]
    print map(sqr, a)
    ```
    输出： `[4, 9, 16]`

    根据函数参数的多少，map 可以接受多组序列，将其对应的元素作为参数传入函数:

    ```python
    def add(x, y): 
        return x + y

    a = (2,3,4)
    b = [10,5,3]
    print map(add,a,b)
    ```
    输出：`[12, 8, 7]`

3. `__name__` 属性  
    只有当文件被当作脚本执行的时候， `__name__`的值才会是 `__main__`
    ```python
    # ex2.py
    def test():
        w = [0,1,2,3]
        assert(sum(w) == 6)
        print 'test passed.'
        
    if __name__ == '__main__':
        test()
    # 当执行python ex2.py 时,会执行test()
    # 当着模块导入时import ex2时，不会执行test()
    ```

### 高阶函数

1. `map(f, sq)` 函数将 f 作用到 sq 的每个元素上去，并返回结果组成的列表

# 
+ 任何python对象都可以表现得像函数，只需实现`__call__`方法。
+ 判断对象能否调用，最安全的方法是使用内置的`callable()`函数。
#

# 装饰器
```python
@decorate
def target():
    print('running target()')

#与下面的写是一样的
def target():
    print('running target()')
target = decorate(target)
```
+ 装饰器能把被装饰的函数替换成其他函数。
```python
def deco(func):
    def inner():
        print('running inner()')
    return inner

@deco
def target():
    print('running target()')

#此时执行target()，不会执行target()中的代码，而变成执行deco中的inner()函数。
```
+ 装饰器在加载模块时立即执行。

+ nonlocal 

    python3中引入，它的作用是把变量标记为自由变量
    ```python
    def make_average():
        count = 0
        total = 0

        def average(new_value):
            #如果不这么做，则在average中使用count,total时会报错，因为count,total是不可变对象
            nonlocal count, total 
            count += 1
            total += new_value
            return total / count
        
        return average
    ```