## 方法
1. **re.match & re.search**
    
    在 re 模块中， re.match 和 re.search 是常用的两个方法：

    `re.match(pattern, string[, flags])`    
    `re.search(pattern, string[, flags])`

    两者都寻找第一个匹配成功的部分，成功则返回一个 match 对象，不成功则返回 None，不同之处在于 re.match 只匹配字符串的开头部分，而 re.search 匹配的则是整个字符串中的子串.

    ```python
    string = 'hello there'
    pattern = 'hello (\w+)'

    match = re.match(pattern, string)
    if match is not None:
        print match.group(0)
        print match.group(1)
    ```
    通常，match.group(0) 匹配整个返回的内容，之后的 1,2,3,... 返回规则中每个括号（按照括号的位置排序）匹配的部分

2. **re.findall & re.finditer**

    `re.findall(pattern, string)` 返回所有匹配的对象。    
     `re.finditer` 则返回一个迭代器。

3. **re.split** 

    `re.split(pattern, string[, maxsplit])` 按照 pattern 指定的内容对字符串进行分割。

4. **re.sub**   

    `re.sub(pattern, repl, string[, count])` 将 pattern 匹配的内容进行替换。

5. **re.compile**   

    `re.compile(pattern)` 生成一个 pattern 对象，这个对象有匹配，替换，分割字符串的方法。

    如果某个 pattern 需要反复使用，那么我们可以将它预先编译

    ```python
    pattern1 = re.compile('hello (\w+)')

    match = pattern1.match(string)
    if match is not None:
        print match.group(1)
    ```



## 正则表达式规则

子表达式|	匹配内容
--:|--
.	|匹配除了换行符之外的内容
\w|	匹配所有字母和数字字符
\d|	匹配所有数字，相当于 [0-9]
\s|	匹配空白，相当于 [\t\n\t\f\v]
\W,\D,\S|	匹配对应小写字母形式的补
[...]	|表示可以匹配的集合，支持范围表示如 a-z, 0-9 等
(...)|	表示作为一个整体进行匹配
¦	|表示逻辑或
^	|表示匹配后面的子表达式的补
*	|表示匹配前面的子表达式 0 次或更多次
+	|表示匹配前面的子表达式 1 次或更多次
?	|表示匹配前面的子表达式 0 次或 1 次
{m}	|表示匹配前面的子表达式 m 次
{m,}	|表示匹配前面的子表达式至少 m 次
{m,n}	|表示匹配前面的子表达式至少 m 次，至多 n 次
--|--