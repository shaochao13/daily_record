## CSS 书写顺序

![[css_order.png]]

## CSS中常用的对齐操作方式

1. margin 居中对齐

   主要用在div、p、h（大盒子）水平居中，直接给当前元素本身设置。

   ```css
   /*
   第1种方式 
   一般针对有固定宽度的盒子，如果大盒子没有设置宽度，会默认占满父元素的宽度。
   */
   margin: 0px auto;
   /* 第2种方式 */
   margin-left:auto;
   margin-right:auto;
   ```

2. text-align 居中对齐

   ```css
   text-align: center;
   /*
   1. 主要针对 文本、span、a、input、img标签
   2. 需要设置在元素的父元素上
   */
   ```

   

3. position 左右对齐

   ```css
   /* position使用绝对位置，然后设置right或者left的距离 */
   position: absolute;
   right: 0px;
   
   position: absolute;
   left: 0px;
   ```

   

4. Float 左右对齐 

   ```css
   float: right;
   float: left;
   ```

   



## 层叠

**css规则的顺序**：当应用两条同级别的规则到一个元素的时候，写在后面的就是实际使用的规则。

有三个因素需要考虑，根据重要性排序如下，前面的更重要：

1. **重要程度** 
2. **优先级** 
3. **资源顺序**

## 优先级

**继承 < 通配符选择器 < 标签选择器 < 类选择器 < id选择器 < 行内样式 < !important**

一个选择器的优先级可以说是由四个部分相加 (分量)，可以认为是个十百千 — 四位数的四个位数：

1. **千位**： 如果声明在 `style` 的属性**（内联样式）**则该位得一分。这样的声明没有选择器，所以它得分总是1000。

2. **百位**： 选择器中包含**ID选择器**则该位得一分。

3. **十位**： 选择器中包含**类选择器**、**属性选择器**或者**伪类**则该位得一分。

4. **个位**：选择器中包含**元素、伪元素选择器**则该位得一分。

   <u>注意：通用选择器 (`*`)，组合符 (`+`, `>`, `~`, ' ')，和否定伪类 (`:not`) 不会影响优先级。</u>
 
![[选择器权重计算公式.png]]

**如果不能直接选中某个元素，通过继承性影响的话，那么权重是0**:
```css
#hezi1 #hezi2 #hezi3 {
	color: red;
}  

div.box div.box div.box {
	color: blue;
}

p {
	color: green;
}
```
因为前面两个选择器都没有直接选中p，所以权重为0
```html
<div class="box" id="hezi1">
	<div class="box" id="hezi2">
		<div class="box" id="hezi3">
			<p>猜我是什么颜色</p>
		</div>
	</div>
</div>
```
**如果大家的权重相同，那么就采用就近原则：谁描述的近，听谁的**：
```css
#box1 {
	color: red;
}
#box2 {
	color: green;
}
#box3 {
	color: blue;
}
```
#box3 最近，所以听它的。
```html
<div id="box1">
	<div id="box2">
		<div id="box3">
			<p>猜我是什么颜色</p>
		</div>
	</div>
</div>
```


比较规则：

	- 先比较第一级的数字，如果比较出来了，之后的统统不看
	- 如果第一级的数字相同，再比较第二级数字，如果比较出来了，之后的统统不看
	- 依此类推
	- 如果!important 不是继承的，则权重最高。

`!important`标记(优先级最高)：
**（1）!important提升的是一个属性，而不是一个选择器**
**（2）!important无法提升继承的权重，该是0还是0**
**（3）!important不影响就近原则**


## 继承

### 控制继承

1. `inherit`   --- 使子元素属性和父元素相同。即 “开启继承”
2. `initial`  --- 设置属性值和浏览器默认样式相同。如果浏览器默认样式中未设置且该属性是自然继承的，那么会设置为 `inherit`
3. `unset`  --- 将属性重置为自然值，也就是如果属性是自然继承那么就是 `inherit`，否则和 `initial` 一样

-   关于文字样式的属性，都具有继承性。这些属性包括：color、 text-开头的、line-开头的、font-开头的。
-   关于盒子、定位、布局的属性，都不能继承。


## 选择器

### 1. 存否和值选择器

| 选择器          | 示例                            | 描述                                                         |
| :-------------- | :------------------------------ | :----------------------------------------------------------- |
| `[attr]`        | `a[title]`                      | 匹配带有一个名为*attr*的属性的元素——方括号里的值。           |
| `[attr=value]`  | `a[href="https://example.com"]` | 匹配带有一个名为*attr*的属性的元素，其值正为*value*——引号中的字符串。 |
| `[attr~=value]` | `p[class~="special"]`           | 匹配带有一个名为*attr*的属性的元素 ，其值正为*value*，或者匹配带有一个*attr*属性的元素，其值有一个或者更多，至少有一个和*value*匹配。注意，在一列中的好几个值，是用空格隔开的。 |
| `[attr｜=value]` | `div[lang｜="zh"]`               | 匹配带有一个名为*attr*的属性的元素，其值可正为*value*，或者开始为*value*，后面紧随着一个连字符。 |


- 使用`li[class]`，我们就能匹配任何有class属性的选择器。这匹配了除了第一项以外的所有项。
- `li[class="a"]`匹配带有一个`a`类的选择器，不过不会选中一部分值为`a`而另一部分是另一个用空格隔开的值的类，它选中了第二项。
- `li[class~="a"]`会匹配一个`a`类，不过也可以匹配一列用空格分开、包含`a`类的值，它选中了第二和第三项。



### 2. 子字符串匹配选择器

