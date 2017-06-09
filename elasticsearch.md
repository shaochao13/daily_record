一个 Elasticsearch 请求和任何 HTTP 请求一样由若干相同的部件组成: 

```sh
curl -X<VERB> '<PROTOCOL>://<HOST>:<PORT>/<PATH>?<QUERY_STRING>' -d '<BODY>'
```
参数名|说明
-|-
VERB|适当的 HTTP 方法 或 谓词 : GET`、 `POST`、 `PUT`、 `HEAD 或者 `DELETE`。
PROTOCOL|http 或者 https`（如果你在 Elasticsearch 前面有一个 `https 代理）
HOST|Elasticsearch 集群中任意节点的主机名，或者用 localhost 代表本地机器上的节点。
PORT|运行 Elasticsearch HTTP 服务的端口号，默认是 9200 。
PATH|API 的终端路径（例如 _count 将返回集群中文档数量）。Path 可能包含多个组件，例如：_cluster/stats 和 _nodes/stats/jvm 。
QUERY_STRING|任意可选的查询字符串参数 (例如 ?pretty 将格式化地输出 JSON 返回值，使其更容易阅读)
BODY|一个 JSON 格式的请求体 (如果请求需要的话)


# 

## 文档元数据

+ `_index` 表示文档在哪存放 （必须小写，不能以下划线开头，不能包含逗号）
+ `_type` 文档表示的对象类别 （可以是大写或者小写，但是不能以下划线或者句号开头，不应该包含逗号， 并且长度限制为256个字符）
+ `_id` 文档唯一标识

_index 、 _type 和 _id 的组合可以唯一标识一个文档


#

1. 存储数据到elasticsearch的行为叫做 `索引`

***索引（名词）：*** 

一个 索引 类似于传统关系数据库中的一个 数据库 ，是一个存储关系型文档的地方。 索引 (index) 的复数词为 indices 或 indexes 。

***索引（动词）：***

索引一个文档 就是存储一个文档到一个 索引 （名词）中以便它可以被检索和查询到。这非常类似于 SQL 语句中的 INSERT 关键词，除了文档已存在时新文档会替换旧文档情况之外。

***倒排索引：***

关系型数据库通过增加一个 索引 比如一个 B树（B-tree）索引 到指定的列上，以便提升数据检索速度。Elasticsearch 和 Lucene 使用了一个叫做 倒排索引 的结构来达到相同的目的。

`默认的，一个文档中的每一个属性都是 被索引 的（有一个倒排索引）和可搜索的。一个没有倒排索引的属性是不能被搜索到的。`

***文档：***
在Elasticsearch中，文档是不可改变的，不能修改它们。

执行修改之类的操作，会执行如下步骤：
> 1. 从旧文档构建 JSON
> 2. 更改该 JSON
> 3. 删除旧文档
> 4. 索引一个新文档


## 集群健康
```sh
GET     /_cluster/health
```
其中 返回的`status`字段：   

    green     所有的主分片和副本分片都正常运行。       
    yellow    所有的主分片都正常运行，但不是所有的副本分片都正常运行。        
    red       有主分片没能正常运行。

## 处理冲突
在数据库领域中，有两种方法通常被用来确保并发更新时变更不会丢失：

+ 悲观并发控制    

    这种方法被关系型数据库广泛使用，它假定有变更冲突可能发生，因此阻塞访问资源以防止冲突。 一个典型的例子是读取一行数据之前先将其锁住，确保只有放置锁的线程能够对这行数据进行修改。

+ 乐观并发控制

    Elasticsearch 中使用的这种方法假定冲突是不可能发生的，并且不会阻塞正在尝试的操作。 然而，如果源数据在读写当中被修改，更新将会失败。应用程序接下来将决定该如何解决冲突。 例如，可以重试更新、使用新的数据、或者将相关情况报告给用户。

    可以利用 `_version` 号来确保 应用中相互冲突的变更不会导致数据丢失。

    `通过外部系统使用版本控制`,通过指定 `version_type=external` 到查询字符串的方式,例如使用 *mysql* 中的 timestamp就能达到控制版本号的效果。

    ```bash
    PUT /website/blog/2?version=5&version_type=external
    {
    "title": "My first external blog entry",
    "text":  "Starting to get the hang of this..."
    }
    ```

## 路由文档到分片
  当索引一个文档的时候，文档会被存储到一个主分片中。 所以在创建索引的时候就确定好主分片的数量，并且永远不会改变这个数量。
如何决定文档被存储在哪个分片上的计算公式：
```bash
shard = hash(routing) % number_of_primary_shards
 # routing 是一个可变值，默认是文档的 _id ，也可以设置成一个自定义的值
```

  所有的文档 API（ get 、 index 、 delete 、 bulk 、 update 以及 mget ）都接受一个叫做 routing 的路由参数 ，通过这个参数我们可以自定义文档到分片的映射。一个自定义的路由参数可以用来确保所有相关的文档——例如所有属于同一个用户的文档——都被存储到同一个分片中

## 操作

+ 查询所有文档
```
GET /website/blog/_search
```

+ 只返回 `_source` 字段的数据

例如：
```
GET /website/blog/123/_source
```

+ 只返回 `_source` 字段，并只返回它中的部分字段的数据

例如：
```bash
# 表示返回title,text字段的数据
GET /website/blog/123/_source?_source_include=title,text 
# 表示返回除title,text字段之外的字段数据
GET /website/blog/123/_source?_source_exclude=title,text
```

+ 更新整个文档

例如：
```bash
PUT /website/blog/123
{
  "title": "My first blog entry",
  "text":  "I am starting to get the hang of this...",
  "date":  "2014/01/02"
}
```

+ 创建文档

    `如果具有相同的 _index 、 _type 和 _id 的文档已经存在，Elasticsearch 将会返回 409 Conflict 响应码`

+ 让elasticsearch 自动生成唯一 `_id`：(使用 `POST`)
```bash
POST /website/blog/
{
  "title": "My first blog entry",
  "text":  "I am starting to get the hang of this...",
  "date":  "2014/01/02"
}
```

+ 自己提供`_id`: (使用 `PUT`)
```bash
PUT /website/blog/123/_create
{
  "title": "My first blog entry",
  "text":  "I am starting to get the hang of this...",
  "date":  "2014/01/02"
}

or 

PUT /website/blog/123?op_type=create
{
  "title": "My first blog entry",
  "text":  "I am starting to get the hang of this...",
  "date":  "2014/01/02"
}
```

5. 删除文档
```bash
DELETE /website/blog/123
```