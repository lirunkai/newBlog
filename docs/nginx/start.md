Nginx是一款高性能的HTTP和反向代理服务器

centos上安装

虚拟主机： 把一台运行在因特网上的服务器主机分成一台台的虚拟主机，每台虚拟主机都可以是一个独立的网站，可以具有独立的域名，拥有完成的internet服务器功能，同一台主机上的虚拟主机之间是完全独立的。

nginx.conf  配置文件

```
http {
 server {
 	listen 80 default;
 }
}
```

nginx可以配置三种虚拟主机：

1. 基于IP的虚拟主机
2.  基于域名的虚拟主机
3.  基于端口的虚拟主机



负载均衡

1. DNS轮训
2.  用户手动选择
3. nginx upstream模块

### HTTP Upstream

Upstream是Nginx负载均衡的主要模块， 提供了一个简单方法来实现在轮询和客户端ip之间的后端服务器负载均衡，并且还可以对后端的服务器进行健康检查

upstream指令用于设置一组可以在proxy_pass和fastcgi_pass指令中使用的代理服务器。

```
upstream backend {
	ip_hash;
	server backend1.example.com weight=5;
	server backend2.example.com:8080 down;
	server unix:/tmp/backend3;
}

server {
	location / {
		proxy_pass http://backend;
	}
}
```

通过upstream请求之后如何保持还是当前的server？也就是说不会被转发到其他的server。

增加ip_hash就可以

weight 设置权重，权重越高，被分配到的客户端越多，默认为1

down 标记服务器为永久离线状态，用于ip_hash指令



include 指令

包含其他配置文件

`include vhosts/*.conf`



try_files

按顺序检查文件是否存在，以及 返回第一个被找到的文件名。 以‘/’结尾的表示一个目录。 如果文件没有找到， 被内部重定向到最后一个参数。 且最后一个参数必须是一个URI。

```
location / {
	try_files /system/maintenacnce.html $uri $uri/index.html $uri.html @mongrel;
}

location @mongrel {
	proxy_pass http://mongrel;
}
```



白名单



```
 server {
        location / {
                deny  192.168.0.1; // 禁止该ip访问
                deny  all; // 禁止所有
            }
  }
```



适配移动端

```
server {
 location / {
        //移动、pc设备agent获取
        if ($http_user_agent ~* '(Android|webOS|iPhone)') {
            set $mobile_request '1';
        }
        if ($mobile_request = '1') {
            rewrite ^.+ http://m.baidu.com;
        }
    } 
}
```



配置跨域

```
location / {  
    add_header Access-Control-Allow-Origin *;
    add_header Access-Control-Allow-Methods 'GET, POST, OPTIONS';
    add_header Access-Control-Allow-Headers 'DNT,X-Mx-ReqToken,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Authorization';

    if ($request_method = 'OPTIONS') {
        return 204;
    }
} 
```



gzip

```
server{
    gzip on; //启动
    gzip_buffers 32 4K;
    gzip_comp_level 6; //压缩级别，1-10，数字越大压缩的越好
    gzip_min_length 100; //不压缩临界值，大于100的才压缩，一般不用改
    gzip_types application/javascript text/css text/xml;
    gzip_disable "MSIE [1-6]\."; // IE6对Gzip不友好，对Gzip
    gzip_vary on;
}
```

