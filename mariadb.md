A "/etc/my.cnf" from another install may interfere with a Homebrew-built
server starting up correctly.

MySQL is configured to only allow connections from localhost by default

To connect:
    mysql -uroot

To have launchd start mariadb now and restart at login:
  brew services start mariadb
Or, if you don't want/need a background service you can just run:
  mysql.server start



# “Access denied for user 'root'@'localhost' (using password:YES)” 问题解决方法
1. 打开MySQL目录下的my.ini文件，在文件的最后添加一行“skip-grant-tables”，保存并关闭文件。
2. 重启MySQL服务。
3. 在命令行中输入“mysql -uroot -p”(不输入密码)，回车即可进入数据库。
4. 执行，“use mysql;”使用mysql数据库。
5. 执行，“update user set password=PASSWORD("rootadmin") where user='root';”（修改root的密码）
6. 打开MySQL目录下的my.ini文件，删除最后一行的“skip-grant-tables”，保存并关闭文件。
7. 重启MySQL服务。
8. 在命令行中输入“mysql -uroot -prootadmin”，问题搞定！



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

-- 返回结果中：
charater_set_client --> 表示服务器默认的客户端传来的数据字符集
charater_set_connection --> 表示连接层字符集
charater_set_database --> 表示当前数据库的字符集
charater_set_results --> 表示服务器默认的对外处理的字符集
```


# 
## 列显示宽度进行零填充(`zerofill`)
在于当数据不够显示宽度的时候，会自动让数据变成对应的显示宽度，通常需要搭配一个前导0来增加宽度，其不改变数据值的大小，即用 `zerofill` 进行零填充，`并且零填充会导致数值自动变成无符号`。
```sql
create table my_int(int_1 int zerofill)charset utf8;

insert into my_int values(6);

select * from my_int; --返回的int_1的值为'0000000006'
```

## timestamp 自动更新，以及update时自动更新

```sql
`create_time` timestamp not null default current_timestamp comment '创建时间'

`update_time` timestamp not null default current_timestamp on update current_timestamp comment '修改时间'
```