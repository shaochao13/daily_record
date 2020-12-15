## 常用属性

`df.shape` -- 返回一个元组， 表示 dataframe有多少行、多少列

`df.columns`  -- 顺序输出每列的名字

`df.index ` -- 顺序输出每行的名字

`df.dtypes` -- 输出每列的数据类型

## 常用函数

`df.head(N)` -- 看前N行的数据，默认是5

`df.tail(N)` -- 看最后N行的数据，默认是5

`df.sample(n=N)` -- 随机抽取N行 ， 用frac参数可以随机抽取百分之多少的行，`df.sample(frac=0.1)`表示抽取10%的数据

`df.describe()` -- 对每列的数据求 count, mean,std,min,max等等。非常有用。

`pd.set_option('expand_frame_repr', False)` -- 当列太多时，显示时不换行

`pd.set_option('max_colwidth', 20)`  -- 设定每一列的最大宽度

  

## 读取数据

### 1. read_csv

```python
#常用参数说明：
pd.read_csv(
  filepath_or_buffer='./table.csv', # 数据的路径
  sep=',', # 数据的分隔符
  skiprows=1, #表示跳过数据文件中的第1行不读入
  nrows=5, # 表示只读取前n行数据，若不指定，则读入全部的数据
  index_col=['dateId'], # 指定列设置为index.如果不指定，index默认为0,1,2,3,……
  usecols=['dateId', 'name', 'age', 'amount'], # 读取指定列的数据，其他数据列的数据不读取。如果不指定，则读取全部列数据
  error_bad_lines=False, #当某行数据有问题时，报错。设定为False时表示不报错，直接跳过该行
  na_values='NULL', # 将数据中的null识别为空值
)
```



## 取数据

`df['colName']` -- 取出colName列的数据，Series类型

`df[['colName1', 'colName2']]`  -- 同时取出colName1,colName2列的数据，DataFrame类型

`df[[0,1,2]]` -- 同时取出第0、1、2列的数据



`df.loc['indexName']` -- 选取index为'indexName' 一行的数据。 Series类型

`df.loc['indexName1':'indexName2']` -- 选取index为indexName1和indexName2之间的多行的数据。 DataFrame类型

`df.loc[:,'colName1':'colName2']` -- 选取columns在'colName1'至'colName2'之间的多列的数据。DataFrame类型

`df.loc['indexName1':'indexName2','colName1':'colName2']` -- 选取index为indexName1和indexName2之间,columns在'colName1'至'colName2'之间的多列的数据。DataFrame类型

`df.at['indexName', 'colName']` 选择指定位置的一个元素。`df.loc['indexName', 'colName']`  也可以，但性能`at`更高。



`df.iloc`与`df.loc` 一样，只是它是通过index,columns的position来读取数据。

`df.loc[0]`  --- 表示选取第0行的数据

`df.loc[1:3]`  --- 表示选取第1-3行的数据

`df.loc[:,1:3]`  --- 表示选取第1-3列的数据

`df.loc[1:3，1:3]`  --- 表示选取index 在1-3之间，columns在1-3位置上的列的数据。

`df.iat` 与`df.at` 同样。

`df.iat[index_position, column_position]` 