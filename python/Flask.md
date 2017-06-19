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