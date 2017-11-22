# 安装(centos 7 中安装nginx)
1. 准备工作
    ```bash
    yum install -y gcc-c++ pcre pcre-devel zlib zlib-devel openssl openssl--devel 
    ```
2. 安装之前，最好检查一下是否已经安装有nginx

    ```bash
    find -name nginx 

    yum remove nginx # 如果系统已经安装了nginx，那么就先卸载
    ```
3. 下载最新的nginx ，解压。
```bash
./configure
make && make install
# 这样基本上就OK。
```

# 常用命令

```bash
# 查看版本
nginx -v # 使用 -V 可以查看 nginx 安装时依赖的模块

# 启动 nginx 服务
nginx
# 重启 nginx 服务
nginx -s reload
# 关闭 nginx 服务
nginx -s quit
# 测试 nginx.conf 配置文件合法性
nginx -t
```

*nginx 中文文档* 参考 http://www.nginx.cn/doc/index.html

# location 讲解
location 用于匹配客户端发送的 url ，从而定位请求资源。

`匹配方式大致分成 3 类`：

    1) location = xxx {} # 精准匹配
    2) location pattern {} # 一般匹配
    3) location ~ pattern {} # 正则表达式匹配

假设 Nginx 配置文件中有如下配置

```nginx
location = / {
    [ 配置 A ]
}
location / {
    [ 配置 B ]
}
location /documents/ {
    [ 配置 C ]
}
location ^~ /images/ {
    [ 配置 D ]
}
location ~* \.(gif|jpg|jpeg)$ {
    [ 配置 E ]
}
```

当请求 http://192.168.2.25/ 时，会定位到配置 A；

当请求 http://192.168.2.25/index.html 时，会定位到配置 B；

当请求 http://192.168.2.25/documents/document.html 时，会定位到配置 C；

当请求 http://192.168.2.25/images/1.gif 时，会定位到配置 D；

当请求 http://192.168.2.25/documents/1.jpg 时，会定位到配置 E。


# 访问控制( ngx_http_access_module 模块，已内置)

在 location 中配置了 deny 和 allow
```nginx
location / {
    root   /usr/share/nginx/html;
    deny   192.168.2.2;
    allow all;
    index  index.html index.htm;
}
```

# 文件压缩( ngx_http_gzip_module 模块, 已内置)
```nginx
location ~* \.(jpg|gif|png|txt|xml)$ {
    gzip on; 
    gzip_http_version 1.1;
    gzip_comp_level 6;
    gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript image/jpeg image/gif image/png
    ;
    root /opt/test;  # 压缩 /opt/test 目录下的资源
}
```

```nginx
gzip on|off;               # 是否开启 gzip，默认值为 off。
gzip_buffers 32 4k|16 8k;  # 缓冲，压缩在内存中缓存分成几块，每块大小
gzip_comp_level [1~9];     # 指定 gzip 压缩程度。推荐使用 6。压缩级别越高，越浪费 cpu 计算资源
gzip_disable MSIE [4-6]\.; # 响应 IE4~IE6 浏览器的请求时，不使用 gzip。
gzip_min_length 200;       # 大于 200 字节就进行文件压缩
gzip_http_version 1.0|1.1; # 使用 http/1.1 协议才进行文件压缩，默认值为 1.1。
gzip_types mime-type ...;  # 设置需要压缩文件的类型，如：text/plain text/css
gzip_vary on|off;          # 是否传输 gzip 压缩标识，默认值为 off。
```

# 静态资源缓存(ngx_http_headers_module 模块)
```nginx
location ~* \.(jpg|gif|png|txt|xml)$ {
    expires 24h; # 向响应头中添加 Cache-Control，设置缓存时间为 24 小时
    # root /opt/test; # 应用是用于设置 针对哪个目录上的文件进行缓存
}
```
```nginx
# 常用时间单位设置
expires 60s; # 60 秒
expires 10m; # 10 分钟
expires 2h;  # 2 小时
expires 30d; # 30 天
```

# 跨域(ngx_http_headers_module 模块)
```nginx
location ~* \.(jpg|gif|png|txt|xml)$ {
    gzip on;
    gzip_http_version 1.1;
    gzip_comp_level 2;
    gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript image/jpeg image/gif image/png
    ;
    
    # 设置允许跨域请求
    add_header 'Access-Control-Allow-Origin' '*';
    add_header 'Access-Control-Allow-Credentials' 'true';
    add_header 'Access-Control-Allow-Methods' 'GET, POST,PUT,DELETE, OPTIONS';
    
    root /opt/test;
}
```

# 防盗链(ngx_http_referer_module 模块)
```nginx
location ~* \.(jpg|gif|png|txt|xml)$ {
    # 只允许 192.168.2.25 的服务器请求资源
    valid_referers none blocked 192.168.2.25;
    if ($invalid_referer) {
            return 403;
    }
}
```

