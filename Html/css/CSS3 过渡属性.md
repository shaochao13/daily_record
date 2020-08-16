# CSS3 过渡属性

CSS3过渡是元素从一种样式转换成另一种样式的效果。

主要包括以下两点内容：

1. 规定效果添加到哪个CSS属性上
2. 规定效果的时长



主要有5个属性用于实现动画过渡：

| 属性                       | 描述                                          |
| -------------------------- | --------------------------------------------- |
| transition                 | 用于在一个属性中设置四个过渡属性              |
| transition-property        | 应用过渡的CSS属性的名称                       |
| transition-duration        | 过渡效果花费的时间，默认为0                   |
| transition-timing-function | 过渡效果的时间曲线，默认是'ease'              |
| transition-delay           | 过渡效果何时开始，即过渡效果延时多久，默认是0 |



```css
/*使用简写的transition属性：*/
/* 这段CSS的功能：当鼠标放在div上时，width,height,rotate发生变化 */
/*需要兼容各类浏览器时，需要针对每类浏览器添加相对应的属性*/
div {
    transition: width 2s, height 2s, transform 2s;
    -webkit-transition: width 2s, height 2s, transform 2s; /* safari chrome */
    -o-transition: width 2s, height 2s, transform 2s;/* opera */
    -moz-transition: width 2s, height 2s, transform 2s;/* firefox */
}
div:hover {
    width: 200px;
    height: 200px;
    transform: rotate(45deg);
    -webkit-transform: rotate(45deg); /* safari chrome */
    -ms-transform: rotate(45deg); /* IE */
    -o-transform: rotate(45deg); /* opera */
    -moz-transform: rotate(45deg); /* firefox */
}
```



```css
/* 不使用简写的transition属性时 */
div {
    transition-property: width;
    transition-delay: 2s;
    transition-timing-function: linear;
    transition-delay: 2s;

    /* firefox */
    -moz-transition-property: width;
    -moz-transition-delay: 2s;
    -moz-transition-timing-function: linear;
    -moz-transition-delay: 2s;

    /* safari chrome */
    -webkit-transition-property: width;
    -webkit-transition-delay: 2s;
    -webkit-transition-timing-function: linear;
    -webkit-transition-delay: 2s;

    /* opera */
    -o-transition-property: width;
    -o-transition-delay: 2s;
    -o-transition-timing-function: linear;
    -o-transition-delay: 2s;
}
```



