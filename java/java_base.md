## 设计模式

### 1. 单例模式实现

```java
/**
 * 单例模式
 */
public class LazyInnerClassSingleton {
    /**
     * 在使用 LazyInnerClassSingleton 的时候，默认会先初始化内部类，
     * 如果没使用，则内部类是不加载的
     */
    private LazyInnerClassSingleton(){
        if (LazyHolder.LAZY != null){
            throw new  RuntimeException("不允许创建多个实例");
        }
    }

    public static final LazyInnerClassSingleton getInstance(){
        return LazyHolder.LAZY;
    }

    public static class LazyHolder{
        private static final LazyInnerClassSingleton LAZY = new LazyInnerClassSingleton();
    }
}

```

### 2. 注册式单例模式

```java
// 1. 枚举式单例模式
public enum EnumSingleton {
    INSTANCE;

    private Object data;
    public Object getData(){
        return data;
    }

    public void setData(Object data){
        this.data = data;
    }

    public static EnumSingleton getInstance(){
        return INSTANCE;
    }
}
```

```java
// 2. 容器式单例
public class ContainerSingleton {
    private ContainerSingleton(){}
    private static Map<String, Object> ioc = new ConcurrentHashMap<>();
    public static Object getBean(String className){
        synchronized (ioc){
            if (!ioc.containsKey(className)){
                Object obj = null;
                try {
                    obj = Class.forName(className).getDeclaredConstructor().newInstance();
                }catch (Exception e){
                    e.printStackTrace();
                }
                return obj;
            } else{
                return ioc.get(className);
            }
        }
    }
}
```









+ Math 中的 round 方法

    它表示“四舍五入”，算法为 `Math.floor(x+0.5)` ，即将原来的数字加上0.5后再向下取整。
    所有符合IEEE标准的语言都采用 `四舍六入五取偶` 这样的算法
    ```java
    Math.round(-1.5) = -1
    Math.round(-1.6) = -2
    ```

+ Java 流类图结构

    以 InputStream（输入）/OutputStream（输出）为后缀的是字节流；以Reader（输入）/Writer（输出）为后缀的是字符流
    
  ![流类图结构](./images/stream.jpg) 