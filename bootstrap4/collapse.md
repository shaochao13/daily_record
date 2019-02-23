`.collapse` 类用于指定一个折叠元素 (实例中的 `<div>`); 点击按钮后会在隐藏与显示之间切换。

控制内容的隐藏与显示，需要在 `<a>` 或 `<button>` 元素上添加 `data-toggle="collapse"` 属性。 `data-target="#id"` 属性是对应折叠的内容 (`<div id="demo">`)。

注意: `<a>` 元素上你可以使用 `href` 属性来代替 `data-target` 属性
```html
<button data-toggle="collapse" data-target="#demo">折叠</button>
<div id="demo" class="collapse">
...
</div>
```

```html
<a href="#demo" data-toggle="collapse">Collapsible</a>
<div id="demo" class="collapse">
...
</div>
```

默认情况下折叠的内容是隐藏的，你可以添加 `.show` 类让内容默认显示
```html
<div id="demo" class="collapse show">
Lorem ipsum dolor text....
</div>
```

- 手风琴实例

使用 `data-parent` 属性来确保所有的折叠元素在指定的父元素下，这样就能实现在一个折叠选项显示时其他选项就隐藏

```html
<div id="accordion">
    <div class="card">
      <div class="card-header">
        <a class="card-link" data-toggle="collapse" href="#collapseOne">
          选项一
        </a>
      </div>
      <div id="collapseOne" class="collapse show" data-parent="#accordion">
        <div class="card-body">
          #1 内容：菜鸟教程 -- 学的不仅是技术，更是梦想！！！
        </div>
      </div>
    </div>
    <div class="card">
      <div class="card-header">
        <a class="collapsed card-link" data-toggle="collapse" href="#collapseTwo">
        选项二
      </a>
      </div>
      <div id="collapseTwo" class="collapse" data-parent="#accordion">
        <div class="card-body">
          #2 内容：菜鸟教程 -- 学的不仅是技术，更是梦想！！！
        </div>
      </div>
    </div>
    <div class="card">
      <div class="card-header">
        <a class="collapsed card-link" data-toggle="collapse" href="#collapseThree">
          选项三
        </a>
      </div>
      <div id="collapseThree" class="collapse" data-parent="#accordion">
        <div class="card-body">
          #3 内容：菜鸟教程 -- 学的不仅是技术，更是梦想！！！
        </div>
      </div>
    </div>
  </div>
```


