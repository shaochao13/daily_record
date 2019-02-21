[重要的全局样式和设置](#1)

[容器类](#2)

[Bootstrap4 网格系统](#3)

[Bootstrap4 文字排版](#4)

[Bootstrap4 颜色](#5)

[Bootstrap4 表格](#6)

[Bootstrap4 图像形状](#7)

[Bootstrap4 Jumbotron (超大屏幕)](#8)

[Bootstrap4 信息提示框](#9)

[Bootstrap4 按钮](#10)

[Bootstrap4 按钮组](#11)


## <span id="1">重要的全局样式和设置</span>

- Bootstrap 要求设置 HTML5 doctype

```html
<!doctype html>
<html lang="en">
  ...
</html>
```

- 响应式 meta 标签 , 移动设备优先

为了确保在所有设备上能够正确渲染并支持触控缩放，务必将设置 viewport 属性的 meta 标签添加到 <head> 中。
```html
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
```

- 盒模型

为了在 CSS 中更直观的设置尺寸，我们将全局的 box-sizing 值从 content-box 修改为 border-box。这就确保了 padding 不会影响元素最终的宽度计算，但是这可能会导致第三方组件出现问题，例如 Google 地图和 Google 定制搜索。

在极少的情况下你需要重置 box-sizing 的值，

```css
.selector-for-some-widget {
  box-sizing: content-box;
}
```
通过以上代码片段，嵌套元素（包括通过 ::before and ::after 生成的内容）都将继承 .selector-for-some-widget 指定的 box-sizing 值。

---

## <span id="2">容器类</span>

Bootstrap 4 需要一个容器元素来包裹网站的内容。

可以使用以下两个容器类：
```
.container 类用于固定宽度并支持响应式布局的容器。

.container-fluid 类用于 100% 宽度，占据全部视口（viewport）的容器。
```

---

## <span id="3">Bootstrap4 网格系统</span>

Bootstrap 提供了一套响应式、移动设备优先的流式网格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多 <span style="color:red;">12</span> 列。    
Bootstrap 4 的网格系统是响应式的，列会根据屏幕大小自动重新排列。

### 网格类

Bootstrap 4 网格系统有以下 5 个类:

- .col- 针对所有设备
- .col-sm- 平板 - 屏幕宽度等于或大于 576px
- .col-md- 桌面显示器 - 屏幕宽度等于或大于 768px)
- .col-lg- 大桌面显示器 - 屏幕宽度等于或大于 992px)
- .col-xl- 超大桌面显示器 - 屏幕宽度等于或大于 1200px)

### 网格系统规则

- 网格每一行需要放在设置了 .container (固定宽度) 或 .container-fluid (全屏宽度) 类的容器中，这样就可以自动设置一些外边距与内边距。
- 使用行来创建水平的列组。
- 内容需要放置在列中，并且只有列可以是行的直接子节点。
- 预定义的类如 .row 和 .col-sm-4 可用于快速制作网格布局。
- 列通过填充创建列内容之间的间隙。 这个间隙是通过 .rows 类上的负边距设置第一行和最后一列的偏移。
- 网格列是通过跨越指定的 12 个列来创建。 例如，设置三个相等的列，需要使用用三个.col-sm-4 来设置。
- Bootstrap 3 和 Bootstrap 4 最大的区别在于 Bootstrap 4 现在使用 flexbox（弹性盒子） 而不是浮动。 Flexbox 的一大优势是，没有指定宽度的网格列将自动设置为等宽与等高列 。

### 偏移列

偏移列通过 offset-`*`-`*` 类来设置。第一个星号( * )可以是 sm、md、lg、xl，表示屏幕设备类型，第二个星号( * )可以是 1 到 11 的数字。

为了在大屏幕显示器上使用偏移，请使用 `.offset-md-*` 类。
```
例如：.offset-md-4 是把.col-md-4 往右移了四列格。
```

---

## <span id="4">Bootstrap4 文字排版</span>

Bootstrap 4 默认的 `font-size` 为 `16px`, `line-height` 为 `1.5`。

默认的 font-family 为 "Helvetica Neue", Helvetica, Arial, sans-serif。

此外，所有的 <p> 元素 margin-top: 0 、 margin-bottom: 1rem (16px)。

- Display 标题类

Bootstrap 提供了四个 Display 类来控制标题的样式: `.display-1, .display-2, .display-3, .display-4`。
Display 标题可以输出比`(h1-h6)`更大更粗的字体样式。

- &lt;small&gt;

在 Bootstrap 4 中 HTML &lt;small&gt; 元素用于创建字号更小的颜色更浅的文本:
```html
<div class="container">
  <h1>更小文本标题</h1>
  <p>small 元素用于字号更小的颜色更浅的文本:</p>       
  <h1>h1 标题 <small>副标题</small></h1>
  <h2>h2 标题 <small>副标题</small></h2>
  <h3>h3 标题 <small>副标题</small></h3>
  <h4>h4 标题 <small>副标题</small></h4>
  <h5>h5 标题 <small>副标题</small></h5>
  <h6>h6 标题 <small>副标题</small></h6>
</div>
```

- &lt;mark&gt;

Bootstrap 4 定义 &lt;mark&gt; 为`黄色背景`及有一定的内边:
```html
<div class="container">
  <h1>高亮文本</h1>    
  <p>使用 mark 元素来 <mark>高亮</mark> 文本。</p>
</div>
```

- &lt;abbr&gt;

Bootstrap 4 定义 HTML <abbr> 元素的样式为显示在文本`底部`的一条`虚线边框`

- &lt;blockquote&gt;  --块引用

对于引用的内容可以在 `<blockquote>` 上添加 `.blockquote` 类 :
```html
<div class="container">
  <h1>Blockquotes</h1>
  <p>The blockquote element is used to present content from another source:</p>
  <blockquote class="blockquote">
    <p>For 50 years, WWF has been protecting the future of nature. The world's leading conservation organization, WWF works in 100 countries and is supported by 1.2 million members in the United States and close to 5 million globally.</p>
    <footer class="blockquote-footer">From WWF's website</footer>
  </blockquote>
</div>
```

- 更多排版类

|类名|描述|
|--:|:--|
| `.font-weight-bold` | 加粗文本 |
| `.font-weight-normal` | 普通文本 | 
| `.font-weight-light` | 更细的文本 
| `.font-italic` | 斜体文本 |
| `.lead` | 让段落更突出 |
| `.small` | 指定更小文本 (为父元素的 85% ) |
| `.text-left` | 左对齐 |
| `.text-center` | 居中 | 
| `.text-right` | 右对齐 | 
| `.text-justify` | 设定文本对齐,段落中超出屏幕部分文字自动换行 |
| `.text-nowrap` | 段落中超出屏幕部分不换行 | 
| `.text-lowercase` | 设定文本小写 | 
| `.text-uppercase` | 设定文本大写 | 
| `.text-capitalize` | 设定单词首字母大写 |
| `.initialism` | `显示在 <abbr> 元素中的文本以小号字体展示，且可以将小写字母转换为大写字母` | 
| `.list-unstyled` | `移除默认的列表样式，列表项中左对齐 ( <ul> 和 <ol> 中)。 这个类仅适用于直接子列表项 (如果需要移除嵌套的列表项，你需要在嵌套的列表中使用该样式)` | 
| `.list-inline` | 将所有列表项放置同一行 |
| `.pre-scrollable` | `使 <pre> 元素可滚动，代码块区域最大高度为340px,一旦超出这个高度,就会在Y轴出现滚动条` |

---

## <span id="5">Bootstrap4 颜色</span>

Bootstrap 4 提供了一些有代表意义的颜色类：`.text-muted, .text-primary, .text-success, .text-info, .text-warning, .text-danger, .text-secondary, .text-white, .text-dark and .text-light`
```html
<div class="container">
  <h2>代表指定意义的文本颜色</h2>
  <p class="text-muted">柔和的文本。</p>
  <p class="text-primary">重要的文本。</p>
  <p class="text-success">执行成功的文本。</p>
  <p class="text-info">代表一些提示信息的文本。</p>
  <p class="text-warning">警告文本。</p>
  <p class="text-danger">危险操作文本。</p>
  <p class="text-secondary">副标题。</p>
  <p class="text-dark">深灰色文字。</p>
  <p class="text-light">浅灰色文本（白色背景上看不清楚）。</p>
  <p class="text-white">白色文本（白色背景上看不清楚）。</p>
</div>
```

在链接中使用
```html
<div class="container">
  <h2>文本颜色</h2>
  <p>鼠标移动到链接。</p>
  <a href="#" class="text-muted">柔和的链接。</a>
  <a href="#" class="text-primary">主要链接。</a>
  <a href="#" class="text-success">成功链接。</a>
  <a href="#" class="text-info">信息文本链接。</a>
  <a href="#" class="text-warning">警告链接。</a>
  <a href="#" class="text-danger">危险链接。</a>
  <a href="#" class="text-secondary">副标题链接。</a>
  <a href="#" class="text-dark">深灰色链接。</a>
  <a href="#" class="text-light">浅灰色链接。</a>
</div>
```

- 背景颜色

提供背景颜色的类有: `.bg-primary, .bg-success, .bg-info, .bg-warning, .bg-danger, .bg-secondary, .bg-dark 和 .bg-light`。注意背景颜色不会设置文本的颜色，在一些实例中你需要与 `.text-*` 类一起使用。
```html
<div class="container">
  <h2>背景颜色</h2>
  <p class="bg-primary text-white">重要的背景颜色。</p>
  <p class="bg-success text-white">执行成功背景颜色。</p>
  <p class="bg-info text-white">信息提示背景颜色。</p>
  <p class="bg-warning text-white">警告背景颜色</p>
  <p class="bg-danger text-white">危险背景颜色。</p>
  <p class="bg-secondary text-white">副标题背景颜色。</p>
  <p class="bg-dark text-white">深灰背景颜色。</p>
  <p class="bg-light text-dark">浅灰背景颜色。</p>
</div>
```

---

## <span id="6">Bootstrap4 表格</span>

- 条纹表格 `.table-striped`

通过添加 `.table-striped` 类，您将在 `<tbody>` 内的行上看到条纹，如下面的实例所示：
```html
<table class="table table-striped">
...
</table>
```

- 带边框表格 `.table-bordered`

`.table-bordered` 类可以为表格添加边框
```html
<table class="table table-bordered">
...
</table>
```

- 鼠标悬停状态表格 `.table-hover`

`.table-hover` 类可以为表格的每一行添加鼠标悬停效果（灰色背景）
```html
<table class="table table-hover">
...
</table>
```

- 黑色背景表格 `.table-dark`

`.table-dark` 类可以为表格添加黑色背景：
```html
<table class="table table-dark">
...
</table>
```

以上几种样式是可以组合使用的。


- 表格颜色类的说明

|类名|描述|
|--:|:--|
|.table-primary	|蓝色: 指定这是一个重要的操作|
|.table-success|	绿色: 指定这是一个允许执行的操作|
|.table-danger	|红色: 指定这是可以危险的操作|
|.table-info	|浅蓝色: 表示内容已变更|
|.table-warning|	橘色: 表示需要注意的操作|
|.table-active|	灰色: 用于鼠标悬停效果|
|.table-secondary|	灰色: 表示内容不怎么重要|
|.table-light	|浅灰色，可以是表格行的背景|
|.table-dark|	深灰色，可以是表格行的背景|
|||

```html
<table class="table">
    <thead>
    </thead>
    <tbody>
      <tr class="table-primary">
      ...
      </tr>
      <tr class="table-success">
      </tr>
      <tr class="table-danger">
      </tr>
      <tr class="table-info">
      </tr>
      <tr class="table-warning">
      </tr>
      <tr class="table-active">
      </tr>
      <tr class="table-secondary">
      </tr>
      <tr class="table-light">
      </tr>
      <tr class="table-dark text-dark">
      </tr>
    </tbody>
</table>
```

- 较小的表格 `.table-sm`

`.table-sm` 类用于通过减少内边距来设置较小的表格
```html
<table class="table table-bordered table-sm">
...
</table>
```
- 表头颜色

`.thead-dark` 类用于给表头添加黑色背景， `.thead-light` 类用于给表头添加灰色背景
```html
<table class="table">
  <thead class="thead-dark">
  </thead>
</table>

<table class="table">
  <thead class="thead-light">
  </thead>
</table>
```

- 响应式表格

`.table-responsive` 类用于创建响应式表格：在屏幕宽度小于 992px 时会创建水平滚动条，如果可视区域宽度大于 `992px` 则显示不同效果（没有滚动条）
```html
<div class="table-responsive">
  <table class="table">
  ...
  </table>
</div>
```

|类名|屏幕宽度|
|-:|:-|
.table-responsive-sm |	< 576px
.table-responsive-md |	< 768px
.table-responsive-lg |	< 992px
.table-responsive-xl |	< 1200px
|||

---

## <span id="7">Bootstrap4 图像形状</span>

- 圆角图片

`.rounded` 类可以让图片显示圆角效果
```html
<img src="cinqueterre.jpg" class="rounded" alt="Cinque Terre">
```

- 椭圆图片

`.rounded-circle` 类可以设置椭圆形图片
```html
<img src="cinqueterre.jpg" class="rounded-circle" alt="Cinque Terre">
```

- 缩略图

`.img-thumbnail` 类用于设置图片缩略图(图片有边框)
```html
<img src="cinqueterre.jpg" class="img-thumbnail" alt="Cinque Terre">
```

- 图片对齐方式

使用 `.float-right` 类来设置图片右对齐，使用 `.float-left` 类设置图片左对齐:
```html
<img src="paris.jpg" class="float-left"> 
<img src="cinqueterre.jpg" class="float-right">
```

- 响应式图片

通过在 `<img>` 标签中添加 `.img-fluid` 类来设置响应式图片.
`.img-fluid` 类设置了 `max-width: 100%; 、 height: auto;` 
```html
<img class="img-fluid" src="img_chania.jpg" alt="Chania">
```

---

## <span id="8">Bootstrap4 Jumbotron (超大屏幕)</span>

通过在 `<div>` 元素 中添加 `.jumbotron` 类来创建 jumbotron
```html
<div class="jumbotron">
  <h1>菜鸟教程</h1> 
  <p>学的不仅是技术，更是梦想！！！</p> 
</div>
```

- 全屏幕的 Jumbotron

创建一个没有圆角的全屏幕，可以在 `.jumbotron-fluid` 类里头的 `div` 添加 `.container 或 .container-fluid` 类来实现
```html
<div class="jumbotron jumbotron-fluid">
  <div class="container">
      <h1>菜鸟教程</h1> 
      <p>学的不仅是技术，更是梦想！！！</p>
  </div>
</div>
```

---

## <span id="9">Bootstrap4 信息提示框</span>

提示框可以使用 `.alert` 类, 后面加上 `.alert-success, .alert-info, .alert-warning, .alert-danger, .alert-primary, .alert-secondary, .alert-light 或 .alert-dark` 类来实现
```html
<div class="alert alert-success">
  <strong>成功!</strong> 指定操作成功提示信息。
</div>
```

- 提示框添加链接

提示框中在链接的标签上添加 `alert-link` 类来设置匹配提示框颜色的链接
```html
<div class="alert alert-success">
  <strong>成功!</strong> 你应该认真阅读 <a href="#" class="alert-link">这条信息</a>。
</div>
```

- 关闭提示框

在提示框中的 div 中添加 `.alert-dismissible` 类，然后在关闭按钮的链接上添加 `class="close"` 和 `data-dismiss="alert"` 类来设置提示框的关闭操作。
```html
<div class="alert alert-success alert-dismissible">
  <button type="button" class="close" data-dismiss="alert">&times;</button>
  <strong>成功!</strong> 指定操作成功提示信息。
</div>
```

- 提示框动画

`.fade` 和 `.show` 类用于设置提示框在关闭时的淡出和淡入效果
```html
<div class="alert alert-danger alert-dismissible fade show">
```

---

## <span id="10">Bootstrap4 按钮</span>

```html
<button type="button" class="btn">基本按钮</button>
<button type="button" class="btn btn-primary">主要按钮</button>
<button type="button" class="btn btn-secondary">次要按钮</button>
<button type="button" class="btn btn-success">成功</button>
<button type="button" class="btn btn-info">信息</button>
<button type="button" class="btn btn-warning">警告</button>
<button type="button" class="btn btn-danger">危险</button>
<button type="button" class="btn btn-dark">黑色</button>
<button type="button" class="btn btn-light">浅色</button>
<button type="button" class="btn btn-link">链接</button>
```

按钮类可用于 `<a>`, `<button>`, 或 `<input>` 元素上.

```html
<a href="#" class="btn btn-info" role="button">链接按钮</a>
<button type="button" class="btn btn-info">按钮</button>
<input type="button" class="btn btn-info" value="输入框按钮">
<input type="submit" class="btn btn-info" value="提交按钮">
```

- 按钮设置边框
```html
<button type="button" class="btn btn-outline-primary">主要按钮</button>
<button type="button" class="btn btn-outline-secondary">次要按钮</button>
<button type="button" class="btn btn-outline-success">成功</button>
<button type="button" class="btn btn-outline-info">信息</button>
<button type="button" class="btn btn-outline-warning">警告</button>
<button type="button" class="btn btn-outline-danger">危险</button>
<button type="button" class="btn btn-outline-dark">黑色</button>
<button type="button" class="btn btn-outline-light text-dark">浅色</button>
```

- 不同大小的按钮

```html
<button type="button" class="btn btn-primary btn-lg">大号按钮</button>
<button type="button" class="btn btn-primary">默认按钮</button>
<button type="button" class="btn btn-primary btn-sm">小号按钮</button>
```

- 块级按钮

通过添加 `.btn-block` 类可以设置块级按钮：
```html
<button type="button" class="btn btn-primary btn-block">按钮 1</button>
```

- 激活和禁用的按钮

按钮可设置为激活或者禁止点击的状态。

`.active` 类可以设置按钮是可用的， `disabled` 属性可以设置按钮是不可点击的。 注意 `<a>` 元素不支持 `disabled` 属性，你可以通过添加 `.disabled` 类来禁止链接的点击。
```html
<button type="button" class="btn btn-primary active">点击后的按钮</button>
<button type="button" class="btn btn-primary" disabled>禁止点击的按钮</button>
<a href="#" class="btn btn-primary disabled">禁止点击的链接</a>
```

## <span id="11">Bootstrap4 按钮组</span>

可以在 `<div>` 元素上添加 `.btn-group` 类来创建按钮组

```html
<div class="btn-group">
  <button type="button" class="btn btn-primary">Apple</button>
  <button type="button" class="btn btn-primary">Samsung</button>
  <button type="button" class="btn btn-primary">Sony</button>
</div>
```

可以使用 `.btn-group-lg|sm` 类来设置按钮组的大小
```html
<div class="btn-group btn-group-lg">
  <button type="button" class="btn btn-primary">Apple</button>
  <button type="button" class="btn btn-primary">Samsung</button>
  <button type="button" class="btn btn-primary">Sony</button>
</div>
```

- 垂直按钮组

使用 `.btn-group-vertical` 类来创建垂直的按钮组
```html
<div class="btn-group-vertical">
  <button type="button" class="btn btn-primary">Apple</button>
  <button type="button" class="btn btn-primary">Samsung</button>
  <button type="button" class="btn btn-primary">Sony</button>
</div>
```

- 内嵌按钮组及下拉菜单
```html
<div class="btn-group">
  <button type="button" class="btn btn-primary">Apple</button>
  <button type="button" class="btn btn-primary">Samsung</button>
  <div class="btn-group">
    <button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">
       Sony
    </button>
    <div class="dropdown-menu">
      <a class="dropdown-item" href="#">Tablet</a>
      <a class="dropdown-item" href="#">Smartphone</a>
    </div>
  </div>
</div>
```

- 拆分按钮下拉菜单

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

- 垂直按钮组及下拉菜单
```html
<div class="btn-group-vertical">
  <button type="button" class="btn btn-primary">Apple</button>
  <button type="button" class="btn btn-primary">Samsung</button>
  <div class="btn-group">
    <button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">
       Sony
    </button>
    <div class="dropdown-menu">
      <a class="dropdown-item" href="#">Tablet</a>
      <a class="dropdown-item" href="#">Smartphone</a>
    </div>
  </div>
</div>
```