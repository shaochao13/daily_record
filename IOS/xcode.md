# Reveal 使用
- 添加：
    1. 先把 Reveal.framework 拖入项目中。
    2. 在Build Phases 中删除 Reveal.framework 的引用。
    3. 在“Build Settings”中的 Other Linker Flags项增加"-ObjC -framework Reveal"
- 移除:
    1. 从 Project Navigator 中删除 Reveal.framework 的引用。
    2. 在Xcode的 Project Navigator中选中您的工程，对于每一个集成了Reveal得target，请选择 Build Settings 标签页，将下面内容从 Debug 配置中的 Other Linked Flags 设置中移除：    
        > -framework Reveal       
        > -ObjC and -lz (删除前请确认此配置内容仅是用于Reveal)。      

# Xcode 7.0 支持http协议请求数据
iOS9引入了新特性App Transport Security (ATS)，新特性要求App内访问的网络必须使用HTTPS协议。
支持http解决方案：
1. 在Info.plist中添加NSAppTransportSecurity类型Dictionary。    
2. 在NSAppTransportSecurity下添加NSAllowsArbitraryLoads类型Boolean,值设为YES

# Facebook SocketRocket 使用注意事项：
1. 报如下错：
    ```
    Undefined symbols for architecture arm64:
    "_OBJC_CLASS_$_FBSession", referenced from: someFile
    ld: symbol(s) not found for architecture arm64
    ```
    解决方法："Build Settings" --> "Other Linker Flags" 中，添加"$(inherited)"。