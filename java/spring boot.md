## 创建线程安全的Map 
```java
static Map<Long, User> users = Collections.synchronizedMap(new HashMap<Long, User>()); 
```


