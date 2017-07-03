- `@contextmanger` 装饰器
    能减少创建上下文管理器的代码量，不用定义`__enter__` 和 `__exit__` 方法，面只需要实现有一个 `yield` 语句的生成器，生成想让`__enter__`方法返回的值。

    `yield` 语句把函数的定义划分成两部分：yield 语句前面的所有代码在`with`块开始时（即解释器调用 `__enter__`方法时）执行，`yield` 语句后面的代码在`with`块结束时（即调用 `__exit__` 方法时）执行。

    ```python
    import contextlib

    @contextlib.contextmanager
    def looking_glass():
        import sys
        original_write = sys.stdout.write

        def reverse_write(text):
            original_write(text[::-1])

        sys.stdout.write = reverse_write
        yield 'JABBERWOCRY'

        sys.stdout.write = original_write
    ```