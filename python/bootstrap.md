# 重要的全局样式和设置

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

## 容器类
Bootstrap 4 需要一个容器元素来包裹网站的内容。

可以使用以下两个容器类：
```
.container 类用于固定宽度并支持响应式布局的容器。

.container-fluid 类用于 100% 宽度，占据全部视口（viewport）的容器。
```

---

## Bootstrap4 网格系统
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

## Bootstrap4 文字排版
Bootstrap 4 默认的 font-size 为 `16px`, line-height 为 `1.5`。

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

## Bootstrap4 颜色

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

## Bootstrap4 表格

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

```html
<table class="table">
    <thead>
      <tr>
        <th>Firstname</th>
        <th>Lastname</th>
        <th>Email</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Default</td>
        <td>Defaultson</td>
        <td>def@somemail.com</td>
      </tr>      
      <tr class="table-primary">
        <td>Primary</td>
        <td>Joe</td>
        <td>joe@example.com</td>
      </tr>
      <tr class="table-success">
        <td>Success</td>
        <td>Doe</td>
        <td>john@example.com</td>
      </tr>
      <tr class="table-danger">
        <td>Danger</td>
        <td>Moe</td>
        <td>mary@example.com</td>
      </tr>
      <tr class="table-info">
        <td>Info</td>
        <td>Dooley</td>
        <td>july@example.com</td>
      </tr>
      <tr class="table-warning">
        <td>Warning</td>
        <td>Refs</td>
        <td>bo@example.com</td>
      </tr>
      <tr class="table-active">
        <td>Active</td>
        <td>Activeson</td>
        <td>act@example.com</td>
      </tr>
      <tr class="table-secondary">
        <td>Secondary</td>
        <td>Secondson</td>
        <td>sec@example.com</td>
      </tr>
      <tr class="table-light">
        <td>Light</td>
        <td>Angie</td>
        <td>angie@example.com</td>
      </tr>
      <tr class="table-dark text-dark">
        <td>Dark</td>
        <td>Bo</td>
        <td>bo@example.com</td>
      </tr>
    </tbody>
</table>
```
