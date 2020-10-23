## 主数据库配置

1. 找到 [mysqld]:
```bash
server-id=1  #这是数据库服务器id主从数据库不能重复，在所有mysql数据库中唯一
log-bin=xxxxx  #二进制文件保存的位置
```
2. 创建用于同步数据的用户与授权:
```mysql
mysql> CREATE USER 'slave'@'%' IDENTIFIED BY 'slave';

mysql> grant file,select,replication slave on *.* to slave@'从数据库ip' identified by 'slave';

mysql> flush privileges;
```
3. 查看状态：
```bash
$ show master status;
# 这里能看到主机的日志文件名，日志Position
```

## 从数据库配置:

1. 找到 [mysqld]:
```bash
server-id = 2 # 这个id必须唯一。
relay-log = /mydata/relaylogs/relay-bin  #这项设置是必须的
#log-bin = /mydata/mysql-bin   //注释不会影响从库，打开也可以
```
3. 依次执行:
```mysql
 stop slave;

 reset slave;

 show slave status \G # 可以查询从机的状态

 change master to MASTER_HOST='主数据库IP', MASTER_USER='同步用户',MASTER_PASSWORD='同步用户的密码',MASTER_PORT='主数据库的端口';

 change master to MASTER_HOST='主数据库IP', MASTER_USER='同步用户',MASTER_PASSWORD='同步用户的密码',MASTER_PORT='主数据库的端口', master_log_file='主数据库的日志文件', master_log_pos= '填写要开始进行同步的位置';
# 如:
 change master to MASTER_HOST='127.0.0.1', MASTER_USER='slave',MASTER_PASSWORD='slave',MASTER_PORT='3306', master_log_file='mysql-bin.000554', master_log_pos= '241158';

 start slave;
```



## 冷备份

```bash
# 1. 收集主机原有数据, 在主机上进行
$ mysqldump -uroot -pmysql --all-databases --lock-all-tables > ~/master_data.sql

# 2. 从机复制主机原有数据 在主机上将数据使用mysql命令复制到从机上
$ mysql -uroot -pmysql -h127.0.0.1 --port=8808 < ~/master_data.sql
```

