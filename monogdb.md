* 单个数据库默认最多可以创建24000个名称空间。每个集合至少包含两个名称空间：一个用于集合自身，另一个用于集合中创建的第一个索引。如果每个集合都只含有一个索引，那么每个数据库默认最多可以拥有12000个集合。不过，可以通过nssize 参数增加名称空间的数目限制。

* 键的名字必须遵守如下规则：
> $ 字符不能是键名的第一个字符。  
> 圆点“.” 不能出现在键名中。

* 集合的名称必须遵守如下规则：
> 集合的名称不能超过128个字符。  
> 集合名称必须以字母或下划线开头。  
> 集合名system 被mongodb保留，不能使用。    
> 集合名不能包含null字符"\0"。    


# 索引
- 每个集合最多可以拥有**40**个索引。
- 所有索引信息都存在在数据库的system.indexes集合中，可以运行```db.indexes.find()```来查看目前已经存储的索引。

#地理空间索引
- 要添加地理空间信息的文档必须含有一个子对象或者数组(第一个元素指定了对象类型，紧接着是该元素的经度和纬度)，如：
``` 
db.restaurants.insert({name:"Kimono",loc:{type:"Point",coordinates:[52.370451,5.217497]}}) 
```  
    其中**type** 参数 可以是Point、LineString、Polygon。
    1. Point 类型用于指定某个条目所在的准确位置，因此需要两个值：经度和纬度。
    2. LineString 类型可用于指定某个沿着特定路线扩展的条目，因此需要起点和终点。   
    如： 
    ``` 
     db.streets.insert({name:"Westblask",loc:{type:"LineString",coordinates:[[52.36881,4.890286],[52.368762,4.890021]]}}) 
     ```
    3. Polygon 类型可用于指定图形(如购物区域)。使用时，需要保证起点和终点是一致的，从而可以闭合这个环。
    如： 
    ``` 
    db.stores.insert({name:"SuperMall",loc:{type:"Polygon",coordinates:[[[52.146917,5.374337],[52.146966,5.375471],[52.146722,5.375085],[52.146744,5.37437],[52.146917,5.374337]]]}})
    ```        

- 一旦在文档中添加了地理空间信息，就可以创建此种类型的索引,如 
    ``` 
    db.restaurants.ensureIndex({loc:"2dsphere"})
    ```

# 查询数据
1. 在使用复杂文档结构时，可以使用点[.]，告诉find函数查找文档中内嵌的信息。  
2. sort() 函数， 如果指定一个不存在的键用于排序，结果将按照文档插入的顺序返回。   
3. limit() 函数， 如果使用的参数为 0， 那将返回所有结果。
4. find() 函数中使用快捷方法忽略并限制结果的数目：```find({},{},10,20)``` 首先将忽略开头的20个文档，然后将结果数目限制为10个。

# 固定集合
1. 固定集合必须使用***createCollection*** 函数显式创建，***必须指定集合的大小***。如下例创建一个固定集合，它最大不能超过20480字节：
```
db.createCollection("audit",{capped:true, size:20480})
``` 
还可以使用max参数限制添加到固定集合中的文档数量。但如果在文档数目达到上限之前，数据大小先达到上限，那么最老的文档将被删除。

2. 固定集合中的文档可以被更新，但文档大小不能改变，如果大小改变，更新将会失败。  
3. 不可以从固定集合中删除文档，如果希望删除文档，就必须删除整个集合并重建。

# 聚集命令
## count() 
返回指定集合中的文档数目。    count()函数默认将忽略skin() 或limit() 参数。为了确保查询不会被忽略这些参数，保证进行计数的结果都符合limit()\skip()参数，使用***count(true)***。
如： 
``` 
db.media.find({Publisher:"Apress",Type:"Book"}).skip(2).count(true)
```
---

## distinct() 
函数获取唯一值 。
如返回集合中 Title 键的唯一值列表：
```
db.media.distinct("Title")
```
还可以接受嵌套键：
```
db.media.distinct("Tracklist.Title")
```
---

## group()
返回一个已经分组元素的数组。  
> 接受3个参数：     
- key -- 指定希望使用哪个键对结果进行分组。    
- initial -- 为每个已分组的结果提供基数（元素开始统计的起始基数）。  
- reduce -- 将接受两个参数：正在遍历的当前文档 和 聚集计数对象。items、prev 
    
如：    
```
db.media.group({
    key: {
        Title: true
    },
    initial: {
        Total: 0
    },
    reduce: function(items, prev) {
        prev.Total += 1;
    }
})
```    
group()函数目前在分片环境中无法正常工作。如果要在分片环境中，应该使用mapreduce()， group()函数的输出结果中包含的键不能超过1000个，否则将会抛出异常,也可以使用mapreduce()。

---

# 条件操作符 (https://docs.mongodb.org/manual/reference/operator/query/)

* ***$gt(大于), $gte(大于等于), $lt(小于), $lte(小于等于)***
```
db.media.find({Released:{$gt:2000}})
db.media.find({Released:{$gte:1999}})
db.media.find({Released:{$lt:1999}})
db.media.find({Released:{$lte:1999}})
db.media.find({Released:{$gte:1990, $lt:2010}})
``` 
 
