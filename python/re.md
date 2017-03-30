## 方法
1. **re.match & re.search**
    
    在 re 模块中， re.match 和 re.search 是常用的两个方法：

    `re.match(pattern, string[, flags])`    
    `re.search(pattern, string[, flags])`

    两者都寻找第一个匹配成功的部分，成功则返回一个 match 对象，不成功则返回 None，不同之处在于 re.match 只匹配字符串的开头部分，而 re.search 匹配的则是整个字符串中的子串.

2. **re.findall & re.finditer**

    `re.findall(pattern, string)` 返回所有匹配的对象。    
     `re.finditer` 则返回一个迭代器。

3. **re.split** 

    `re.split(pattern, string[, maxsplit])` 按照 pattern 指定的内容对字符串进行分割。

4. **re.sub**   

    `re.sub(pattern, repl, string[, count])` 将 pattern 匹配的内容进行替换。

5. **re.compile**   

    `re.compile(pattern)` 生成一个 pattern 对象，这个对象有匹配，替换，分割字符串的方法。