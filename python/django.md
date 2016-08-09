# 命令
1. 新建一个django project:  
 ```python
    django-admin.py startproject project-name 
    django-admin startproject project-name #windows环境下
```
2. 新建app:       
 ```python
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
```python
#此命令会询问是 yes 还是 no, 选择 yes 会把数据全部清空掉，只留下空表。
python manage.py flush
```
5. 创建超级管理员
 ```python
#按照提示输入用户名和对应的密码就好了邮箱可以留空，用户名和密码必填
python manage.py createsuperuser
#修改 用户密码可以用：
python manage.py changepassword username
```
6. 导出数据 导入数据
```python
python manage.py dumpdate appname > appname.json
python manage.py loaddata appname.json
```
7. 数据库命令行
```python
#Django 会自动进入在settings.py中设置的数据库，如果是 MySQL 或 postgreSQL 会要求输入数据库用户密码。在这个终端可以执行数据库的SQL语句。
python manage.py dbshell
```


- 模板中的for 循环        

变量                     |   描述
:---:                   |   :---:
forloop.counter         |   索引从 1 开始算
forloop.counter0        |   索引从 0 开始算
forloop.revcounter	    |   索引从最大长度到 1
forloop.revcounter0     |   索引从最大长度到 0
forloop.first           |   当遍历的元素为第一项时为真
forloop.last            |   当遍历的元素为最后一项时为真
forloop.parentloop      |   用在嵌套的 for 循环中，获取上一层 for 循环的 forloop
                        |
- 当列表中可能为空值时用 for  empty
```python
<ul>
{% for athlete in athlete_list %}
    <li>{{ athlete.name }}</li>
{% empty %}
    <li>抱歉，列表为空</li>
{% endfor %}
</ul>
```
                        
- 逻辑操作      
*** ==, !=, >=, <=, >, < *** 这些比较都可以在模板中使用，比如：  
```python
{% if var >= 90 %}
成绩优秀，自强学堂你没少去吧！学得不错
{% elif var >= 80 %}
成绩良好
{% elif var >= 70 %}
成绩一般
{% elif var >= 60 %}
需要努力
{% else %}
不及格啊，大哥！多去自强学堂学习啊！
{% endif %}
```
***and, or, not, in, not in ***也可以在模板中使用:   
```python
{% if num <= 100 and num >= 0 %}
num在0到100之间
{% else %}
数值不在范围之内！
{% endif %}
```
```python
{% if 'ziqiangxuetang' in List %}
自强学堂在名单中
{% endif %}
```
- 模板中 获取当前网址，当前用户等： 
Django 1.8 及以后 修改 settings.py :
```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                ...
                'django.template.context_processors.request',
                ...
            ],
        },
    },
]
```
获取当前用户：
```python
{{ request.user }}
```
如果登陆就显示内容，不登陆就不显示内容：
```python
{% if request.user.is_authenticated %}
    {{ request.user.username }}，您好！
{% else %}
    请登陆，这里放登陆链接
{% endif %}
```
获取当前网址：
```python
{{ request.path }}
```
获取当前 GET 参数：
```python
{{ request.GET.urlencode }}
```

# 数据导入方法
- 批量导入

```python
#coding:utf-8

import os
os.environ.setdefault("DJANGO_SETTINGS_MODULE","mysite_2.settings")

import django
if django.VERSION >= (1,7):
    django.setup()

def main():
    from blog.models import Blog
    f = open('oldblog.txt')
    for line in f:
        title, content = line.split("****")
        # Blog.objects.create(title = title, content=content)
        #可以避免重复导入数据
        Blog.objects.get_or_create(title=title,content=content)

    f.close()

if __name__ == '__main__':
    main()
    print "Done!"
```
- 用fixture导入      
最常见的fixture文件就是用python manage.py dumpdata 导出的文件,示例如下:   
```json
[
  {
    "model": "myapp.person",
    "pk": 1,
    "fields": {
      "first_name": "John",
      "last_name": "Lennon"
    }
  },
  {
    "model": "myapp.person",
    "pk": 2,
    "fields": {
      "first_name": "Paul",
      "last_name": "McCartney"
    }
  }]
```
可以根据自己的models,创建这样的json文件,然后用 python manage.py loaddata fixture.json 导入。

- Model.objects.bulk_create() 更快    

```python
#!/usr/bin/env python
import os
os.environ.setdefault("DJANGO_SETTINGS_MODULE", "mysite.settings")
 
def main():
    from blog.models import Blog
    f = open('oldblog.txt')
    BlogList = []
    for line in f:
        title,content = line.split('****')
        blog = Blog(title=title,content=content)
        BlogList.append(blog)
    # 以上四行 也可以用 列表解析 写成下面这样
    # BlogList = [Blog(title=line.split('****')[0], content=line.split('****')[1]) for line in f]
    f.close()
     
    Blog.objects.bulk_create(BlogList)
 
if __name__ == "__main__":
    main()
    print('Done!')
```

