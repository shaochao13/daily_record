通过向元素添加 `data-toggle="popover"` 来来创建弹出框。

`title` 属性的内容为弹出框的标题，`data-content` 属性显示了弹出框的文本内容:
```html
<a href="#" data-toggle="popover" title="弹出框标题" data-content="弹出框内容">多次点我</a>

$(document).ready(function(){
    $('[data-toggle="popover"]').popover(); 
});

```

```html
<a href="#" title="Header" data-toggle="popover" data-placement="top" data-content="Content">点我</a>
<a href="#" title="Header" data-toggle="popover" data-placement="bottom" data-content="Content">点我</a>
<a href="#" title="Header" data-toggle="popover" data-placement="left" data-content="Content">点我</a>
<a href="#" title="Header" data-toggle="popover" data-placement="right" data-content="Content">点我</a>
```

默认情况下，弹出框在再次点击指定元素后就会关闭，你可以使用 `data-trigger="focus"` 属性来设置在鼠标点击元素外部区域来关闭弹出框：
```html
<a href="#" title="取消弹出框" data-toggle="popover" data-trigger="focus" data-content="点击文档的其他地方关闭我">点我</a>
```

如果想实现在鼠标移动到元素上显示，移除后消失的效果，可以使用 `data-trigger` 属性，并设置值为 `"hover"`:
```html
<a href="#" title="Header" data-toggle="popover" data-trigger="hover" data-content="一些内容">鼠标移动到我这</a>
```