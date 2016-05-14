## 跨域读写Cookie
+ 利用html script 标签跨域写Cookie。但由于有些浏览器开启了隐私保护策略，即使往不同域下写入了cookie，也不一定能读取出来 ，所以就有了W3C制定的P3P协议。
+ P3P协议， 通过在response的头中加入P3P协议，就可以使往跨域写cookie成功。