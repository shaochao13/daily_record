[重要的全局样式和设置](#1)

[容器类](#2)

[网格系统](#3)

[文字排版](./text_typesetting)

[颜色](./color.md)

[表格](./table.md)

[图像形状](./img.md)

[Jumbotron (超大屏幕)](./jumbotron.md)

[信息提示框](./alert.md)

[按钮](./botton.md)

[徽章(Badges)](./badge.md)

[进度条](./progress.md)

[分页](./pagination.md)

[列表组](./list_group.md)

[卡片](./card.md)

[下拉列表](./dropdown.md)

[折叠](./collapse.md)

[导航](./nav.md)

[导航栏](./navbar.md)

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

