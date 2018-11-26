1. 实例变量可以为 final 但是不能是 const。
2. 没有初始化的变量自动获取一个默认值为 null。类型为数字的 变量如何没有初始化其值也是 null
3. 只有两个对象是布尔类型的：true 和 false 所创建的对象， 这两个对象也都是编译时常量。只有 true 对象才被认为是 true。 所有其他的值都是 flase。这点和 JavaScript 不一样， 像 1、 "aString"、 以及 someObject 等值都被认为是 false。
4. 和 Java 不同的是，Dart 没有 public、 protected、 和 private 关键字。如果一个标识符以 (_) 开头，则该标识符 在库内是私有的。