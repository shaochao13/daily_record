# CSS HINT

1. 不要使用多个class选择元素，如a.foo.boo,这在ie6及以下不能正确解析

2. 移除空的css规则，如a{}

3. 正确的使用显示属性，如display:inline不要和width、height、float、margin、padding同时使用，display:inline-block不要和float同时使用等。

4. 避免过多的浮动，当浮动次数超过十次时，会显示警告。

5. 避免使用过多的字号，当字号声明超过十种时，显示警告。

6. 避免使用过多web字体，当使用超过五次时，显示警告。

7. 避免使用id作为样式选择器

8. 标题元素只定义一次

9. 使用width:100%时要小心 

10. 属性值为0时，不要写单位

11. 各浏览器专属的css属性要有规范

    ```css
    /*例如：*/
    foo{-moz-border-radius:5px;border-radius:5px;}
    ```

12. 避免使用看起来像正则表达式的css3选择器

13. 遵守盒模规则

