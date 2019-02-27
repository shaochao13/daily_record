使用 `.navbar` 类来创建一个标准的导航栏，后面紧跟: `.navbar-expand-xl|lg|md|sm` 类来创建响应式的导航栏 (大屏幕水平铺开，小屏幕垂直堆叠)。

导航栏上的选项可以使用 `<ul>` 元素并添加 `class="navbar-nav"` 类。 然后在 `<li>` 元素上添加 `.nav-item` 类， `<a>` 元素上使用 `.nav-link` 类:
```html
<!-- 小屏幕上水平导航栏会切换为垂直的 -->
<nav class="navbar navbar-expand-sm bg-light">
 
  <!-- Links -->
  <ul class="navbar-nav">
    <li class="nav-item">
      <a class="nav-link" href="#">Link 1</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link 2</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link 3</a>
    </li>
  </ul>
 
</nav>
```

- 垂直导航栏

删除 `.navbar-expand-xl|lg|md|sm` 类来创建垂直导航栏:
```html
<!-- 垂直导航栏 -->
<nav class="navbar bg-light">
 
  <!-- Links -->
  <ul class="navbar-nav">
    <li class="nav-item">
      <a class="nav-link" href="#">Link 1</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link 2</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link 3</a>
    </li>
  </ul>
 
</nav>
```

- 不同颜色导航栏

可以使用以下类来创建不同颜色导航栏：`.bg-primary, .bg-success, .bg-info, .bg-warning, .bg-danger, .bg-secondary, .bg-dark` 和 `.bg-light`)。

```html
<!-- 灰底黑字 -->
<nav class="navbar navbar-expand-sm bg-light navbar-light"></nav>
 
<!-- 黑底白字 -->
<nav class="navbar navbar-expand-sm bg-dark navbar-dark">...</nav>
 
<!-- 蓝底白字 -->
<nav class="navbar navbar-expand-sm bg-primary navbar-dark">...</nav>
```

- 品牌/Logo

`.navbar-brand` 类用于高亮显示品牌/Logo:
```html
<nav class="navbar navbar-expand-sm bg-dark navbar-dark">
  <a class="navbar-brand" href="#">Logo</a>
  ...
</nav>
```

如果使用图片，可以使用 `.navbar-brand` 类来设置图片自适应导航栏。
```html
<nav class="navbar navbar-expand-sm bg-dark navbar-dark">
   <a class="navbar-brand" href="#">
    <img src="bird.jpg" alt="Logo" style="width:40px;">
  </a>
  ...
</nav>
```

- 折叠导航栏 ( **这个很有用！** )
  
通常，小屏幕上都会折叠导航栏，通过点击来显示导航选项。

要创建折叠导航栏，可以在按钮上添加 `class="navbar-toggler", data-toggle="collapse" 与 data-target="#thetarget"` 类。然后在设置了 `class="collapse navbar-collapse"` 类的 `div` 上包裹导航内容（链接）, `div` 元素上的 `id` 匹配按钮 `data-target` 的上指定的 `id`:

```html
<nav class="navbar navbar-expand-md bg-dark navbar-dark">
  <!-- Brand -->
  <a class="navbar-brand" href="#">Navbar</a>
 
  <!-- Toggler/collapsibe Button -->
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#collapsibleNavbar">
    <span class="navbar-toggler-icon"></span>
  </button>
 
  <!-- Navbar links -->
  <div class="collapse navbar-collapse" id="collapsibleNavbar">
    <ul class="navbar-nav">
      <li class="nav-item">
        <a class="nav-link" href="#">Link</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Link</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Link</a>
      </li> 
    </ul>
  </div> 
</nav>
```

- 导航栏使用下拉菜单

```html
<nav class="navbar navbar-expand-sm bg-dark navbar-dark">
  <!-- Brand -->
  <a class="navbar-brand" href="#">Logo</a>
 
  <!-- Links -->
  <ul class="navbar-nav">
    <li class="nav-item">
      <a class="nav-link" href="#">Link 1</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link 2</a>
    </li>
 
    <!-- Dropdown -->
    <li class="nav-item dropdown">
      <a class="nav-link dropdown-toggle" href="#" id="navbardrop" data-toggle="dropdown">
        Dropdown link
      </a>
      <div class="dropdown-menu">
        <a class="dropdown-item" href="#">Link 1</a>
        <a class="dropdown-item" href="#">Link 2</a>
        <a class="dropdown-item" href="#">Link 3</a>
      </div>
    </li>
  </ul>
</nav>
```

- 导航栏的表单与按钮

导航栏的表单 `<form>` 元素使用 `class="form-inline"` 类来排版输入框与按钮：
```html
<nav class="navbar navbar-expand-sm bg-dark navbar-dark">
  <form class="form-inline">
    <input class="form-control" type="text" placeholder="Search">
    <button class="btn btn-success" type="submit">Search</button>
  </form>
</nav>
```

- 导航栏文本

使用 `.navbar-text` 类来设置导航栏上非链接文本，可以保证水平对齐，颜色与内边距一样。
```html
<nav class="navbar navbar-expand-sm bg-dark navbar-dark">
<!-- Links -->
  <ul class="navbar-nav">
    <li class="nav-item">
      <a class="nav-link" href="#">Link 1</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link 2</a>
    </li>
  </ul>
  <!-- Navbar text-->
  <span class="navbar-text">
    Navbar text
  </span>
</nav>
```

- 固定导航栏

导航栏可以固定在头部或者底部。

使用 `.fixed-top` 类来实现导航栏的固定,`.fixed-bottom` 类用于设置导航栏固定在底部:
```html
<nav class="navbar navbar-expand-sm bg-dark navbar-dark fixed-top">
  ...
</nav> 

<nav class="navbar navbar-expand-sm bg-dark navbar-dark fixed-bottom">
  ...
</nav>
```











