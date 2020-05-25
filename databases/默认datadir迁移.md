## 将ubuntu下的mariadb数据库的默认datadir迁移到/home目录下的方法
1. 修改默认datadir  
```bash
mkdir /home/mysqldata

sudo chown mysql:mysql /home/mysqldata
```
2. 然后进行拷贝
```bash
sudo rsync -avzh /var/lib/mysql /home/mysqldata
```
3. 接下来改变默认的datadir配置,vim编辑/etc/mysql/my.cnf文件，将datadir修改为新的目录

4.  由于新的目录在/home目录下，因此还需要修改其他参数,
将/etc/systemd/system目录下的mysql.service和mysqld.service的ProtectHome参数都改为False