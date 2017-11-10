# 4个重要的类型
1. `@Variable` 计算图谱中的变量
2. `@Tensor` 一个多维矩阵，带有很多方法
3. `@Graph` 一个计算图谱
4. `@Session` 用来运行一个计算图谱

+ 使用图 (graph) 来表示计算任务.
+ 在被称之为 会话 (Session) 的上下文 (context) 中执行图.
+ 使用 tensor 表示数据.
+ 通过 变量 (Variable) 维护状态.
+ 使用 feed 和 fetch 可以为任意的操作(arbitrary operation) 赋值或者从其中获取数据.

# 三个重要的入门函数
1. Variable 变量
```python
tf.Variable.__init__(
    initial_value=None, @Tensor
    trainable=True,
    collections=None,
    validate_shape=True,
    caching_device=None,
    name=None,
    variable_def=None,
    dtype=None
)
```

2. Constant 常数
```python
tf.constant(value, dtype=None, shape=None, name='Const')
# return a constant @Tensor
```

3. Placeholder 暂时变量
```python
tf.placeholder(dtype, shape=None, name=None)
#return: 一个还尚未存在的 @Tensor
```