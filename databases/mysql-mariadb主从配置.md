## 主数据库配置
1. 找到 [mysqld]:
```bash
server-id=1  #这是数据库服务器id主从数据库不能重复，在所有mysql数据库中唯一
log-bin=xxxxx  #二进制文件保存的位置
```
2. 创建用于同步数据的用户与授权:
```sql
CREATE USER 'slave'@'%' IDENTIFIED BY 'slave';

grant file,select,replication slave on *.* to slave@'从数据库ip' identified by 'slave';

flush privileges;
```
3. 查看状态：
```sql
show master status;
```

## 从数据库配置:
1. 找到 [mysqld]:
```bash
server-id = 2
relay-log = /mydata/relaylogs/relay-bin  #这项设置是必须的
#log-bin = /mydata/mysql-bin   //注释不会影响从库，打开也可以
```
3. 依次执行:
```sql
stop slave;

reset slave;

change master to MASTER_HOST='主数据库IP', MASTER_USER='同步用户',MASTER_PASSWORD='同步用户的密码',MASTER_PORT='主数据库的端口';

start slave;
```