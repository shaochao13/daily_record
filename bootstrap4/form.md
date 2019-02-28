表单元素 `<input>`, `<textarea>`, 和 `<select>` elements 在使用 `.form-control` 类的情况下，宽度都是设置为 `100%`

- 堆叠表单 (全屏宽度)：垂直方向

```html
<form>
  <div class="form-group">
    <label for="email">Email address:</label>
    <input type="email" class="form-control" id="email">
  </div>
  <div class="form-group">
    <label for="pwd">Password:</label>
    <input type="password" class="form-control" id="pwd">
  </div>
  <div class="form-check">
    <label class="form-check-label">
      <input class="form-check-input" type="checkbox"> Remember me
    </label>
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
```

- 内联表单

所有内联表单中的元素都是左对齐的。

注意：在屏幕宽度小于 `576px` 时为垂直堆叠，如果屏幕宽度大于等于`576px`时表单元素才会显示在同一个水平线上。

内联表单需要在 `<form>` 元素上添加 `.form-inline`类。
```html
<form class="form-inline">
  <label for="email">Email address:</label>
  <input type="email" class="form-control" id="email">
  <label for="pwd">Password:</label>
  <input type="password" class="form-control" id="pwd">
  <div class="form-check">
    <label class="form-check-label">
      <input class="form-check-input" type="checkbox"> Remember me
    </label>
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
```
