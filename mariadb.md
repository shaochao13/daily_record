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


<h1 id="mariadb">mariadb 操作</h1>

## 安装

1. /etc/yum.repos.d/mariadb.repo 
```bash
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.1/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```

然后执行以下命令替换源地址:

```bash
sudo sed -i 's#yum.mariadb.org#mirrors.ustc.edu.cn/mariadb/yum#' /etc/yum.repos.d/mariadb.repo
# 建议使用 HTTPS
sudo sed -i 's#http://mirrors.ustc.edu.cn#https://mirrors.ustc.edu.cn#g' /etc/yum.repos.d/mariadb.repo
```

若安装时遇到错误 “Failed to connect to 2001:da8:d800:95::110: Network is unreachable”，将源地址中的 mirrors.ustc.edu.cn 替换为 ipv4.mirrors.edu.cn 以强制使用 IPv4：

```bash
sudo sed -i 's#//mirrors.ustc.edu.cn#//ipv4.mirrors.ustc.edu.cn#g' /etc/yum.repos.d/mariadb

```



2. 安装mariadb
    ```bash
    yum -y install mariadb mariadb-server
    ```

3. 启动 

    ```bash
    systemctl start mariadb
    ```

    设置开机启动

    ```bash    
    systemctl enable mariadb
    ```

4. 配置

    ```bash
    mysql_secure_installation
    ```

5. 配置MariaDB的字符集

    vi /etc/my.cnf
    在[mysqld]标签下添加
    ```bash
    init_connect='SET collation_connection = utf8_unicode_ci' 
    init_connect='SET NAMES utf8' 
    character-set-server=utf8 
    collation-server=utf8_unicode_ci 
    skip-character-set-client-handshake
    ```

    文件/etc/my.cnf.d/client.cnf
 
    在[client]中添加
    ```
    default-character-set=utf8
    ```

    文件/etc/my.cnf.d/mysql-clients.cnf

    在[mysql]中添加
    ```bash
    default-character-set=utf8
    ```

+ 创建用户命令

    ```sql
    create user username@localhost identified by 'password';
    ```

+ 直接创建用户并授权的命令

    ```sql
    grant all on *.* to username@localhost indentified by 'password';
    ```

+ 授予外网登陆权限 

    ```sql
    grant all privileges on *.* to username@'%' identified by 'password';
    ```

+ 授予权限并且可以授权

    ```sql
    grant all privileges on *.* to username@'hostname' identified by 'password' with grant option;
    ```

+ 刷新权限
    ```sql
    FLUSH PRIVILEGES;
    ```

+ 其中只授予部分权限把 其中 all privileges或者all改为select,insert,update,delete,create,drop,index,alter,grant,references,reload,shutdown,process,file其中一部分


+ 根据数据库名，获取其下面所有的表信息
```sql
SELECT TABLE_NAME, TABLE_COMMENT FROM information_schema.`TABLES` 
WHERE TABLE_SCHEMA ='bihuyihu_test' 
```

+ 根据数据库表名，获取其下面所有的字段的信息
```sql
select TABLE_NAME, COLUMN_NAME, COLUMN_DEFAULT, COLUMN_TYPE, COLUMN_COMMENT from `COLUMNS` where table_schema = 'bihuyihu_test'
```