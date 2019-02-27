创建一个简单的水平导航栏，可以在 `<ul>` 元素上添加 `.nav` 类，在每个 `<li>` 选项上添加 `.nav-item` 类，在每个链接上添加 `.nav-link` 类:
```html
<ul class="nav">
  <li class="nav-item">
    <a class="nav-link" href="#">Link</a>
  </li>
  <li class="nav-item">
    <a class="nav-link" href="#">Link</a>
  </li>
  <li class="nav-item">
    <a class="nav-link" href="#">Link</a>
  </li>
  <li class="nav-item">
    <a class="nav-link disabled" href="#">Disabled</a>
  </li>
</ul>
```

- 导航对齐方式

`.justify-content-center` 类设置导航居中显示， `.justify-content-end` 类设置导航右对齐。
```html
<!-- 导航居中 -->
<ul class="nav justify-content-center">
 
<!-- 导航右对齐 -->
<ul class="nav justify-content-end">
```

- 垂直导航

`.flex-column` 类用于创建垂直导航：
```html
<ul class="nav flex-column">
...
</ul>
```

- 选项卡

使用 `.nav-tabs` 类可以将导航转化为选项卡。然后对于选中的选项使用 `.active` 类来标记。

```html
<ul class="nav nav-tabs">
...
</ul>
```

- 胶囊导航

`.nav-pills` 类可以将导航项设置成胶囊形状。

```html
<ul class="nav nav-pills">
...
</ul>
```

- 导航等宽

`.nav-justified` 类可以设置导航项齐行等宽显示。

```html
<ul class="nav nav-pills nav-justified">..</ul>
<ul class="nav nav-tabs nav-justified">..</ul>
```
 

要设置选项卡是动态可切换的，可以在每个链接上添加 `data-toggle="tab"` 属性。 然后在每个选项对应的内容的上添加 `.tab-pane` 类。

希望有淡入效果可以在 `.tab-pane` 后添加 `.fade` 类:
```html
<!-- Nav tabs -->
<ul class="nav nav-tabs">
  <li class="nav-item">
    <a class="nav-link active" data-toggle="tab" href="#home">Home</a>
  </li>
  <li class="nav-item">
    <a class="nav-link" data-toggle="tab" href="#menu1">Menu 1</a>
  </li>
  <li class="nav-item">
    <a class="nav-link" data-toggle="tab" href="#menu2">Menu 2</a>
  </li>
</ul>
 
<!-- Tab panes -->
<div class="tab-content">
  <div class="tab-pane active container" id="home">...</div>
  <div class="tab-pane container" id="menu1">...</div>
  <div class="tab-pane container" id="menu2">...</div>
</div>
```


胶囊状动态选项卡只需要将代码中 `data-toggle` 属性设置为 `data-toggle="pill"`:
```html
<!-- Nav pills -->
<ul class="nav nav-pills">
  <li class="nav-item">
    <a class="nav-link active" data-toggle="pill" href="#home">Home</a>
  </li>
  <li class="nav-item">
    <a class="nav-link" data-toggle="pill" href="#menu1">Menu 1</a>
  </li>
  <li class="nav-item">
    <a class="nav-link" data-toggle="pill" href="#menu2">Menu 2</a>
  </li>
</ul>
 
<!-- Tab panes -->
<div class="tab-content">
  <div class="tab-pane active container" id="home">...</div>
  <div class="tab-pane container" id="menu1">...</div>
  <div class="tab-pane container" id="menu2">...</div>
</div>
```





