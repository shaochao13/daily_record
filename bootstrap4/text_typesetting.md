
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


