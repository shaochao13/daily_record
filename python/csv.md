### 读 csv 文件

默认数据内容都被当作字符串处理

```python
fp = open("data.csv")
r = csv.reader(fp)
for row in r:
    print row
    
fp.close()
```

### 写 csv 文件

一般要用 'wb' 即二进制写入方式，防止出现换行不正确的问题

```python
data = [('one', 1, 1.5), ('two', 2, 8.0)]
with open('out.csv', 'wb') as fp:
    w = csv.writer(fp)
    w.writerows(data)
```

### 更换分隔符

默认情况下，csv 模块默认 csv 文件都是由 excel 产生的，实际中可能会遇到这样的问题

```python
data = [('one, \"real\" string', 1, 1.5), ('two', 2, 8.0)]
with open('out.csv', 'wb') as fp:
    w = csv.writer(fp)
    w.writerows(data)
```

可以修改分隔符来处理这组数据

```python
data = [('one, \"real\" string', 1, 1.5), ('two', 2, 8.0)]
with open('out.psv', 'wb') as fp:
    w = csv.writer(fp, delimiter="|")
    w.writerows(data)
```


numpy.loadtxt() 和 pandas.read_csv() 可以用来读写包含很多数值数据的 csv 文件

如：

使用 pandas 进行处理，生成一个 DataFrame 对象

```python
import pandas
df = pandas.read_csv('trades.csv', index_col=0)
```
