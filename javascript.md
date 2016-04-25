1. 操作符之间的优先级（高到低）：
> 算术操作符 --> 比较操作符 --> 逻辑操作符 --> “=” 赋值符号    

# Date对象
1. *get/setFullYear()* 返回/设置年份，用**四位**数表示。
2. *getDay()* 返回星期，返回的是*0-6*的数字，**0**表示星期天。
3. *get/setTime()* 返回/设置时间，单位**毫秒数**，计算从*1970年1月1日零时*到日期对象所指的日期的毫秒数。
> 例如：如果将目前日期对象的时间推迟1小时：
```javascript
<script type="text/javascript">
  var mydate=new Date();
  document.write("当前时间："+mydate+"<br>");
  mydate.setTime(mydate.getTime() + 60 * 60 * 1000);
  document.write("推迟一小时时间：" + mydate);
</script>
```
     
# 字符串
1. toUpperCase()/toLowerCase() 把字符串转变为大写/小写。
2. charAt() 返回指定位置的字符。
3. indexOf() 返回某个指定字符串值在字符串中的首次出现的位置。   
> 语法：stringObject.indexOf(substring, startpos) 如果要检索的字符串值没有出现，则返回-1。
4. split() 将字符串分割为字符串数组，并返回此数组。
> 语法：stringObject.split(sparator, limit) 。如把空字符串("")用作separator,那stringObject中的每个字符之间都会被分割。 
5. substring() 提取字符串中介于两个指定下标之间的字符。
> 语法：stringObject.substring(starPos, stopPos) 
    - 返回的内容是从 start开始(包含start位置的字符)到 stop-1 处的所有字符，其长度为 stop 减start。
    - 如果参数 start 与 stop 相等，那么该方法返回的就是一个空串（即长度为 0 的字符串）。
    - 如果 start 比 stop 大，那么该方法在提取子串之前会先交换这两个参数。
            
6. substr() 从字符串中提取从startPos位置开始的指定数目的字符串。
> 语法：stringObject.substr(startPos,length)。  
**注意：**
    - 如果参数startPos是负数，从字符串的尾部开始算起的位置。也就是说，-1 指字符串中最后一个字符，-2 指倒数第二个字符，以此类推。
    - 如果startPos为负数且绝对值大于字符串长度，startPos为0。
      
# Math对象
1. ceil() 向上取整，语法：Math.ceil(x),返回的是大于或者等于x,并且与x最接近的整数。 floor()方法与ceil()相反，它为向下取整。
2. round() 把一个数字四舍五入为最接近的整数。  语法：Math.round(x)
    - 返回与x最接近的整数。
    - 对于0.5,将进行上舍入。（5.5将舍入为6）
    - 如果x与两侧整数同等接近，则结果接近*正无穷大*方向的数字值。   

# Array 数组对象
数组对象是一个对象的集合，里边的对象可以是不同类型的。
1. concat() 用于连接两个或多个数组，此方法返回一个新数组，不改变原来的数组。
    > 语法：
    arrayObject.concat(array1,array2,...,arrayN);
2. join() 用于把数组中的所有元素通过指定的分隔符放入一个字符串。
    > 语法：
    arrayObject.join(分隔符);  //如果省略“分隔符”， 则使用逗号作用分隔符。
3. reverse() 用于颠倒数组中元素的顺序。
    > 语法：
    arrayObject.reverse()  会改变原来的数组，而不会创建新的数组。
4. slice() 切片函数，与python中的切片功能一样。
    > 语法：
    arrayObject.slice(start,end);    
5. sort() 排列。
    > 语法：
    arrayObject.sort(方法函数);  // “方法函数”可以没有。
    

