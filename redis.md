### 安装(centos 7)

在安装 之前，最好先安装 `gcc-c++`
```
yum install -y gcc-c++
```

## 数据结构

+ 二进制安全 (binary-safe) 的字符串。
+ 列表：按照插入顺序排序的字符串元素 (element) 的集合 (collection)。通常是链表。
+ 集合：唯一的，无序的字符串元素集合。
+ 有序集合：和集合类似，但是每个字符串元素关联了一个称为分数 (score) 的浮点数。元素总是按照分数排序，所以可以检索一个范围的元素 (例如，给我前 10，或者后 10 个元素)。
+ 哈希：由字段 (field) 及其关联的值组成的映射。字段和值都是字符串类型。这非常类似于 Ruby 或 Python 中的哈希 / 散列。
+ 位数组 (位图)：使用特殊的命令，把字符串当做位数组来处理：你可以设置或者清除单个位值，统计全部置位为 1 的位个数，寻找第一个复位或者置位的位，等等。
+ 超重对数 (HyperLogLog)：这是一个用于估算集合的基数 (cardinality，也称势，译者注) 的概率性数据结构。

### Redis 键 (Keys)
Redis 键是二进制安全的，这意味着可以使用任何二进制序列作为键，从像”foo” 这样的字符串到一个 JPEG 文件的内容。空字符串也是合法的键。

关于键的其他一些规则：

+ 不要使用太长的键，例如，不要使用一个 1024 字节的键，不仅是因为内存占用，而且在数据集中查找键时需要多次耗时的键比较。即使手头需要匹配一个很大值的存在性，对其进行哈希 (例如使用 SHA1) 是个不错的主意，尤其是从内存和带宽的角度。
+ 不要使用太短的键。用”u1000flw” 取代”user:1000:followers” 作为键并没有什么实际意义，后者更具有可读性，相对于键对象本身以及值对象来说，增加的空间微乎其微。然而不可否认，短的键会消耗少的内存，你的任务就是要找到平衡点。
+ 坚持一种模式 (schema)。例如，”object-type:id” 就不错，就像”user:1000”。点或者横线常用来连接多单词字段，如”comment:1234:reply.to”，或者”comment:1234:reply-to”。
+ 键的最大大小是 512MB。

### Redis 过期 (expires)
+ 过期时间可以设置为秒或者毫秒精度。
+ 过期时间分辨率总是 1 毫秒。
+ 过期信息被复制和持久化到磁盘，当 Redis 停止时时间仍然在计算 (也就是说 Redis 保存了过期时间)。


### 订阅redis键过期消息通知
+ 首先启用redis通知功能：

    编辑redis.conf文件，添加或启用以下内容（过期通知）：
    ```sh
    notify-keyspace-events Ex
    ```
    或者登陆redis-cli之后，输入以下命令：
    ```sh
    config set notify-keyspace-events Ex
    ```

    ```java
    import org.springframework.data.redis.connection.Message;
    import org.springframework.data.redis.connection.MessageListener;
    
    public class MyRedisKeyExpiredMessageDelegate    implements MessageListener {
    
        
        public void onMessage(Message message, byte[] pattern) {
            System.out.println("channel:" + new String(message.getChannel())
                    + ",message:" + new String(message.getBody()));
        }
    }
    ```
    ```xml
    <bean id="messageListener"
            class="org.springframework.data.redis.listener.adapter.MessageListenerAdapter">
            <constructor-arg>
                <bean class="com.zww.common.redis.MyRedisKeyExpiredMessageDelegate" />
            </constructor-arg>
        </bean>
        <bean id="redisContainer"
            class="org.springframework.data.redis.listener.RedisMessageListenerContainer">
            <property name="connectionFactory" ref="connectionFactory" />
            <property name="messageListeners">
                <map>
                    <entry key-ref="messageListener">
                        <list>
                            <!--  <bean class="org.springframework.data.redis.listener.ChannelTopic"> 
                                <constructor-arg value="__keyevent@1__:expired" /> </bean>  -->
                            <!-- <bean class="org.springframework.data.redis.listener.PatternTopic"> 
                                <constructor-arg value="*" /> </bean> -->
                            <bean class="org.springframework.data.redis.listener.PatternTopic">
                                <constructor-arg value="__key*__:expired" />
                            </bean>
                        </list>
                    </entry>
                </map>
            </property>
        </bean>
    ```



## Sentinel 哨兵

通过redis提供的sentinel模式，可以在redis集群中进行自动的故障转移。

当哨兵监测到master宕机，会自动将slave切换成master，然后通过**发布订阅模式**通知其他的从服务器，修改配置文件，让它们切换主机。

注：

1. 至少要开三个sentinel
2. sentinel要分散运行在不同的机器上

```bash
$ redis-sentinel sentinel.conf
```



## Redis cluster 分片集群

 