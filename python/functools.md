+ `functools.wraps` 可以将原函数对象的指定属性复制给包装函数对象, 默认有 `__module__`, `__name__`, `__qualname__`, `__doc__`, `__annotations__`,或者通过参数选择。
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

+ `functools.lru_cache` 实现了备忘功能，是一项优化技术，它把耗时的函数的结果保存起来，避免传入相同的参数时重复计算.`LRU` -> `Least Recently Used`的缩写。

