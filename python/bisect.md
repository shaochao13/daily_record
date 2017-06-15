bisect 模块包含两个主要函数， `bisect` 和 `insort` , 两个函数都利用二分查找法来在有序序列中查找或者插入元素。

```python
data = [4, 2, 9, 7]
data.sort()
# [2, 4, 7, 9]
```

+ `bisect.bisect` 其目的在于查找该数值将会插入的位置并返回，而不会插入, `bisect.bisect` 与 `bisect.bisect_right` 作用一样，即如果有相同数值时，相同数值的右侧为即插入数值的位置。     
`bisect.bisect_left` 即如果有相同数值时，则相同数值的左侧为即插入数值的位置。
```python
bisect.bisect(data, 1)  #out: 0
bisect.bisect(data, 2)  #out: 1
bisect.bisect_right(data, 2)  #out: 1
bisect.bisect_left(data, 2) #out:0
```

+ `bisect.insort` 插入新元素，`bisect.insort(seq, item)` 把变量`item` 插入到序列 `seq` 中， 并能保持 seq 的升序顺序。     
`bisect.insort(seq, item)` 与 `bisect.insort_right（seq, item)` 作用一样，即如果插入数值与seq中的数值相同， 则在相同数值的右侧插入。
```python
bisect.insort(data, 3)
# data --> [2, 3, 4, 7, 9]
```

