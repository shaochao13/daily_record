1.  找到 [mysqld] 
```bash
innodb_file_per_table = 1
#如果没有设置”log_error“
log_error = ***/**/error.log
```


2. 在数据库中创建一张表名与被恢复表表名一致的表，表结构不限制
   
3. 复制被恢复的表的frm文件替换新创建的同名表的frm文件。

4. 执行
```sql   
flush tables
```

5. 查看error.log 文件。错误日志中会打印我们需要恢复的表的字段数。

6. 删除已经创建的新表，重新创建一个同名表， 使表的字段个数跟error 日志中一样多，字段名以及字段类型不限制。

7. 再次使用被恢复的frm文件替换新创建的同名表的frm文件。

8. 通过 show create table 语句拿到 表的 表结构。

9. 使用 拿到的表结构 创建新表。

10. 使用ibd文件恢复数据：
```sql
 alter table + 表名 + discard tablespace;
 # 如果[mysqld]配置文件中有innodb_force_recovery = 6 设置，将其去掉。
```

把ibd文件复制到mysql目录下的数据库中，并执行：
```sql
alter table + 表名 + import tablespace;
```

11. 恢复完成 。