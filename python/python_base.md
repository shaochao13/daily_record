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

- while 和 for 循环后跟else语句：
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

- map 方法

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

- `__name__` 属性  
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

- `__slot__` 属性

    `__slot__` 使用时，要`慎重`。
    1. `__slot__` 能显著节省内存。
    2. 每个子类都要定义 `__slot__` 属性，因为解释器会忽略继承的 `__slot__` 属性.
    3. 实例只能拥有 `__slot__` 中列出的属性，除非把 `__dict__` 加入到 `__slot__` 中（这样做就失去了节省内存的功效）
    4. 如果不把 `__weakref__` 加入 `__slot__` ，实例就不能作为弱引用的目标。

- `__mro__` 属性

    类都有一个`__mro__`属性,它的值是一个元组， 按照方法解析顺序列出各个超类，从当前类一直向上，直到object类。
    `此属性可以用来查看一个类在继承了多个类之后，是如何执行超类中的函数顺序的。`


- `__getattr__()`

    只有在没有找到属性的情况下，才调用 `__getattr__` ，已有的属性，比如name，不会在 `__getattr__` 中查找。

    可以利用`__getattr__()`方法实现一个链式调用:

    ```python
    class Chain(object):
        def __init__(self, path=''):
            self._path = path
        
        def __getattr__(self, path):
            return Chain('%s/%s' % (this._path, path))

        def __str__(self):
            return self._path
        
        __repr__ = __str__
    ```

    ```python
    >>> Chain().status.user.timeline.list
    '/status/user/timeline/list'
    ```


- 任何python对象都可以表现得像函数，只需实现`__call__`方法。

- 判断对象能否调用，最安全的方法是使用内置的`callable()`函数。

- python 唯一支持的参数传递模式是`共享传参`，即函数的各个形式参数获取实参中各个引用的副本，也就是说，函数内部的形参是实参的别名。

- 不要使用可变类型作为参数的默认值。

- [枚举类的使用](./枚举类.md)

- `类属性` 与 `实例属性`

    1. 类属性 可用于为实例属性提供默认值。
    2. 如果为不存在的 实例属性 赋值，会新建实例属性，那么同名的 类属性 不受影响，此自之后，self.XXX 读取的是实例属性，也就是把同名的 类属性 遮盖住了。

- `itertools.zip_longest` & `zip`

    `itertools.zip_longest` 按最长的可迭代对象进行 , `zip` 按最短的可迭代对象距离进行
```python
from itertools import zip_longest
list(zip_longest(range(3), 'ABC', [0.0, 1.1, 2.2, 3.3], fillvalue=-1)) # fillvalue 默认值为None，用于填充缺失的值。
# out: [(0, 'A', 0.0), (1, 'B', 1.1), (2, 'C', 2.2), (-1, -1, 3.3)]


list(zip(range(3), 'ABC', [0.0, 1.1, 2.2, 3.3]))
#out: [(0, 'A', 0.0), (1, 'B', 1.1), (2, 'C', 2.2)]
```

- `不要子类化内置类型`，直接子类化内置类型(如dict,list 或 str) 容易出错，因为内置类型的方法通常会忽略用户覆盖的方法。 `自定义的类应该继承collections模块中的类` ，例如UserDict,UserList,UserString等等。


- `all(it)` `it`中的所有元素都为真值时返回True, 否则返回False; `all([]) 返回True`

- `any(it)` 只要`it`中有元素为真值就返回True, 否则返回False; `any([]) 返回False`

- 如何判断一个对象是可迭代对象 

    通过 `collections` 模块的Iterable类型判断
    ```python
    from collections import Iterable

    isinstance('abc', Iterable)   # True
    isinstance([1,2,3], Iterable)  # True
    isinstance(123, Iterable) # False
    ```

- 内置的 `enumerate` 函数可以把一个list变成索引-元素对

    ```python
    for i, value in enumerate(['a', 'b', 'c']):
        print(i, value)
    ```

#


### 高阶函数

1. `map(f, sq)` 函数将 f 作用到 sq 的每个元素上去，并返回结果组成的列表
