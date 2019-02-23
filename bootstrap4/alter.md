
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
