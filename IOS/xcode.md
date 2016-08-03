# Reveal 使用
1. 先把 Reveal.framework 拖入项目中。
2. 在Build Phases 中删除 Reveal.framework 的引用。
3. 在“Build Settings”中的 Other Linker Flags项增加"-ObjC -framework Reveal"