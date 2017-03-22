[matplotlib官网](http://matplotlib.org/index.html)
## 方法
1. plot画二维图
    + plot(y) 只给定 y 值，默认以下标为 x 轴
    + plot(x, y) 给定 x 和 y 值
    + plot(x1, y1, x2, y2) 多条数据线
    + plot(x, y, 'r-^') 给定线条参数

    `在脚本中使用 plot 时，通常图像是不会直接显示的，需要增加 show() 选项，只有在遇到 show() 命令之后，图像才会显示`

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

    ```python
    subplot(1, 2, 1) # 在第一个格子里绘制plot(x)
    plot(x)
    subplot(1, 2, 2) # 在第二个格子里绘制plot(x)
    plot(y)
    ```

5. legend 添加标签  

    ```python
    plot(x, label='sin')
    plot(y, label='cos')
    legend()
    ```
    或者直接在 legend中加入:    

    ```python
    plot(x)
    plot(y)
    legend(['sin', 'cos'])
    ```

6. 坐标轴，标题，网格

    ```python
    plot(x, sin(x))
    xlabel('radians') # 设置x轴
    # 可以设置字体大小
    ylabel('amplitude', fontsize='large')  # 设置y轴
    title('Sin(x)') # 设置图的标题
    grid(linestyle=':') # 设置网格
    ```

7. 清除、关闭图像  

    + 清除已有的图像使用： `clf()`    
    + 关闭当前图像：   `close()`
    + 关闭所有图像：   `close('all')`

8. imshow 显示图片
    ```python
    imshow(img,
       # 设置坐标范围
      extent = [-25, 25, -25, 25],
       # 设置colormap
      cmap = cm.bone)
      # cm 表示 colormap ,可以通过dir(cm) 查看cm的种类
    ```

