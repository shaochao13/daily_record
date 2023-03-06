## JavaScript 基础知识

### Hello,World!

#### script 标签

可以使用 &lt;script&gt; 标签将 javascript 程序插入到 html 文档中的任何位置。当浏览器遇到 &lt;script&gt; 标签时，代码会自动运行。

```html
<script>
  alert('Hello, World!')
  console.log('Hello, World!')
</script>
```

#### 外部脚本

可以 &lt;script&gt; 标签的`src`属性来添加外部的 js 文件。

```html
<!-- js文件在网站内部的绝对路径 -->
<script src="/path/to/example.js"></script>

<!-- js文件在网站内部的相对路径 -->
<script src="../example.js"></script>
<!-- 加载外部的js文件,使用外部JS文件的完整的url地址 -->
<script
  src="https://unpkg.com/react@18/umd/react.development.js"
  crossorigin></script>
```

如果&lt;script&gt;设置了`src`属性的值，则标签内的内容将会被忽略。

```html
<script src="./example.js">
  // 此处编写的任何代码将会被忽略，因为提供了 src
  console.log('Hello, World!')
</script>
```

在&lt;script&gt;标签中，不要同时有 src 属性和内部包裹的代码。
