transform

1. Skew 斜拉

2. Scale 缩放

3. Rotate 旋转

4. Translate 位移

   

BFC,IFC,GFC,FFC



http://tridiv.com/ -- 一个用css3画图的网址，牛逼。



陀螺仪：又叫角速度传感器。陀螺仪的角度问题？

Z轴为轴，alpha的作用域为(0,360).

x轴为轴，beta的作用域为(-180,180).

y轴为轴，gamma的作用域为(-90,90).

 

获取旋转角度：

```javascript
window.addEventListener("deviceorientation", function(event){
            //处理event.alpha,event.beta及event.gamma
        },true);
```





获取罗盘校准：

```javascript
window.addEventListener("compassneedscalibration", function(event){
            alert("您的罗盘需要校准");
            event.preventDefault();
        }, true);
```





获取重力加速度:

```javascript
 window.addEventListener("devicemotion", function(event){
            //处理event.acceleration
            //x(y,z):设备在x(y,z)方向上的移动加速度值
            //event.accelerationIncludingGravity
            考虑了重力加速度后设备在x(y,z)
            //event.rotationRate
            //alpha, beta, gamma：设备绕x,y,z轴旋转的角度
        }, true);  
```

