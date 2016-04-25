# 命令
1. 新建一个django project:  
> ```python
    django-admin.py startproject project-name 
    django-admin startproject project-name #windows环境下
    ```
2. 新建app:   
> ```python
    python manage.py startapp app-name
    ```
或 
```python
     django-admin.py startapp app-name
     ```     
3. 同步数据库:   
> 
```
python manage.py syncdb
```   
***Django 1.7.1 及以上的版本使用以下命令***：  
```python
python manage.py makemigrations
python manage.py migrate
```
4. 清空数据库:   
> ```python
#此命令会询问是 yes 还是 no, 选择 yes 会把数据全部清空掉，只留下空表。
python manage.py flush
```
5. 创建超级管理员
> ```python
#按照提示输入用户名和对应的密码就好了邮箱可以留空，用户名和密码必填
python manage.py createsuperuser
#修改 用户密码可以用：
python manage.py changepassword username
```
6. 导出数据 导入数据
> ```python
python manage.py dumpdate appname > appname.json
python manage.py loaddata appname.json
```
7. 数据库命令行
> ```python
#Django 会自动进入在settings.py中设置的数据库，如果是 MySQL 或 postgreSQL 会要求输入数据库用户密码。在这个终端可以执行数据库的SQL语句。
python manage.py dbshell
```