* ***$ne*** 获取集合中除某些符合特定条件之外的所有文档。    如，下面将返回作者不是Eelco Plugge 的所有图书列表：
```
db.media.find({Type:"Book", Author: {$ne: "Plugge, Eelco"}})
```    

* ***$in***  指定一组可能的匹配值。对应 SQL 中的操作符"IN"。  如：
```
db.media.find( {Released: {$in: [1999,2000,2009] } } )
```

* ***$nin*** 查找不在数组中的文档。  如：
```
db.media.find( {Released: {$nin: [1999,2000,2009] } } )
```

* ***$all*** 与$in类似，但$all 要求条件的属性值都匹配。

* ***$or*** 将返回满足其中任何一个条件的文档，与$in 不同，$or 允许同时指定键和值，而不是只指定值。
```
db.media.find({ $or: [ {Title: "Toy Story 3"}, {"ISBN": "987-1-4302-3051-9" } ] })
db.media.find({ Type: "DVD", $or: [ {Title: "Toy Story 3"}, {"ISBN": "987-1-4302-3051-9" } ] })
```

* ***$slice***  获取的文档将只包含数组中特定范围的值。
语法如下：
```
db.collection.find( { field: value }, { array: {$slice: count } } );
```
返回Cast列表中的前3项：
```
db.media.find({"Title":"Matrix, The", { "Cast":{ $slice: 3 } }})
```
返回Cast列表中的后3项：
```
db.media.find({"Title":"Matrix, The", { "Cast":{ $slice: -3 } }})
```
忽略前两项，并返回忽略之后的前3项：
```
db.media.find({"Title":"Matrix, The", { "Cast":{ $slice: [2,3] } }})
```

* ***$mod*** 可以用来搜索由奇数或者偶数组成的特定数据。
语法如下：
```
{ field: { $mod: [ divisor, remainder ] } }
``` 
返回集合中任何 Released 字段为偶数的文档：
```
db.media.find({ Released: {$mod: [2,0]} })
```
返回集合中任何 Released 字段为奇数的文档：
```
db.media.find({ Released: {$mod: [2,1]} })
```
返回集合中 qty 字段的值能为 4 整除的文档：
```
db.inventory.find( { qty: { $mod: [ 4, 0 ] } } )
```
*$mod 只能作用于整数，不能作用于包含数值的字符串，例如不能用于{Released:"1999"}，因为1999d在引号中只是个字符串。*
 
* ***$size***  可以过滤出文档中数组大小符合条件的结果。 
例如，返回只含有两首歌曲的CD:
```
db.media.find({ Tracklist: { $size: 2 } })
```

* ***$exists*** 返回含有或者不含有特定字段的文档。   
例如， 返回集合中含有键Author的所有文档：
```
db.media.find({ Author: { $exists: true } })
```

* ***$elemMatch***  匹配文档中的完整数组。     
语法如下：
```
{ <field>: { $elemMatch: { <query1>, <query2>, ... } } }
```
*< field >* 为数组，而对其有两个以上的查询条件时，就使用$elemMatch ，如果只有一个查询条件，就没有必要使用。   
返回 集合中的 results 数组中大于等于80 ，且小于85的文档：
```
db.scores.find({ results: { $elemMatch: { $gte: 80, $lt: 85 } } })
```

* ***$not***    否定任何标准操作符执行的检查。     
返回price 小于等于1.99 或者 price字段不存在的文档：
```
db.inventory.find( { price: { $not: { $gt: 1.99 } } } )
```

# 更新数据操作符
* ***$set*** 将某个字段设置为指定值。 如：
```
db.media.udpate({ "Title":"Matrix, The" }, { $set: { Genre: "Sci-Fi" } })
```

* ***$unset***  删除指定的字段。 如：
```
db.media.update({ "Title": "Matrix, The" }, { $unset: { "Genre" : 1 } })
```

* ***$push*** 往数组字段中添加某个值。 如：
```
db.media.update({ "ISBN":"978-1-4302-5821-6" }, { $push: { Author: "Griffin, Stewie" } })
```
与*$each* 组合 可以往数组字段中添加多个值。如：
```
db.media.update({ "ISBN":"978-1-4302-5821-6" },{ $push: {Author: { $each: [ "Griffin, Peter", "Griffin, Brian" ] }} })
```
**$push + $each + $slice** 可以用来限制一个数组字段的数据个数。如： 
下面操作不公保证两个新值会被加到数组中，还保证将把数组的大小限制为指定值（2）。
```
db.media.update({ "ISBN":"978-1-4302-5821-6" },{ $push: { Author: { $each: [ "Griffin, Peter", "Griffin, Brian" ] ,$slice: -2 } } })
```



#####

To have launchd start mongodb now and restart at login:
  brew services start mongodb
Or, if you don't want/need a background service you can just run:
  mongod --config /usr/local/etc/mongod.conf