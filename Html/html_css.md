# 选择器
1. ">"作用于元素的第一代后代，空格作用于元素的所有后代.
2. *** 伪类选择符***，它允许给html不存在的标签（标签的某种状态）设置样式，比如说我们给html中一个标签元素的鼠标滑过的状态来设置字体颜色： `a:hover{color:red;}`  伪类选择符，到目前为止，可以兼容所有浏鉴器的“伪类选择符”就是 a 标签上使用 :hover 了（其实伪类选择符还有很多，尤其是 css3 中，但是因为不能兼容所有浏览器
3. 对同一元素设置不同的CSS样式时，浏览器会根据权值来判断使用哪种css样式，权值高的就使用哪种css样式。 ***标签的权值为1，类选择的权值为10，ID选择的权值最高为100.***， 例如下面的代码： * ` p{color:red;} /*权值为1*/ p span{color:green;} /*权值为1+1=2*/ .warning{color:white;} /*权值为10*/
	p span.warning{color:purple;} /*权值为1+1+10=12*/
	\#footer .note p{color:yellow;} /*权值为100+10+1=111*/``
4. 设置最高权值： *!important*,如`p{color:red!important;}`  ***!important要写在分号的前面，通过它设置的样式，具有最高权值。***

# 文字样式
* 文字排版—删除线 ， `.oldPrice{text-decoration:line-through;} `   
* 文字排版—下划线， `p a{text-decoration:underline;}`   
* 文字排版—字体， `body{font-family:"Microsoft Yahei";}` 或 `body{font-family:"微软雅黑";}` 第一种方法比第二种方法兼容性更好 一些。
* 文字排版—字号、颜色， `body{font-size:12px;color:#666}`   
* 文字排版—粗体， `p{font-weight:bold;}`  
* 文字排版—斜体， `p{font-style:italic}`   
* 段落排版— 缩进， `p{text-indent:2em;}` **2em** 的意思就是文字的2倍大小。 上面表示p 中的中文文字的段前都缩进两个空格。       
* 段落排版--行间距（行高）， `p{line-height:1.5em;}`              
* 段落排版--中文字间距、字母间距,*letter-spacing*:设置中文字间隔或者字母间隔； *word-spacing*:用来设置英文单词之间的间距。      
* 段落排版—对齐，*text-align* 可以对块状元素中的文本、图片设置对齐样式。如`div{text-align:center;}`        

# 元素分类
* **内联元素**：通过 `display:inline` 可以将元素设置为内联元素。*特点*：和其他元素都在一行上，并且元素的高度、宽度及顶部和底部边距不可设置，元素宽度就是它包含的文字或图片的宽度，不可改变。***常用的块状元素有***：`<div>、<p>、<h1>...<h6>、<ol>、<ul>、<dl>、<table>、<address>、<blockquote> 、<form>`     
* **块级元素**：通过 `display:block` 可以将其他的元素设置为块级元素。*特点*：每个块级元素都从新的一行开始，并且其后的元素也另起一行；元素的高度、宽度、行高以及顶和底边距都可设置；元素宽度在不设置的情况下，是它本身父容器的100%（和父元素的宽度一致），除非设定一个宽度。***常用的内联元素有***:`<a>、<span>、<br>、<i>、<em>、<strong>、<label>、<q>、<var>、<cite>、<code>`      
* **内联块状元素**：通过 `display:inline-block` 可以将其他元素设置为内联块状元素。*特点*:其他元素都在一行上；元素的高度、宽度、行高以及顶和底边距都可设置。***常用的内联块状元素***：`<img>、<input>`

# CSS布局模型
CSS包含3种基本的布局模型：
1. 流动模型 ***Flow*** ,***HTML网页的默认布局模式***。
> 特征：
> + 块状元素都会在所处的包含元素内*** 自上而下***按顺序垂直延伸分布，因为在默认状态下，块状元素的宽度都为100%。实际上，块状元素都会以行的形式占据位置。
> + 内联元素都会在所处的包含元素内*** 从左到右***水平分布显示。
2. 浮动模型 ***Float ***
> 当设置了float属性后，会影响紧邻其后的元素，也只会影响紧邻其后的元素。
> 清除浮动的常用方法(在受到影响的元素上)：
    1. 为元素设置**clear**属性，如clear:both;  clear:left;   clear:right。  clear 一般只设置在紧邻元素上起效果。
    2. 同时为元素设置width:100%（或固定宽度） + overflow:hidden;**overflow:hidden;width:100%;**：      
3. 层模型 ***Layer ***
>  层模型有三种形式：
> 1. 绝对定位(position:absolute), 相对于其最接近的一个具有定位属性的父包含块进行绝对定位。如果不存在这样的包含块，则相对于body元素，即相对于浏览器窗口。
> 2. 相对定位(position:relative) ,相对定位完成的过程是首先按static(float)方式生成一个元素(并且元素像层一样浮动了起来)，然后相对于以前的位置移动，移动的方向和幅度由left、right、top、bottom属性确定，偏移前的位置保留不动。
> 3. 固定定位(position:fixed),视图本身是固定的，它不会随浏览器窗口的滚动条滚动而变化，除非你在屏幕中移动浏览器窗口的屏幕位置，或改变浏览器窗口的显示大小，因此固定定位的元素会始终位于浏览器窗口内视图的某个位置，不会受文档流动影响，这与background-attachment:fixed;属性功能相同。     
    * 静态定位(static)
    * 相对定位(relative)        
        *相对于自身原有位置进行偏移*
        *仍处于标准文档流中*
        *随即拥有偏移属性和z-index属性*
    * 绝对定位(absolute,fixed)
        *建立了以包含块为基准的定位*     
        *完全脱离了标准文档流*        
        *随即拥有偏移属性和z-index属性*        
        当一个元素设置了绝对定位，没有设置宽度时，元素的宽度根据内容进行调节。     
        1. 当设置的元素没有 设置定位或偏移量的祖先元素时，在对其设置偏移后，其是html 标签元素进行偏移的，而不是body元素。
        2. 当设置的元素有 已经设置定位或者偏移的祖先元素时，在对其设置偏移后，其是针对祖先元素进行偏移。
4. Relative与Absolute组合使用
> 一个元素相对于其它元素进行定位，必须遵守如下规范：
> 1. 参照定位的元素必须是相对定位元素的前辈元素：
> ```html
<div id="box1”><!--参照定位的元素--> <div id="box2">相对参照元素进行定位</div><!--相对定位元素--></div>
```
> 2. 参照定位的元素必须加入*** position:relative***
> ```css 
#box1{ width:200px;height:200px;position:relative;}
```
> 3. 定位元素加入***position:absolute***,便可以使用top,bottom,left,right来进行偏移定位了。
> ```css 
#box2{position:absolute;top:20px;left:30px;}
```
这样box2就可以相对于父元素box1定位了。

# 样式
1. border-style(边框样式)常见样式有：`dashed(虚线) | dotted(点线) | solid(实线)`
2. ***em*** 如果元素的font-size为14px,那么 1em = 14px;如果font-size=18px,那么 1em=18px。 当给font-size设置单位为em 时，此时计算的标准以父元素的font-size为基础。
```html
 <p>以这个<span>例子</span>为例。</p> ```  
```css 
p{font-size:14px}   span{font-size:0.8em;}```
结果span 中的字体“例子”字体大小就为11.2px （14\*0.8=11.2）
3. 块状元素使用`text-align:center`不起作用，在满足*** 定宽***的条件下，可以通过`margin:0 auto`来实现居中。
4. 不定宽度的块状元素有三种方法居中：
> 1. 加入table 标签
> 2. 设置块级元素的`display:inline`，然后使用`text-align:center`来实现居中：
```html
<body>
		<div class="container">
			<ul>
				<li><a href="#">1</a></li>
				<li><a href="#">2</a></li>
				<li><a href="#">3</a></li>
			</ul>
		</div>
</body>``` 
```css
	<style>
	.container{
		text-align:center;
	}
	.container ul{
		list-style:none;
		margin:0;
		padding:0;
		display:inline;
	}
	.container li{
		margin-right:8px;
		display:inline;
	}
	</style> ```
> 3. 设置`position:relative` 和 `left:50%`,通过给父元素设置*float*,然后给父元素设置`position:relative `和`left:50% `,子元素设置`position:relative `和`left:-50% `来实现水平居中。
5. 垂直居中— 父元素高度确定的单行文本 ， 通过设置父元素的* height*和 * line-height* 高度一致来实现。
``` html 
<div class="wrap">
	<h2>hi,imooc!</h2>
</div> 
```
``` css
<style>
.container{
    height:100px;
    line-height:100px;
    background:#999;
}
</style> ```
6. 垂直居中-父元素高度确定的多行文本（方法一）
> 使用插入 table (包括tbody、tr、td)标签，同时设置 vertical-align：middle。
说到竖直居中，css 中有一个用于竖直居中的属性 vertical-align，但这个样式只有在父元素为 td 或 th 时，才会生效。        
html code:
```html
<body>
<table><tbody><tr><td class="wrap">
<div>
    <p>看我是否可以居中。</p>
    <p>看我是否可以居中。</p>
    <p>看我是否可以居中。</p>
    <p>看我是否可以居中。</p>
    <p>看我是否可以居中。</p>
</div>
</td></tr></tbody></table>
</body>
```
css code:
```css
table td{height:500px;background:#ccc}
```
7. 垂直居中-父元素高度确定的多行文本（方法二）
> 在 chrome、firefox 及 IE8 以上的浏览器下可以设置块级元素的 display 为 table-cell，激活 vertical-align 属性，但注意 IE6、7 并不支持这个样式。     
html code:
```html
<div class="container">
    <div>
        <p>看我是否可以居中。</p>
        <p>看我是否可以居中。</p>
        <p>看我是否可以居中。</p>
        <p>看我是否可以居中。</p>
        <p>看我是否可以居中。</p>
    </div>
</div>
```
css code:
```css
<style>
.container{
    height:300px;
    background:#ccc;
    display:table-cell;/*IE8以上及Chrome、Firefox*/
    vertical-align:middle;/*IE8以上及Chrome、Firefox*/
}
</style>
```
8. 隐性改变display类型
> 当为元素（不论之前是什么类型元素，display:none 除外）设置以下 2 个句之一：
    1. position : absolute
    2. float : left 或 float:right  
元素会自动变为以 display:inline-block 的方式显示，当然就可以设置元素的 width 和 height 了且默认宽度不占满父元素。     
> 如，a 标签是行内元素，所以设置它的 width 是 没有效果的，但是设置为 position:absolute 以后，就可以了：
html code:
```html
<div class="container">
    <a href="#" title="">进入课程请单击这里</a>
</div>
```
css code:
```css
<style>
.container a{
    position:absolute;
    width:200px;
    background:#ccc;
}
</style>
```

# 三列布局
> 三列布局，如果想让左右固定，中间的自适应，不能通过float来实现，需要通过position定位来实现。      
html code:
```html
<body>
    <div class="left">left</div>
    <div class="main">设计首页的第一步是设计版面布局。就象传统的报刊杂志编辑一样，我们将网页看作一张报纸，一本杂志来进行排版布局。 虽然动态网页技术的发展使得我们开始趋向于学习场景编剧，但是固定的网页版面设计基础依然是必须学习和掌握的。它们的基本原理是共通的，你可以领会要点，举一反三。</div>
    <div class="right">right</div>
</body>
```
css code:
```css
<style type="text/css">
body{ margin:0; padding:0; font-size:30px; font-weight:bold}
div{ line-height:50px}
.left{ width:200px; height:600px; background:#ccc; position:absolute; left:0; top:0}
.main{ height:600px; margin:0 310px 0 210px; background:#9CF}
.right{ height:600px; width:300px; position:absolute; top:0;right: 0; background:#FCC;}
</style>
```

