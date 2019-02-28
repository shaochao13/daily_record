通过向元素添加 `data-toggle="tooltip"` 来来创建提示框

```html
<a href="#" data-toggle="tooltip" title="我是提示内容!">鼠标移动到我这</a>
```

```javascript
$(document).ready(function(){
    $('[data-toggle="tooltip"]').tooltip(); 
});
```


可以使用 `data-placement` 属性来设定提示框显示的方向: `top, bottom, left` 或 `right`:

```html
<a href="#" data-toggle="tooltip" data-placement="top" title="我是提示内容!">鼠标移动到我这</a>
<a href="#" data-toggle="tooltip" data-placement="bottom" title="我是提示内容!">鼠标移动到我这</a>
<a href="#" data-toggle="tooltip" data-placement="left" title="我是提示内容!">鼠标移动到我这</a>
<a href="#" data-toggle="tooltip" data-placement="right" title="我是提示内容!">鼠标移动到我这</a>
```