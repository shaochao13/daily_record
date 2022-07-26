1. enctype属性
```txt
    application/x-www-form-urlencoded   表示在发送前编码所有字符（默认）
    multipart/form-data   不对字符编码。在使用包含文件上传控件的表单时，必须使用该值。
    text/plain    空格转换为 "+" 加号，但不对特殊字符编码。
```

## 拖拽
通过为元素增加 `draggable="true"` 来设置此元素是否可以进行拖拽操作，其中图片、链接默认是开启拖拽的。
**拖拽元素的事件监听**：（应用于拖拽元素）
-   `ondragstart`当拖拽开始时调用
-   `ondragleave` 当**鼠标离开拖拽元素时**调用
-   `ondragend` 当拖拽结束时调用
-   `ondrag` 整个拖拽过程都会调用
**目标元素的事件监听**：（应用于目标元素）
-   `ondragenter` 当拖拽元素进入时调用
-   `ondragover` 当拖拽元素停留在目标元素上时，就会连续一直触发（不管拖拽元素此时是移动还是不动的状态）
-   `ondrop` 当在目标元素上松开鼠标时调用
-   `ondragleave` 当鼠标离开目标元素时调用

**注意**：如果想让拖拽元素在目标元素里做点事情，就必须要在 `ondragover()` 里加`event.preventDefault()`这一行代码。

## 历史
在HTML5中可以通过 `window.history` 操作访问历史状态，让一个页面可以有多个历史状态
`window.history`对象可以让我们管理历史记录，可用于单页面应用，Single Page Application，可以无刷新改变网页内容。
**常用方法**：
-   window.history.forward(); // 前进
-   window.history.back(); // 后退
-   window.history.go(); // 刷新
-   window.history.go(n); //n=1 表示前进；n=-1 后退；n=0s 刷新。如果移动的位置超出了访问历史的边界，会静默失败，但不会报错。
-   通过JS可以加入一个访问状态
-   history.pushState; //放入历史中的状态数据, 设置title(现在浏览器不支持改变历史状态)

## 地理定位
### API详解
-   navigator.getCurrentPosition(successCallback, errorCallback, options) 获取当前地理信息
-   navigator.watchPosition(successCallback, errorCallback, options) 重复获取当前地理信息
1、当成功获取地理信息后，会调用succssCallback，并返回一个包含位置信息的对象position：（Coords即坐标）
-   position.coords.latitude纬度
-   position.coords.longitude经度
2、当获取地理信息失败后，会调用errorCallback，并返回错误信息error。
3、可选参数 options 对象可以调整位置信息数据收集方式。
```javascript
<script>

if (navigator.geolocation) { 

	navigator.geolocation.getCurrentPosition(successCallack, errorCallback)

} else {

	console.log('浏览器不支持获取地理位置信息')

}

function successCallack(position) {

	console.log('Success..!')
	
	var latitude = position.coords.latitude
	
	var longitude = position.coords.longitude
	
	console.log(latitude + '.....' + longitude)

}


function errorCallback(error) {

	console.log(error.message)
	
	console.log('Fail!')

}

</script>
```

## 全屏
> HTML5规范允许用户自定义网页上**任一元素**全屏显示。

### 开启/关闭全屏显示
```javascript
requestFullscreen()   //让元素开启全屏显示
cancleFullscreen()    //让元素关闭全屏显示
```
不同的浏览器需要**在此基础之上**，添加私有前缀，比如：（注意 screen 是大写）
```javascript
webkitRequestFullScreen
webkitCancleFullScreen
mozRequestFullScreen
mozCancleFullScreen
```
### 检测当前是否处于全屏状态
```javascript
document.fullScreen
//不同浏览器需要加私有前缀
document.webkitIsFullScreen
document.mozFullScreen
```
### 全屏的伪类
-   :full-screen .box {}
-   :-webkit-full-screen {}
-   :moz-full-screen {}
当元素处于全屏状态时，改变它的样式。这时就可以用到伪类。
```html
<body>
<div class="box"></div>
<script>
	var box = document.querySelector('.box')
	box.onclick = function () {
		if (box.requestFullscreen) {
			box.requestFullscreen()
		} if (box.webkitRequestFullScreen) {
			box.webkitRequestFullScreen()
		} else if (box.mozRequestFullScreen) {
			box.mozRequestFullScreen()
		}
	}
</script>
</body>
```
```css
.box {
	width: 250px;
	height: 250px;
	background-color: green;
	margin: 100px auto;
	border-radius: 50%;
}

.box:-webkit-full-screen {
	background-color: red;
}
```

