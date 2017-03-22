## 方法
1. plot画二维图
    + plot(y) 只给定 y 值，默认以下标为 x 轴
    + plot(x, y) 给定 x 和 y 值
    + plot(x1, y1, x2, y2) 多条数据线
    + plot(x, y, 'r-^') 给定线条参数

2. scatter 散点图  
    + scatter(x, y)
    + scatter(x, y, size)
    + scatter(x, y, size, color)

    ```python
    x = rand(200)
    y = rand(200)
    size = rand(200) * 30
    color = rand(200)
    scatter(x, y, size, color)
    # 显示颜色条
    colorbar()
    ```

3. figure 产生多张独立的图
    ```python
    t = linspace(0, 2*pi, 50)
    x = sin(t)
    y = cos(t)
    figure()
    plot(x)
    figure()
    plot(y)
    ```

4. subplot 在一幅图中画多幅子图   
    + subplot(nrows, ncols, plot_number)    
    `nrows` -- 表示有多少行   
    `ncols` -- 表示有多少列   
    `plot_number` --表示要在第几个格子里绘制图形