| 选择器          | 示例                | 描述                                                         |
| :-------------- | :------------------ | :----------------------------------------------------------- |
| `[attr^=value]` | `li[class^="box-"]` | 匹配带有一个名为*attr*的属性的元素，其值开头为*value*子字符串。 |
| `[attr$=value]` | `li[class$="-box"]` | 匹配带有一个名为*attr*的属性的元素，其值结尾为*value*子字符串 |
| `[attr=value]`  | `li[class*="box"]`  | 匹配带有一个名为*attr*的属性的元素，其值的字符串中的任何地方，至少出现了一次*value*子字符串。 |

### 3. 大小写敏感

如果你想在大小写不敏感的情况下，匹配属性值的话，你可以在闭合括号之前，使用`i`值。

```css
li[class^="a"] {
    background-color: yellow;
}
/*大小写不敏感：*/
li[class^="a" i] {
    color: red;
}
```

### 4. 伪类 和 伪元素

常见的伪类：

| 选择器                                                       | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`:active`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:active) | 在用户激活（例如点击）元素的时候匹配。                       |
| [`:any-link`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:any-link) | 匹配一个链接的`:link`和`:visited`状态。                      |
| [`:blank`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:blank) | 匹配空输入值的 元素   |
|   [`:checked`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:checked)  |  匹配处于选中状态的单选或者复选框。                           |
| [`:current`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:current) | 匹配正在展示的元素，或者其上级元素。                         |
| [`:default`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:default) | 匹配一组相似的元素中默认的一个或者更多的UI元素。             |
| [`:dir`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:dir) | 基于其方向性（HTML`dir`属性或者CSS`direction`属性的值）匹配一个元素。 |
| [`:disabled`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:disabled) | 匹配处于关闭状态的用户界面元素                               |
| [`:empty`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:empty) | 匹配除了可能存在的空格外，没有子元素的元素。                 |
| [`:enabled`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:enabled) | 匹配处于开启状态的用户界面元素。                             |
| [`:first`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:first) | 匹配[分页媒体](https://developer.mozilla.org/en-US/docs/Web/CSS/Paged_Media)的第一页。 |
| [`:first-child`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:first-child) | 匹配兄弟元素中的第一个元素。                                 |
| [`:first-of-type`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:first-of-type) | 匹配兄弟元素中第一个某种类型的元素。                         |
| [`:focus`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:focus) | 当一个元素有焦点的时候匹配。                                 |
| [`:focus-visible`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:focus-visible) | 当元素有焦点，且焦点对用户可见的时候匹配。                   |
| [`:focus-within`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:focus-within) | 匹配有焦点的元素，以及子代元素有焦点的元素。                 |
| [`:future`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:future) | 匹配当前元素之后的元素。                                     |
| [`:hover`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:hover) | 当用户悬浮到一个元素之上的时候匹配。                         |
| [`:indeterminate`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:indeterminate) | 匹配未定态值的UI元素，通常为[复选框](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox)。 |
| [`:in-range`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:in-range) | 用一个区间匹配元素，当值处于区间之内时匹配。                 |
| [`:invalid`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:invalid) | 匹配诸如`<input>`的位于不可用状态的元素。                    |
| [`:lang`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:lang) | 基于语言（HTML[lang](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes/lang)属性的值）匹配元素。 |
| [`:last-child`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:last-child) | 匹配兄弟元素中最末的那个元素。                               |
| [`:last-of-type`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:last-of-type) | 匹配兄弟元素中最后一个某种类型的元素。                       |
| [`:left`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:left) | 在[分页媒体](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Pages)中，匹配左手边的页。 |
| [`:link`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:link) | 匹配未曾访问的链接。                                         |
| [`:local-link`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:local-link) | 匹配指向和当前文档同一网站页面的链接。                       |
| [`:is()`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:is) | 匹配传入的选择器列表中的任何选择器。                         |
| [`:not`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:not) | 匹配作为值传入自身的选择器未匹配的物件。                     |
| [`:nth-child`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:nth-child) | 匹配一列兄弟元素中的元素——兄弟元素按照an+b形式的式子进行匹配（比如2n+1匹配元素1、3、5、7等。即所有的奇数个）。 |
| [`:nth-of-type`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:nth-of-type) | 匹配某种类型的一列兄弟元素（比如，`<p>`元素）——兄弟元素按照an+b形式的式子进行匹配（比如2n+1匹配元素1、3、5、7等。即所有的奇数个）。 |
| [`:nth-last-child`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:nth-last-child) | 匹配一列兄弟元素，从后往前倒数。兄弟元素按照an+b形式的式子进行匹配（比如2n+1匹配按照顺序来的最后一个元素，然后往前两个，再往前两个，诸如此类。从后往前数的所有奇数个）。 |
| [`:nth-last-of-type`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:nth-last-of-type) | 匹配某种类型的一列兄弟元素（比如，`<p>`元素），从后往前倒数。兄弟元素按照an+b形式的式子进行匹配（比如2n+1匹配按照顺序来的最后一个元素，然后往前两个，再往前两个，诸如此类。从后往前数的所有奇数个）。 |
| [`:only-child`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:only-child) | 匹配没有兄弟元素的元素。                                     |
| [`:only-of-type`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:only-of-type) | 匹配兄弟元素中某类型仅有的元素。                             |
| [`:optional`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:optional) | 匹配不是必填的form元素。                                     |
| [`:out-of-range`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:out-of-range) | 按区间匹配元素，当值不在区间内的的时候匹配。                 |
| [`:past`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:past) | 匹配当前元素之前的元素。                                     |
| [`:placeholder-shown`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:placeholder-shown) | 匹配显示占位文字的input元素。                                |
| [`:playing`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:playing) | 匹配代表音频、视频或者相似的能“播放”或者“暂停”的资源的，且正在“播放”的元素。 |
| [`:paused`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:paused) | 匹配代表音频、视频或者相似的能“播放”或者“暂停”的资源的，且正在“暂停”的元素。 |
| [`:read-only`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:read-only) | 匹配用户不可更改的元素。                                     |
| [`:read-write`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:read-write) | 匹配用户可更改的元素。                                       |
| [`:required`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:required) | 匹配必填的form元素。                                         |
| [`:right`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:right) | 在[分页媒体](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Pages)中，匹配右手边的页。 |
| [`:root`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:root) | 匹配文档的根元素。                                           |
| [`:scope`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:scope) | 匹配任何为参考点元素的的元素。                               |
| [`:valid`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:valid) | 匹配诸如`<input>`元素的处于可用状态的元素。                  |
| [`:target`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:target) | 匹配当前URL目标的元素（例如如果它有一个匹配当前[URL分段](https://en.wikipedia.org/wiki/Fragment_identifier)的元素）。 |
| [`:visited`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:visited) | 匹配已访问链接。                                             |

常见的伪元素：

| 选择器                                                       | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`::after`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::after) | 匹配出现在原有元素的实际内容之后的一个可样式化元素。有一个content属性 |
| [`::before`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::before) | 匹配出现在原有元素的实际内容之前的一个可样式化元素。有一个content属性 |
| [`::selection`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::selection) | 匹配文档中被用户高亮的部分（比如使用鼠标或其他选择设备选中的部分）。               |
| [`::first-letter`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::first-letter) | 匹配元素的第一个字母。                                       |
| [`::first-line`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::first-line) | 匹配包含此伪元素的元素的第一行。                             |
| [`::grammar-error`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::grammar-error) | 匹配文档中包含了浏览器标记的语法错误的那部分。               |
| [`::selection`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::selection) | 匹配文档中被选择的那部分。                                   |
| [`::spelling-error`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::spelling-error) | 匹配文档中包含了浏览器标记的拼写错误的那部分。               |



## 文本 
### text-shadow 设置文本的阴影
>参数格式：水平位移 垂直位移 模糊程度 阴影颜色。

```css
text-shadow: 20px 27px 22px pink;
```

```css
/* text-shadow 可以设置多个阴影，每个阴影之间使用逗号隔开*/
.tu {
	text-shadow: -1px -1px 1px #fff, 1px 1px 1px #000;
}
```

### border-radius 边框圆角
单个属性的写法：
```css
border-top-left-radius: 60px 120px;        /*参数解释：水平半径   垂直半径 */
border-top-right-radius: 60px 120px;
border-bottom-left-radius: 60px 120px;
border-bottom-right-radius: 60px 120px;
```
复合写法：
```css
border-radius: 60px/120px;     /*参数：水平半径/垂直半径*/
border-radius: 20px 60px 100px 140px; /*从左上开始，顺时针赋值。如果当前角没有值，取对角的值*/
border-radius: 20px 60px;
```
最简洁的写法：（四个角的半径都相同时）
```css
border-radius: 60px;
```

### box-shadow 边框阴影
格式：
```css
box-shadow: 水平偏移 垂直偏移 模糊程度 阴影大小 阴影颜色

box-shadow: 15px 21px 48px -2px #666;
```

参数解释：
-   水平偏移：正值向右 负值向左。
-   垂直偏移：正值向下 负值向上。
-   模糊程度：不能为负值。

另外，后面还可以再加一个inset属性，表示内阴影。如果不写，则默认表示外阴影：
```css
box-shadow:3px 3px 3px 3px #666 inset;
```
**注意**：设置边框阴影不会改变盒子的大小，即不会影响其兄弟元素的布局。

### border-image 边框图片

### 文字换行
#### `overflow-wrap` 通用属性。
用来说明当一个不能被分开的字符串（单词）太长而不能填充其包裹盒时，为防止其溢出，浏览器是否允许这样的单词**中断换行**。
#### `word-break` 指定了怎样在单词内断行
涉及到CJK（中文/日文/韩文）的文字换行
#### `white-space`空白处是否换行
如果想让一段很长的文本不换行，可以直接设置`white-space: nowrap` 这一个属性即可。如果想换行，可以试试`white-space: pre-wrap`。


-------
## 盒子模型

### box-sizing属性
指定盒子宽度和高度的计算方式。其值可以是：`content-box`、`border-box`。
#### 外加模式（默认方式）：
```css
box-sizing: content-box;
```
此时设置的 width 和 height 是**内容区域**的宽高。`盒子的实际宽度 = 设置的 width + padding + border`。此时改变 padding 和 border 的大小，也不会改变内容的宽高，而是盒子的总宽高发生变化。
#### 内减模式：
```css
box-sizing: border-box;
```
此时设置的 width 和 height 是**盒子**的总宽高。`盒子的实际宽度 = 设置的 width`。此时改变 padding 和 border 的大小，会改变内容的宽高，盒子的总宽高不变。



### 1. 块级盒子 Block box

- 盒子会在内联的方向上扩展并占据父容器在该方向上的所有可用空间，在绝大数情况下意味着盒子会和父容器一样宽
- 每个盒子都会换行
- [`width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width) 和 [`height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/height) 属性可以发挥作用
- 内边距（padding）, 外边距（margin） 和 边框（border） 会将其他元素从当前盒子周围“推开”

### 2. 内联盒子 Inline box

- 盒子不会产生换行。
-  [`width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width) 和 [`height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/height) 属性将不起作用。
- 垂直方向的内边距、外边距以及边框会被应用但是不会把其他处于 `inline` 状态的盒子推开。
- 水平方向的内边距、外边距以及边框会被应用且会把其他处于 `inline` 状态的盒子推开。

### 3. 盒模型的各个部分

​	CSS中组成一个块级盒子需要:

- **Content box**: 这个区域是用来显示内容，大小可以通过设置 [`width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width) 和 [`height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/height).
- **Padding box**: 包围在内容区域外部的空白区域； 大小通过 [`padding`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding) 相关属性设置。
- **Border box**: 边框盒包裹内容和内边距。大小通过 [`border`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border) 相关属性设置。
- **Margin box**: 这是最外面的区域，是盒子和其他元素之间的空白区域。大小通过 [`margin`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin) 相关属性设置。

### 4. 标准盒模型

​	在标准模型中，如果你给盒设置 `width` 和 `height`，实际设置的是 *content box*。 padding 和 border 再加上设置的宽高一起决定整个盒子的大小。

### 5. 替代(IE) 盒模型

​	这个模型，所有宽度都是可见宽度，所以内容宽度是该宽度减去边框和填充部分。

​	通过为其设置 `box-sizing: border-box` 来实现。 


## Flex 布局
`弹性盒子`：指的是用`display:flex`或`display:inline-flex`声明的父容器。
`子元素/弹性元素`：指的是父容器里面的子元素们（父容器被声明为`flex`盒子的情况下）。
`主轴`：flex容器的主轴，默认是水平方向，从左向右。
`侧轴`：与主轴垂直的轴称作侧轴，默认是垂直方向，从上往下。
主轴和侧轴并不是固定不变的，可以通过`flex-direction`更换方向。

### `flex-direction` 属性
`flex-direction`：用于设置盒子中**子元素**的排列方向。属性值可以是：

|属性值 | 描述|
| :-------------- | :-------------- |
|row|从左到右水平排列子元素（默认值）
|column|从上到下垂直排列子元素
|row-reverse|从右向左排列子元素
|column-reverse|从下到上垂直排列子元素
如果我们不给父容器写`flex-direction`这个属性，那么，子元素默认就是从左到右排列的。

### `flex-wrap` 控制子元素溢出时的换行处理。

### `justify-content` 设置子元素在主轴上的对齐方式
属性值：
-   `flex-start` 从主轴的起点对齐（默认值）
-   `flex-end` 从主轴的终点对齐
-   `center` 居中对齐
-   `space-around` 在父盒子里平分，均匀排列每个元素，每个元素周围分配相同的空间。
-   `space-between` 两端对齐 平分，均匀排列每个元素，首个元素放置于起点，末尾元素放置于终点。

### `align-items` 设置子元素在侧轴上的对齐方式
- `stretch` 元素被拉伸以适应容器（默认值）。如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。
- `center` 元素位于容器的中心。弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。
- `flex-start` 元素位于容器的开头。弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。
- `flex-end` 元素位于容器的结尾。弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。
- `baseline` 元素位于容器的基线上。如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。

### `flex` 属性设置子盒子的权重，用于设置或检索弹性盒模型对象的子元素如何分配空间



------------------------
## 定位
### 相对定位 `position: relative;`
**相对定位**：让元素相对于自己原来的位置，进行位置调整（可用于盒子的位置微调）。
不脱标，老家留坑，**别人不会把它的位置挤走**。也就是说，相对定位的真实位置还在老家，只不过影子出去了，可以到处飘。

相对定位的用途：
如果想做“压盖”效果（把一个div放到另一个div之上），我们一般**不用**相对定位来做。相对定位，就两个作用：
- 微调元素
- 做绝对定位的参考，子绝父相

#### 子绝父相:
一个绝对定位的元素，如果父辈元素中也出现了已定位（无论是绝对定位、相对定位，还是固定定位）的元素，那么将以父辈这个元素，为参考点。这里说的是父辈元素，不一定需要是直接的父元素，也可以是爷爷辈的元素。哪个忆定位的父辈元素离此子元素最近，则以这个父辈元素作为参考。
- （1）要听最近的已经定位的祖先元素的，不一定是父亲，可能是爷爷：
```html
<div class="box1">        <!--相对定位-->
	<div class="box2">    <!--没有定位-->
		<p></p>    <!--绝对定位，将以box1为参考，因为box2没有定位，box1就是最近的父辈元素-->       
	</div>
</div>
```

```html
<div class="box1">        <!--相对定位-->
	<div class="box2">    <!--相对定位-->
		<p></p>      <!--绝对定位，将以box2为参考，因为box2是自己最近的父辈元素-->     
	</div>
</div>
```

- （2）不一定是相对定位，任何定位，都可以作为儿子的参考点：
子绝父绝、**子绝父相**、子绝父固，都是可以给儿子定位的。但是在工程上，如果子绝、父绝，没有一个盒子在标准流里面了，所以页面就不稳固，没有任何实战用途。
“**子绝父相**”有意义：这样可以保证父亲没有脱标，儿子脱标在父亲的范围里面移动。于是，工程上经常这样做：
>父亲浮动，设置相对定位（零偏移），然后让儿子绝对定位一定的距离。

- （3） 绝对定位的儿子，无视参考的那个盒子的padding。

 

### 绝对定位  `position: absolute;`
**绝对定位的盒子脱离了标准文档流。**
绝对定位之后，标签就不区分所谓的行内元素、块级元素了，不需要`display:block`就可以设置宽、高了。

`让绝对定位中的盒子在父亲里居中`：
```css
div {
	width: 600px;
	height: 60px;
	position: absolute;  /*绝对定位的盒子*/
	left: 50%;           /*首先，让左边线居中*/
	top: 0;
	margin-left: -300px;  /*然后，向左移动宽度（600px）的一半*/
}
```
总结成一个公式：
> left:50%; margin-left:负的宽度的一半


### 固定定位 `position: fixed;`
就是相对浏览器窗口进行定位。无论页面如何滚动，这个盒子显示的位置不变。
备注：IE6不兼容。

**用途1**：网页右下角的“返回到顶部”:
```css
.backtop{
	position: fixed;
	bottom: 100px;
	right: 30px;
	width: 60px;
	height: 60px;
	background-color: gray;
	text-align: center;
	line-height:30px;
	color:white;
	text-decoration: none;   /*去掉超链接的下划线*/
	z-index: 99999;
}
```

只有定位了的元素，才能有z-index值。也就是说，不管相对定位、绝对定位、固定定位，都可以使用z-index值。**而浮动的元素不能用**。




## 书写模式

​	`writing-mode`的三个值分别是：

- `horizontal-tb`: 块流向从上至下。对应的文本方向是横向的。
- `vertical-rl`: 块流向从右向左。对应的文本方向是纵向的。
- `vertical-lr`: 块流向从左向右。对应的文本方向是纵向的。



## 单位
html中的单位只有一种，那就是像素px，所以单位是可以省略的，但在css中不一样，css中的单位是必须要写的，因为它没有默认单位。

### 相对单位

| 单位   | 相对于                                                       |
| :----- | :----------------------------------------------------------- |
| `em`   | 印刷单位相当于12个点。在 font-size 中使用是相对于父元素的字体大小，在其他属性中使用是相对于自身的字体大小，如 width |
| `ex`   | 字符“x”的高度                                                |
| `ch`   | 数字“0”的宽度                                                |
| `rem`  | 根元素的字体大小                                             |
| `lh`   | 元素的line-height                                            |
| `vw`   | 视窗宽度的1%                                                 |
| `vh`   | 视窗高度的1%                                                 |
| `vmin` | 视窗较小尺寸的1%                                             |
| `vmax` | 视图大尺寸的1%                                               |

### 绝对单位

| 单位 | 名称         | 等价换算            |
| :--- | :----------- | :------------------ |
| `cm` | 厘米         | 1cm = 96px/2.54     |
| `mm` | 毫米         | 1mm = 1/10th of 1cm |
| `Q`  | 四分之一毫米 | 1Q = 1/40th of 1cm  |
| `in` | 英寸         | 1in = 2.54cm = 96px |
| `pc` | 十二点活字   | 1pc = 1/16th of 1in |
| `pt` | 点           | 1pt = 1/72th of 1in |
| `px` | 像素         | 1px = 1/96th of 1in |

#### ems and rems

- **在排版属性中 em 单位的意思是“父元素的字体大小”**。
- **rem单位的意思是“根元素的字体大小”**。

---

## 图表填充

`object-fit`:

```css
/*缩小了图像，维持了图像的比例，所以图像可以整齐地充满盒子，同时由于比例保持不变，图像的一部分将会被盒子裁切掉。*/
.cover {
  object-fit: cover;
}
/*图像将会缩放到足以放到盒子里面的大小。如果它和盒子的比例不同，这将会导致“开天窗”的结果。*/
.contain {
  object-fit: contain;
}
/*让图像充满盒子，但是不会维持比例。*/
.fill {
  object-file: fill;
}
```


## 背景属性

### `background-size` 属性：背景尺寸
```css
/* 宽、高的具体数值 */
background-size: 500px 500px;

/* 宽高的百分比（相对于容器的大小） */
background-size: 50% 50%;   // 如果两个属性值相同，可以简写成：background-size: 50%;

background-size: 100% auto;  //这个属性可以自己试验一下。

/* cover：图片始终填充满容器，且保证长宽比不变。图片如果有超出部分，则超出部分会被隐藏。 */
background-size: cover;

/* contain：将图片完整地显示在容器中，且保证长宽比不变。可能会导致容器的部分区域为空白。  */
background-size: contain;
```
-   `cover`：图片始终**填充满**容器，且保证**长宽比不变**。图片如果有超出部分，则超出部分会被隐藏。
-   `contain`：将图片**完整地**显示在容器中，且保证**长宽比不变**。可能会导致容器的部分区域留白。

### `background-position` 背景定位属性
有两种方式：
- `用像素描述`
```
background-position:向右偏移量 向下偏移量;
```
属性值可以是正数，也可以是负数。比如：`100px 200px`、`-50px -120px`。
- `用单词描述`
```
background-position: 描述左右的词 描述上下的词;
```
描述左右的词：`left`、`center`、`right`
描述上下的词：`top` 、`center`、`bottom`
`background-position` 属性在设置背景图片时，非常有用处。

### `background-attachment` 设置背景图片是否固定
属性值可以是：
-   `fixed`（背景就会被固定住，不会被滚动条滚走）。
-   `scroll`（与fixed属性相反，默认属性）

### `clip-path` 裁剪出元素的部分区域做展示
`clip-path`属性可以创建一个只有元素的部分区域可以显示的剪切区域。区域内的部分显示，区域外的隐藏。
虽然`clip-path`不是背景属性，但这个属性非常强大，但往往会结合背景属性一起使用，达到一些效果。
`clip-path`属性的好处是，即使做了任何裁剪，**容器的占位大小是不变的**。

```css
div {
	width: 320px;
	height: 320px;
	border: 1px solid red;
	background: url(http://img.smyhvae.com/20191006_1410.png) no-repeat;
	background-size: cover;
	clip-path: circle(50px at 100px 100px);
	transition: clip-path .4s;
}

div:hover {
	clip-path: circle(80px at 100px 100px);
}
```




### `background-image` 渐变
- 线性渐变 `linear-gradient`
```css
background-image: linear-gradient(方向, 起始颜色, 终止颜色);
background-image: linear-gradient(to right, yellow, green);
```
方向可以是：`to left`、`to right`、`to top`、`to bottom`、角度`30deg`（指的是顺时针方向30°）。
- 径向渐变 `radial-gradient`
```css
background-image: radial-gradient(辐射的半径大小, 中心的位置, 起始颜色, 终止颜色);

background-image: radial-gradient(100px at center,yellow ,green);
```
中心点的位置可以是：at left right center bottom top。如果以像素为单位，则中心点参照的是盒子的左上角。
```css
background-image: radial-gradient(100px at center, yellow, green);
background-image: radial-gradient(at left top, yellow, green);
background-image: radial-gradient(at 50px 50px, yellow, green);
background-image: radial-gradient(100px at center,
	yellow 0%,
	green 30%,
	blue 60%,
	red 100%);
background-image: radial-gradient(100px 50px at center, yellow, green);
```
- 重复渐变 `repeating-linear-gradient`  &  `repeating-radial-gradient()`


## 动画
### 过渡：`transition`
实现元素**不同状态间的平滑过渡**（`补间动画`），经常用来制作动画效果。
```css
transition: 让哪些属性进行过度 过渡的持续时间 运动曲线 延迟时间;
```
-   `transition-property: all;` 如果希望所有的属性都发生过渡，就使用all。
-   `transition-duration: 1s;` 过渡的持续时间。
- `transition-timing-function: linear;` 运动曲线：
	`linear` 线性
	`ease` 减速
	`ease-in` 加速
	`ease-out` 减速
	`ease-in-out` 先加速后减速
-   `transition-delay: 1s;` 过渡延迟。多长时间后再执行这个过渡动画。

-   补间动画：自动完成从起始状态到终止状态的的过渡。不用管中间的状态。
-   帧动画：通过一帧一帧的画面按照固定顺序和速度播放。如电影胶片。

### 转换：`transform`
#### 1. 缩放 `scale`
格式：
```css
transform: scale(x, y);
transform: scale(2, 0.5);
```
 x：表示水平方向的缩放倍数。y：表示垂直方向的缩放倍数。如果只写一个值就是等比例缩放。

#### 2. 位移 `translate`
格式：
```css
transform: translate(水平位移, 垂直位移);
transform: translate(-50%, -50%);
```
-   参数为百分比，相对于自身移动。
-   正值：向右和向下。 负值：向左和向上。如果只写一个值，则表示水平移动。

利用translate来实现绝对定位的盒子居中：
```css
div {
	width: 600px;
	height: 60px;
	position: absolute;  /*绝对定位的盒子*/
	left: 50%;           /*首先，让左边线居中*/
	top: 0;
	/*margin-left: -300px;  然后，向左移动宽度（600px）的一半 */
	transform: translate(-50%); /*然后，利用translate，往左走自己宽度的一半*/
	}
```

3D移动： `translateX`、`translateY`、`translateZ`

#### 3. 旋转 `rotate`
格式：
```css
transform: rotate(角度);
transform: rotate(45deg);
```
正值 顺时针；负值：逆时针。
rotate 旋转时，默认是以盒子的正中心为坐标原点的。如果想**改变旋转的坐标原点**，可以用`transform-origin`属性。
```css
transform-origin: 水平坐标 垂直坐标;
transform-origin: 50px 50px;
transform-origin: center bottom;   /*旋转时，以盒子底部的中心为坐标原点*/
```
3D旋转： `rotateX`、`rotateY`、`rotateZ`。

#### 4. 透视 `perspective`
只是视觉呈现出 3d 效果，并不是正真的3d。
格式有两种写法：
-   作为一个属性，设置给父元素，作用于所有3D转换的子元素。
-   作为 transform 属性的一个值，做用于元素自身。

#### 5. 3D呈现 `transform-style`
```css
	transform-style: preserve-3d;     /* 让 子盒子 位于三维空间里 */
	transform-style: flat;            /* 让子盒子位于此元素所在的平面内（子盒子被扁平化） */
```

```html
<div class="box">
	<div class="up">上</div>
	<div class="down">下</div>
	<div class="left">左</div>
	<div class="right">右</div>
	<div class="forward">前</div>
	<div class="back">后</div>
</div>
```
```css
.box {
	width: 250px;
	height: 250px;
	/* border: 1px solid red; */
	margin: 100px auto;
	/* border-radius: 50%; */
	transform-style: preserve-3d;
	animation: gun 8s linear infinite;
	/* transform: rotateX(30deg) rotateY(-150deg); */
}

@keyframes gun {
	0% {
		transform: rotateX(0deg) rotateY(0deg);
	}
	100% {
		transform: rotateX(360deg) rotateY(360deg);
	}
}

.box>div {
	width: 100%;
	height: 100%;
	position: absolute;
	text-align: center;
	line-height: 250px;
	font-size: 60px;
	color: #daa520;
}

.left {
	background-color: rgba(2500, 0, 0, 0.3);
	transform-origin: left;
	transform: rotateY(90deg) translateX(-125px);
}

.right {
	background: rgba(0, 0, 255, 0.3);
	transform-origin: right;
	transform: rotateY(90deg) translateX(125px);
}

.forward {
	background: rgba(255, 255, 0, 0.3);
	transform: translateZ(125px);
}

.back {
	background: rgba(0, 255, 255, 0.3);
	transform: translateZ(-125px);
}

.up {
	background: rgba(255, 0, 255, 0.3);
	transform: rotateX(90deg) translateZ(125px);
}

.down {
	background: rgba(99, 66, 33, 0.3);
	transform: rotateX(-90deg) translateZ(125px);
}
```


### 动画
#### 定义动画的步骤
（1）通过@keyframes定义动画；
（2）将这段动画通过百分比，分割成多个节点；然后各节点中分别定义各属性；
（3）在指定元素里，通过 `animation` 属性调用动画。

```
定义动画：
	@keyframes 动画名{
		from{ 初始状态 }
		to{ 结束状态 }
	}

 调用：
  animation: 动画名称 持续时间；
```

animation属性的格式如下：

```
animation: 定义的动画名称 持续时间  执行次数  是否反向  运动曲线 延迟执行。(infinite 表示无限次)

animation: move1 1s  alternate linear 3;

animation: move2 4s;
```






## 表单

表单元素中的一些地基式设置：

```css
button,
input,
select,
textarea {
  font-family: inherit;
  font-size: 100%;
  box-sizing: border-box;
  padding: 0; margin: 0;
}

textarea {
  overflow: auto;
} 
```



## 表格

最有用的点：

- 使您的表格标记尽可能简单，并且保持灵活性，例如使用百分比，这样设计就更有响应性。
- 使用 [`table-layout`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/table-layout)`: fixed` 创建更可控的表布局，可以通过在标题[`width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width)中设置[`width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width)来轻松设置列的宽度。
- 使用 [`border-collapse`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-collapse)`: collapse` 使表元素边框合并，生成一个更整洁、更易于控制的外观。
- 使用`thead`、`tbody`和 `tfoot` 将表格分割成逻辑块，并提供额外的应用CSS的地方，因此如果需要的话，可以更容易地将样式层叠在一起。
- 使用斑马线来让其他行更容易阅读。
- 使用 [`text-align`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-align)直线对齐文本，使内容更整洁、更易于跟随。



## 清除浮动Float

浮动的元素，只能被有高度的盒子关住。 也就是说，如果盒子内部有浮动，这个盒子有高，那么妥妥的，浮动不会互相影响。


```html
<div class="father clearfix">
    <div class="son"></div>
</div>
```

### 第1种方式：单伪元素清除法

```css
.clearfix::after{
  content: '';
  display: block;
  clear: both;
  /*补充代码： 在网页中看不到伪元素*/
  height: 0;
  visibility: hidden;
}
```

### 第2种方式： 双伪元素清除法

```css
.clearfix::before,
.clearfix::after {
  content: '';
  display: table;
}

.clearfix::after {
  clear: both;
} 
```

 使用这种方式，还可以解决margin塌陷问题（即当div的第一个子元素设置了margin-top时，div 也会跟着一起）

```html
<head>
  <style>
    .father{
      width: 400px;
      height: 400px;
      background-color: pink;
    }

    .son{
      width: 100px;
      height: 100px;
      background-color: blue;
      margin-top: 100px;
    }

    .clearfix::before,
    .clearfix::after {
      content: '';
      display: table;
    }

    .clearfix::after {
      clear: both;
    } 
  </style>
</head>  
<body>
  <div class="father clearfix">
    <div class="son"></div>
  </div>
</body>
```

### 第3种方式， 给父元素设置overflow:hidden

```css
.father{
      width: 400px;
      height: 400px;
  		overflow: hidden;
      background-color: pink;
    }
```

### 第4种方式：内墙法
```html
<div>
	<p></p>
	<p></p>
	<p></p>
	<div class="cl"></div>
</div>

<div>
	<p></p>
	<p></p>
	<p></p>
</div>
```

```css
.cl {
	clear: both;
}
```

## 浏览器的兼容性问题

### 第1条: 解决微型盒子问题：
IE6不支持小于12px的盒子，任何小于12px的盒子，在IE6中看都大。即：IE 6不支持微型盒子。解决办法很简单，就是将盒子的字号大小，设置为**小于盒子的高**，比如，如果盒子的高为5px，那就把font-size设置为0px(0px < 5px)。
```css
height: 5px;
_font-size: 0px;
```
只要给css属性之前，加上**下划线**，这个属性就是IE6的专有属性。

### 第2条：IE6不支持用`overflow:hidden;`来清除浮动
解决方法：
```css
overflow: hidden;
_zoom: 1;
```

### 第3条：margin塌陷或margin重叠
标准文档流中，竖直方向的margin不叠加，取较大的值作为margin(水平方向的margin是可以叠加的，即水平方向没有塌陷现象)。
如果不在标准流，比如盒子都浮动了，那么两个盒子之间是没有塌陷现象的。

### 第4条：善于使用父亲的padding，而不是儿子的margin
如果父亲没有border，那么儿子的margin实际上踹的是“流”，踹的是这“行”。所以，父亲整体也掉下来了。

`margin` 这个属性，本质上描述的是兄弟和兄弟之间的距离； 最好不要用这个 marign 表达父子之间的距离。

所以，如果要表达父子之间的距离，我们一定要善于使用父亲的 `padding`，而不是儿子的margin。

### 第5条：IE6的双倍margin的bug
解决方案：
- 使浮动的方向和margin的方向，相反。
```css
loat: left;
margin-right: 40px;
```
- 使用hack：（没必要，别惯着这个IE6）
单独给队首的元素，写一个一半的margin：
```css
_margin-left:20px;
```

### 第6条：私有前缀
```
-webkit-: 谷歌 苹果
-moz-:火狐
-ms-：IE
-o-：欧朋
```

```css
background: -webkit-linear-gradient(left, green, yellow);
background: -moz-linear-gradient(left, green, yellow);
background: -ms-linear-gradient(left, green, yellow);
background: -o-linear-gradient(left, green, yellow);
background: linear-gradient(left, green, yellow);
```




## 通过CSS 绘制三角形
利用border绘制三角形:
```css
.triangle {
	width: 0;
	height: 0;
	border-top: 100px solid transparent;
	border-right: 100px solid transparent;
	border-bottom: 150px solid blue;
	border-left: 100px solid transparent;
}
```

```css
.triangle2 {
	width: 0;
	height: 0;
	border-top: 30px solid red;
	border-left: 20px solid transparent;
	border-right: 20px solid transparent;
}
```

## 通过CSS绘制太极图
```html
<div class="item" data-brief="太极图">
	<div class="border-radius"></div>
</div>
```
```css
.item {
	width: 210px;
	height: 210px;  
	background-color: #fff; 
	box-shadow: 2px 2px 5px #ccc;
}

.item::after {
	content: attr(data-brief);
	display: block;
	width: 100%;
	height: 100%;
	text-align: center;
	line-height: 210px;
	position: absolute;
	top: 0;
	left: 0;
	color: #fff;
	font-size: 18px;
	background-color: rgba(170, 170, 170, 0);
	z-index: -1;
	transition: all 0.3s ease-in;
	-webkit-transition: all 0.3s ease-in;
	-moz-transition: all 0.3s ease-in;
	-ms-transition: all 0.3s ease-in;
	-o-transition: all 0.3s ease-in;
}

.item:hover::after {
	background-color: rgba(170, 170, 170, 0.6);
	z-index: 100;
}

.item:nth-child(21) .border-radius {
	width: 180px;
	height: 90px;
	border-bottom-width: 90px;
	border-style: solid;
	border-bottom-color: green;
	background-color: red;
	border-radius: 90px;
	-webkit-border-radius: 90px;
	-moz-border-radius: 90px;
	-ms-border-radius: 90px;
	-o-border-radius: 90px;
	position: relative;

}

.item  .border-radius::after,
.item  .border-radius::before {
	content: '';
	position: absolute;
	top: 50%;
	width: 20px;
	height: 20px;
	border-width: 35px;
	border-style: solid;
	border-radius: 45px;
	-webkit-border-radius: 45px;
	-moz-border-radius: 45px;
	-ms-border-radius: 45px;
	-o-border-radius: 45px;
}

.item  .border-radius::after {
	background-color: red;
	border-color: green;
}

.item  .border-radius::before {
	background-color: green;
	border-color: red;
	right: 0;
}
```

## 让元素水平垂直居中
### 1、行内元素水平垂直居中
#### 水平居中
给父容器设置：
```css
text-align: center;
```
#### 垂直居中
让文字的行高等于盒子的高度
```css
.father {
	height: 20px;
	line-height: 20px;
}
```

### 2、块级元素水平垂直居中
#### 方式一：绝对定位 + translate（无需指定子元素的宽高）
```css
.father{
	position: relative;
	min-height: 500px;
	background: pink;
}
.son {
	position: absolute;
	background: red;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
}
```

#### 方式二：flex 布局
将父容器设置为 Flex 布局，再给父容器加个属性`justify-content: center`，这样的话，子元素就能水平居中了；再给父容器加个属性 `align-items: center`，这样的话，子元素就能垂直居中了。
```css
.father{
	display: flex;
	justify-content: center;
	align-items: center;
	min-height: 100vh;
	background: pink;
}
```
不足之处在于：给父容器设置属性`justify-content: center`和`align-items: center`之后，导致父容器里的所有子元素们都垂直居中了（如果父容器里有多个子元素的话）。

#### 方式三：flex 布局 + margin: auto
先给父容器设置 `display: flex`，再给指定的子元素设置我们再熟悉不过的 `margin: auto`，即可让这个指定的子元素在**剩余空间**里，水平垂直居中。
```css
.father{
	display: flex;
	min-height: 100vh;
	background: pink;
}
.son {
	margin: auto;
	background: red;
}
```
当我们给父容器使用 Flex 布局 时，子元素的`margin: auto`不仅能让其在水平方向上居中，**垂直方向上也是居中的**。

#### 方式四：### 绝对定位 + margin（需要指定子元素的宽高）
```css
.father{
	position: relative;
	min-height: 500px;
	background: pink;
}
.son {
	position: absolute;
	width: 200px;
	height: 100px;
	background: red;
	top: 50%;
	left: 50%;
	margin-top: -50px;
	margin-left: -100px;
}
```

## 实现移动端的红包弹窗(水平垂直居中)
```html
<body>
	<div class="content">默认文档流中的页面主体</div>
		<div class="component_popup">
			<div class="popup_mask">		
				<div class="popup_content">	
					<div class="content_box"></div>	
					<div class="content_close"></div>	
				</div>
			</div>
		</div>
</body>
```
```css
.component_popup {
	position: fixed;
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
	z-index: 100;
}

.popup_mask {
	position: fixed;
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
	background: rgba(0, 0, 0, 0.7);
}

.popup_content {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	-webkit-transform: translate(-50%, -50%);
	-moz-transform: translate(-50%, -50%);
	-ms-transform: translate(-50%, -50%);	
	-o-transform: translate(-50%, -50%);
}

.content_box {
	width: 15.45rem;
	height: 19.32rem;	
	background: url(http://img.smyhvae.com/20191010_1500_red-packet.png) no-repeat;	
	background-size: 15.45rem 19.32rem;
}

.content_close {
	width: 1.25em;	
	height: 1.25em;	
	background: url(http://img.smyhvae.com/20191010_1500_close.png) no-repeat;	
	background-size: contain;	
	margin: 0 auto;	
	margin-top: 0.5em;
}
```