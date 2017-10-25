

生成器都是 Iterator 对象，但list、dict、str虽然是Iterable，却不是Iterator。

可以被next()函数调用并不断返回下一个值的对象称为迭代器：Iterator。


可以使用isinstance()判断一个对象是否是Iterator对象:
```python
>>> from collections import Iterator
>>> isinstance((x for x in range(10)), Iterator)
True
>>> isinstance([], Iterator)
False
>>> isinstance({}, Iterator)
False
>>> isinstance('abc', Iterator)
False
```

把list、dict、str等Iterable变成Iterator可以使用iter()函数:
```python
>>> isinstance(iter([]), Iterator)
True
>>> isinstance(iter('abc'), Iterator)
True
```

Iterator对象表示的是一个数据流，Iterator对象可以被next()函数调用并不断返回下一个数据，直到没有数据时抛出StopIteration错误。可以把这个数据流看做是一个有序序列，但我们却不能提前知道序列的长度，只能不断通过next()函数实现按需计算下一个数据，所以Iterator的计算是惰性的，只有在需要返回下一个数据时它才会计算。

+ 凡是可作用于for循环的对象都是Iterable类型；

+ 凡是可作用于next()函数的对象都是Iterator类型，它们表示一个惰性计算的序列；

+ 集合数据类型如list、dict、str等是Iterable但不是Iterator，不过可以通过iter()函数获得一个Iterator对象。
