
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
