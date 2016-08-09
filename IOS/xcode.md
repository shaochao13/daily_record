# Reveal 使用
1. 先把 Reveal.framework 拖入项目中。
2. 在Build Phases 中删除 Reveal.framework 的引用。
3. 在“Build Settings”中的 Other Linker Flags项增加"-ObjC -framework Reveal"

# Xcode 7.0 支持http协议请求数据
iOS9引入了新特性App Transport Security (ATS)，新特性要求App内访问的网络必须使用HTTPS协议。
支持http解决方案：
1. 在Info.plist中添加NSAppTransportSecurity类型Dictionary。    
2. 在NSAppTransportSecurity下添加NSAllowsArbitraryLoads类型Boolean,值设为YES