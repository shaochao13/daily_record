MySQL is configured to only allow connections from localhost by default

To connect:
    mysql -uroot

To have launchd start mariadb now and restart at login:
  brew services start mariadb
Or, if you don't want/need a background service you can just run:
  mysql.server start



# 校对集问题

校对集，其实就是数据的比较方式。

校对集，共有三种，分别为：   
`_bin`：binary，二进制比较，区分大小写；  
`_cs`：case sensitive，大小写敏感，区分大小写；   
`_ci`：case insensitive，大小写不敏感，不区分大小写。   

查看（全部）校对集 –> 基本语法：`show collation;`   

`校对集必须在没有数据之前声明好，如果有了数据之后，再进行校对集的修改，则修改无效。`


# 中文数据问题

中文数据问题的本质就是字符集的问题。

### 查看服务器识别的全部字符集
```sql
show character set;
```   

### 查看服务器默认的对外处理的字符集
```sql
show variables like 'character_set%';

-- 返回结果中：
charater_set_client --> 表示服务器默认的客户端传来的数据字符集
charater_set_connection --> 表示连接层字符集
charater_set_database --> 表示当前数据库的字符集
charater_set_results --> 表示服务器默认的对外处理的字符集
```