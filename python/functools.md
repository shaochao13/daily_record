+ [`functools.reduce`](#reduce) 
+ [`functools.wraps`](#wraps)   
+ [`functools.lru_cache`](#lru_cache)     
+ [`functools.singledispatch`](#singledispatch)  
 

## <span id="reduce">`functolls.reduce`</span>
`reduce(function, sequence[, initial]) -> value`

reduce是一个二元操作函数，用来将一个数据集合中的所有数据传给function函数先对集合中的第1、2个数据进行操作，得到的结果再与第三个数据用function()函数运算，依此类推，最后得到一个结果。  reduce就是要把一个list给缩成一个值。
```python
from functools import reduce

l = [1,2,3,4,5]
print(reduce(lambda x, y: x + y , l))
# out: 15

print(reduce(lambda x, y: x + y , l, 10))
#out: 25

```

## <span id="wraps">`functools.wraps`</span> 
可以将原函数对象的指定属性复制给包装函数对象, 默认有 `__module__`, `__name__`, `__qualname__`, `__doc__`, `__annotations__`,或者通过参数选择。
```python
from functools import wraps
def logged(func):
    #这样就把func的一些属性带进来了
    @wraps(func) 
    def with_logging(*args, **kwargs):
        print func.__name__ + " was called"
        return func(*args, **kwargs)
    return with_logging
 
@logged
def f(x):
   """does some math"""
   return x + x * x
 
print f.__name__  # prints 'f'
print f.__doc__   # prints 'does some math'
```

## <span id="lru_cache">`functools.lru_cache(maxsize=128, typed=False)`</span>

    实现了备忘功能，是一项优化技术，它把耗时的函数的结果保存起来，避免传入相同的参数时重复计算.`LRU` -> `Least Recently Used`的缩写。
    `maxsize`应该设为2的幂  
    被lru_cache装饰的函数，它的所有参数都必须是可散列的。
    
```python
import time
import functools

def clock(func):
    def clocked(*args):
        t0 = time.perf_counter()
        result = func(*args)
        elapsed = time.perf_counter() - t0
        name = func.__name__
        arg_str = ', '.join(repr(arg) for arg in args)
        print('[%0.8fs] %s(%s) -> %r' % (elapsed, name, arg_str, result))
        return result
    return clocked
#如果此处不加@functools.lru_cache()，则不会进行任何缓存。
@functools.lru_cache()
@clock
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n-2) + fibonacci(n-1)

if __name__ == '__main__':
    print(fibonacci(100))
```

## <span id="singledispatch">`functools.singledispatch`</span> (python3.4新增)
functools.singledispatch 装饰器能把整体方案拆分成多个模块，使用`@singledispatch` 装饰的普通函数会变成 `泛函数`：根据第一个参数的类型，以不同方式执行相同操作的一组函数。

例如：
```python
from functools import singledispatch
from collections import abc
import numbers
import html
'''
根据传入的数据的数据类型使用不同的方法
htmlize({1,3,4})
htmlize(tuple)
htmlize([1,3,"asdfa",{2,34,2}])
'''

@singledispatch
def htmlize(obj):
    content = html.escape(repr(obj))
    return '<pre>{} </pre>'.format(content)

@htmlize.register(str)
def _(text):
    content = html.escape(text).replace('\n', '<br>\n')
    return '<p>{0}</p>'.format(content)

@htmlize.register(numbers.Integral)
def _(n):
    return '<pre>{0}(0x{0:x})</p>'.format(n)

@htmlize.register(tuple)
@htmlize.register(abc.MutableSequence)
def _(seq):
    inner = '</li>\n<li>'.join(htmlize(item) for item in seq)
    return '<ul>\n<li>' + inner + '</li>\n</ul>'
```