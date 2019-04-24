LNMP环境搭建-安装Nginx
====================

## 安装
### 编译环境
在开始安装之前，需要将编译环境gcc、g++开发库之类提前安装好。

```
yum -y install gcc gcc-c++
```

### 依赖安装
#### 安装pcre（重定向用)
```
// 下载并解压
curl -O https://ftp.pcre.org/pub/pcre/pcre-8.42.tar.gz
tar -zxvf pcre-8.42.tar.gz
cd pcre-8.42

// 编译安装
./configure --prefix=/usr/local/pcre
make && make install
```
#### openssl（https支持）

```
yum -y install openssl-devel
```

### 下载Nginx
[Nginx官网下载页](http://nginx.org/en/download.html)

官网下载页给出了三种版本
- Mainline version
- Stable version
- Legacy verions

这里我选择使用 **Stable version**，即**稳定版本**。


```
curl -O http://nginx.org/download/nginx-1.14.0.tar.gz
```
```
tar -zxvf nginx-1.14.0.tar.gz
```

```
[root@localhost ~]# cd nginx-1.14.0
[root@localhost nginx-1.14.0]#
```
### 编译安装
创建nginx运行账户，不允许直接登录系统
```
useradd www -s /sbin/nologin
```
编译安装nginx

```
./configure --prefix=/usr/local/nginx --without-http_memcached_module --user=www --group=www --with-http_stub_status_module --with-http_ssl_module
```
```
make && make install

Configuration summary
  + using system PCRE library
  + using system OpenSSL library
  + using system zlib library

  nginx path prefix: "/usr/local/nginx"
  nginx binary file: "/usr/local/nginx/sbin/nginx"
  nginx modules path: "/usr/local/nginx/modules"
  nginx configuration prefix: "/usr/local/nginx/conf"
  nginx configuration file: "/usr/local/nginx/conf/nginx.conf"
  nginx pid file: "/usr/local/nginx/logs/nginx.pid"
  nginx error log file: "/usr/local/nginx/logs/error.log"
  nginx http access log file: "/usr/local/nginx/logs/access.log"
  nginx http client request body temporary files: "client_body_temp"
  nginx http proxy temporary files: "proxy_temp"
  nginx http fastcgi temporary files: "fastcgi_temp"
  nginx http uwsgi temporary files: "uwsgi_temp"
  nginx http scgi temporary files: "scgi_temp"
```
安装成功后/usr/local/nginx目录如下

```
[root@localhost ~]# ll /usr/local/nginx
总用量 4
drwxr-xr-x. 2 root root 4096 7月  26 20:46 conf
drwxr-xr-x. 2 root root   40 7月  26 20:46 html
drwxr-xr-x. 2 root root    6 7月  26 20:46 logs
drwxr-xr-x. 2 root root   19 7月  26 20:46 sbin
```

### 验证Nginx配置文件

```
[root@localhost ~]# cd /usr/local/nginx/sbin
[root@localhost sbin]# ./nginx -t
```
验证Nginx配置文件是否正确，正确则会出现如下两行内容
```
nginx: the configuration file /usr/local/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /usr/local/nginx/conf/nginx.conf test is successful
```
### 启动Nginx

```
[root@localhost ~]# /usr/local/nginx/sbin/nginx
```
在浏览器中输入ip地址，发现无效，查看nginx服务

```
[root@localhost sbin]# ps -ef|grep nginx
root     15615     1  0 15:46 ?        00:00:00 nginx: master process /usr/local/nginx/sbin/nginx
www      15616 15615  0 15:46 ?        00:00:00 nginx: worker process
root     15622 29750  0 15:46 pts/1    00:00:00 grep --color=auto nginx
```
关闭防火墙

```
systemctl stop firewalld.service
```
刷新浏览器，出现如下信息，即成功。

```
Welcome to nginx!
If you see this page, the nginx web server is successfully installed and working. Further configuration is required.

For online documentation and support please refer to nginx.org.
Commercial support is available at nginx.com.

Thank you for using nginx.
```
### nginx命令不存在
切换目录后，执行nginx出现 **nginx命令不存在** 的问题。解决方法：创建nginx软链接到 **/usr/bin/** 目录。
```
ln -s /usr/local/nginx/sbin/nginx /usr/bin/nginx
```


## Nginx 常用命令

```
/usr/local/nginx/nginx/sbin/nginx -s reload            # 重新载入配置文件
/usr/local/nginx/nginx/sbin/nginx -s reopen            # 重启 Nginx
/usr/local/nginx/nginx/sbin/nginx -s stop              # 停止 Nginx
```

## 相关资源
- [nginx官网](https://www.nginx.com/)
- [nginx中文站](http://www.nginx.cn/)
- [nginx中文文档](http://www.nginx.cn/doc/)
