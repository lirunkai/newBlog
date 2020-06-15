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

### 设置子域名

```

# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user root;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

# Load dynamic modules. See /usr/share/doc/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;
        
    server {

        listen 8080;
        root /root/cms;
        location / {
          try_files $uri $uri/ /index.html;
        }
    }

   server {
        listen 8081;
        root /root/fe;
        location / {
          try_files $uri $uri/ /index.html;
        }
   }
        
    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        
        gzip on;
        gzip_buffers 32 4k;
        gzip_http_version 1.1;
        gzip_types text/plain application/json application/x-javascript application/css application/xml application/xml+rss text/javascript application/x-httpd-php image/jpeg image/gif image/png image/x-ms-bmp;
        gzip_comp_level 5;

        location / {
          root /root/promote;
          index index.html;
          try_files $uri $uri/ $uri.html;
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }

# Settings for a TLS enabled server.
#
#    server {
#        listen       443 ssl http2 default_server;
#        listen       [::]:443 ssl http2 default_server;
#        server_name  _;
#        root         /usr/share/nginx/html;
#
#        ssl_certificate "/etc/pki/nginx/server.crt";
#        ssl_certificate_key "/etc/pki/nginx/private/server.key";
#        ssl_session_cache shared:SSL:1m;
#        ssl_session_timeout  10m;
#        ssl_ciphers HIGH:!aNULL:!MD5;
#        ssl_prefer_server_ciphers on;
#
#        # Load configuration files for the default server block.
#        include /etc/nginx/default.d/*.conf;
#
#        location / {
#        }
#
#        error_page 404 /404.html;
#            location = /40x.html {
#        }
#
#        error_page 500 502 503 504 /50x.html;
#            location = /50x.html {
#        }
#    }

}


```

代理

```
server {
    listen 80;
    server_name cms.zilvkeji.com;
    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host            $host;
        proxy_set_header X-Real-IP       $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```