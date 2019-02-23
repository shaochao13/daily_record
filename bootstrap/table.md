
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