# 反向代理(ngx_http_proxy_module 模块)
```nginx
listen       80;
    
location / {
    proxy_pass http://192.168.2.25:8080; # 被代理服务器地址。
    # proxy_set_header xx xx;          # 更改 Nginx 服务器接收的客户端请求的头信息，然后将新请求头发给后端服务器。
    proxy_set_header Host $http_host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    
    proxy_connect_timeout 30; # Nginx 与后端服务器建立连接超时时间
    proxy_send_timeout 30; # Nginx 向后端服务器发送 write 请求后，等待响应的超时时间
    proxy_read_timeout 30; # Nginx 向后端服务器发送 read 请求后，等待响应的超时时间。
    
    proxy_buffering on; # 是否开启 Proxy Buffer
    proxy_buffer_size 32k; # 缓冲区大小
    proxy_buffers 4 128k; # 缓冲区数量和大小
    proxy_busy_buffers_size 256k; # 设置系统很忙时可以使用的 proxy_buffers的大小，官方推荐位 proxy_buffers * 2
    proxy_temp_file_write_size 128k;# 当后端服务器的响应过大时 Nginx 一次性写入临时文件的数据大小
    proxy_max_temp_file_size 256k; # 每个请求能用磁盘上临时文件最大大小
}
```

# 负载均衡(ngx_http_upstream_module 模块)
nginx 的 upstream目前支持 4 种方式的分配

    1)、轮询（默认） 每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器down掉，能自动剔除。
    2)、weight   指定轮询几率，weight和访问比率成正比，用于后端服务器性能不均的情况。
    2)、ip_hash  每个请求按访问ip的hash结果分配，这样每个访客固定访问一个后端服务器，可以解决session的问题。
    3)、fair（第三方）    按后端服务器的响应时间来分配请求，响应时间短的优先分配。
    4)、url_hash（第三方）

```nginx
upstream servers2.mydomain.com { 
    server 192.168.2.3:8080 down; 
    server 192.168.2.4:8081 weight=2; 
    server 192.168.2.5:8082 backup;
    ip_hash;# ip_hash技术能够将某个ip的请求定向到同一台后端，这样一来这个ip下的某个客户端和某个后端就能建立起稳固的session

    #upstream 每个设备的状态:
    # down 表示单前的server暂时不参与负载
    # weight 默认为1.weight越大，负载的权重就越大。
    # max_fails ：允许请求失败的次数默认为1.当超过最大次数时，返回proxy_next_upstream 模块定义的错误
    # fail_timeout:max_fails 次失败后，暂停的时间。
    # backup： 其它所有的非backup机器down或者忙的时候，请求backup机器。所以这台机器压力会最轻。
}

server{ 
    listen 80; 
    server_name www.mydomain.com; 
    location / { 
        proxy_pass http://servers2.mydomain.com; 
        proxy_set_header Host $host; 
        proxy_set_header X-Real-IP $remote_addr; 
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; 
    } 
}
```

# 代理缓存(ngx_http_proxy_module 模块)
Proxy Cache 机制依赖于 Proxy Buffer 机制，因此，只有当 Proxy Buffer 开启时，Proxy Cache 的配置才发挥作用。

```nginx
upstream mytomcat {
    server 192.168.2.25:8081;
    server 192.168.2.25:8082;
    server 192.168.2.25:8083;
}
proxy_cache_path /usr/proxy/cache level=1:2 keys_zone=light_cache:10m max_size=10g inactive=60m use_temp_path=off;
server {
    location / {
        proxy_pass http://mytomcat;
        
        proxy_buffering on;
        
        proxy_cache light_cache;
        proxy_cache_valid 200 304 12h;
        proxy_cache_valid any 10m;
        proxy_cache_key $host$uri$is_args$args;
        add_header Nginx-Cache "$upstream_cache_status";
    }
}
```
常用配置说明：
```nginx
proxy_cache_path xx xx ..      # 设置 Nginx 服务器存储缓存数据路径以及缓存索引相关内容
proxy_cache name|off;          # name 表示存放缓存索引的内存区域名称，off 表示关闭 Proxy Cache
proxy_cache_valid 200 304 12h; # 针对不同的 HTTP 响应状态设置不同的缓存时间
proxy_cache_key xxx;           # 设置 Nginx 服务器在内存中为缓存数据建立索引时使用的关键字
```

# 配置 HTTPS(ngx_http_ssl_module 模块)
```nginx
server {
    listen  443;
    
    ssl on;
    ssl_certificate  /etc/nginx/cert/xxx.pem;
    ssl_certificate_key  /etc/nginx/cert/xxx.key;
    
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;
}
```