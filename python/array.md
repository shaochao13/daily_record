如果需要一个只包含数字的列表， 数组 `array.array` 比 list 更高效，并且还能节约空间。

数组支持所有跟可变序列有关的操作。

数组还提供从文件读取和存入文件的更快的方法，如`.fromtypes` `.tofile` `.fromfile`

例如创建一个有 1000万个随机浮点数的数组：
```python
from array import array
from random import random
floats = array('d', (random() for i in range(10**7)))
fp = open('test.bin', 'wb')
#保存为二进制数值文件
floats.tofile(fp)
fp.close()
#从文件中读取二进制数据
floats2 = array(floats.typecode) #floats2 = array('d')
floats2.fromfile(fp, 10**7)
fp.close()

```