## 存储
### H5 中有两种存储的方式

1、**`window.sessionStorage` 会话存储：**
-   保存在内存中。
-   **生命周期**为关闭浏览器窗口。也就是说，当窗口关闭时数据销毁。
-   在同一个窗口下数据可以共享。

2、**`window.localStorage` 本地存储**：
-   有可能保存在浏览器内存里，有可能在硬盘里。
-   永久生效，除非手动删除（比如清理垃圾的时候）。
-   可以多窗口共享。

### [#](https://web.qianguyihao.com/01-HTML/11-HTML5%E8%AF%A6%E8%A7%A3%EF%BC%88%E4%B8%89%EF%BC%89.html#web-%E5%AD%98%E5%82%A8%E7%9A%84%E7%89%B9%E6%80%A7)Web 存储的特性

（1）设置、读取方便。
（2）容量较大，sessionStorage 约5M、localStorage 约20M。
（3）只能存储字符串，可以将对象 JSON.stringify() 编码后存储。

### 常用 API
```javascript
setItem(key, value); // 设置存储内容
removeItem(key); // 根据键，删除存储内容
getItem(key); // 读取存储内容
clear(); // 清空所有存储内容
key(n); // 根据索引值来获取存储内

```

## 网络状态
通过 `window.onLine` 来检测用户当前的网络状况，返回一个布尔值。另外：

-   window.online：用户网络连接时被调用。
-   window.offline：用户网络断开时被调用（拔掉网线或者禁用以太网）。

```javascript
window.addEventListener('online', function () {
	console.log('online....')
})

window.addEventListener('offline', function () {
	console.log('offline....')
})
```

## 应用缓存
HTML5中可以轻松的构建一个离线（无网络状态）应用，只需要创建一个 `cache manifest` 缓存清单文件。缓存清单文件中列出了浏览器应缓存，以供离线访问的资源。推荐使用 `.appcache`作为后缀名，另外还要添加MIME类型。

**缓存清单文件里的内容怎样写：**
（1）顶行写CACHE MANIFEST。
（2）CACHE: 换行 指定我们需要缓存的静态资源，如.css、image、js等。
（3）NETWORK: 换行 指定需要在线访问的资源，可使用通配符（也就是：不需要缓存的、必须在网络下面才能访问的资源）。
（4）FALLBACK: 换行 当被缓存的文件找不到时的备用资源（当访问不到某个资源时，自动由另外一个资源替换）。

格式：
```sh
CACHE MANIFEST

#要缓存的文件
CACHE:
    images/img1.jpg
    images/img2.jpg

#指定必须联网才能访问的文件
NETWORK:
     images/img3.jpg
     images/img4.jpg

FALLBACK:
#当前页面无法访问是回退的页面
    404.html
# 当访问不到某个资源时，自动由另一个资源进行替换
	./css/online.css ./css/offline.css
```

在需要应用缓存在页面的根元素(html)里，添加属性manifest="demo.appcache"。路径要保证正确。
```html
<html manifest="demo.appcache">
```


[[html]] [[html5]] [[drag]] [[history]]  [[geolocation]] [[地理位置信息]] [[全屏]] [[拖拽]] [[存储]] [[sessionStorage]] [[localStorage]] [[网络状态]] [[应用缓存]]