`.dropdown` 类用来指定一个下拉菜单。

可以使用一个按钮或链接来打开下拉菜单， 按钮或链接需要添加 `.dropdown-toggle` 和 `data-toggle="dropdown"` 属性。
`<div>` 元素上添加 `.dropdown-menu` 类来设置实际下拉菜单，然后在下拉菜单的选项中添加 `.dropdown-item` 类
```html
<div class="dropdown">
  <button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">
    Dropdown button
  </button>
  <div class="dropdown-menu">
    <a class="dropdown-item" href="#">Link 1</a>
    <a class="dropdown-item" href="#">Link 2</a>
    <a class="dropdown-item" href="#">Link 3</a>
  </div>
</div>
```

- 下拉菜单中的分割线
`.dropdown-divider` 类用于在下拉菜单中创建一个水平的分割线
```html
<div class="dropdown">
    <button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">
      Dropdown button
    </button>
    <div class="dropdown-menu">
      <a class="dropdown-item" href="#">Link 1</a>
      <a class="dropdown-item" href="#">Link 2</a>
      <a class="dropdown-item" href="#">Link 3</a>
      <div class="dropdown-divider"></div>
      <a class="dropdown-item" href="#">Another link</a>
    </div>
  </div>
```

- 下拉菜单中的标题

`.dropdown-header` 类用于在下拉菜单中添加标题
```html
<div class="dropdown">
    <button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">
      Dropdown button
    </button>
    <div class="dropdown-menu">
      <h5 class="dropdown-header">Dropdown header</h5>
      <a class="dropdown-item" href="#">Link 1</a>
      <a class="dropdown-item" href="#">Link 2</a>
      <a class="dropdown-item" href="#">Link 3</a>
      <h5 class="dropdown-header">Dropdown header</h5>
      <a class="dropdown-item" href="#">Another link</a>
    </div>
  </div>
```

- 下拉菜单中的可用项与禁用项

`.active` 类会让下拉菜单的选项高亮显示 (添加蓝色背景)。

如果要禁用下拉菜单的选项，可以使用`.disabled` 类
```html
<a class="dropdown-item active" href="#">Active</a>
<a class="dropdown-item disabled" href="#">Disabled</a>
```

- 下拉菜单的定位

`.dropdown-menu-right` 右对齐，`.dropdown-menu-left` 左对齐。

```html
<div class="dropdown-menu dropdown-menu-right">
<div class="dropdown-menu dropdown-menu-left">
```

- 指定向上弹出的下拉菜单

下拉菜单向上弹出，可以将 `<div>` 元素的 `class="dropdown"` 替换为 `"dropup"`
```html
<div class="dropup">
    <button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">
      Dropdown button
    </button>
    <div class="dropdown-menu">
      <a class="dropdown-item" href="#">Link 1</a>
      <a class="dropdown-item" href="#">Link 2</a>
    </div>
</div>
```

- 按钮中设置下拉菜单
```html
<div class="btn-group">
  <button type="button" class="btn btn-primary">Sony</button>
  <button type="button" class="btn btn-primary dropdown-toggle dropdown-toggle-split" data-toggle="dropdown">
    <span class="caret"></span>
  </button>
  <div class="dropdown-menu">
    <a class="dropdown-item" href="#">Tablet</a>
    <a class="dropdown-item" href="#">Smartphone</a>
  </div>
</div>
```