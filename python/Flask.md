## 注册过滤器
在Jinja2中注册自己的过滤器：       
```python
@app.template_filter('reverse')
def reverse_filter(s):
    return s[:: -1]

def reverse_filter(s):
    return s[:: -1]
app.jinja_env.filters['reverse'] = reverse_filter
```
使用如下：
```html
{% for x in mylist | reverse %}
{% enffor %}
```

## 上下文处理器
Flask 中的上下文处理器自动向模板的上下文中插入新变量。上下文处理器在模板渲染之前运行，并且可以在模板上下文中插入新值。上下文处理器是一个返回字典的函数。
```python
@app.context_processor
def inject_user():
    return dict(user=g.user)
```
也可以使函数在模板中可用：
```python
def utility_processor():
    def format_price(amount, currency=u'$'):
        return u'{0:.2f}{1}'.format(amount, currency)
    return dict(format_price=format_price)

#页面中如下使用
# {{ format_price(0.33) }}

#也可以定义成过滤器
@app.template_filter('format_price')
def format_price(dic):
    return u'{0:.2f}{1}'.format(dic['amount'], dic['currency'])

```

## 使用过滤器进行登录权限验证
```python
from functools import wraps
from flask import g, request, redirect, url_for

def login_required(f):
    @wraps(f)
    def decorated_function(*args, **kwargs):
        if g.user is None: #此处可以替换成其他的方式进行验证
            return redirect(url_for('login', next=request.url))
        return f(*args, **kwargs)
    return decorated_function

## 使用
@app.route('/secret_page')
@login_required
def secret_page():
    pass
```