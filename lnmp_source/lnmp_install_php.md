LNMP环境搭建-安装PHP
====================

## 一、环境
- CentOS7

## 二、相关资源
- [PHP官方网站](https://www.php.net/)
- [PHP官方下载页](https://www.php.net/downloads.php)

## 三、编译安装
### 1. 下载php
- 下载并解压
```
# 下载php
wget https://www.php.net/distributions/php-7.2.16.tar.gz

# 解压
tar -zxvf php-7.2.16.tar.gz
```
- 查看目录
```
[root@cloudhost ~]# ll
总用量 19232
drwxrwxr-x 14 root root     4096 3月   5 19:05 php-7.2.16
-rw-r--r--  1 root root 19686462 4月  12 15:50 php-7.2.16.tar.gz
```

### 2. 创建用户和组
```
[root@cloudhost ~]# groupadd www-data
[root@cloudhost ~]# useradd -g www-data www-data
```

### 3. 配置选项
[配置选项](https://www.php.net/manual/zh/configure.about.php)
```
./configure
--prefix=/usr/local/php
--with-config-file-path=/usr/local/php/etc
--enable-fpm
--with-fpm-user=www-data
--with-fpm-group=www-data
--enable-mbstring
--with-curl=/usr/local/curl
--with-gd
--with-zlib
--with-bz2
--enable-sockets
--enable-sysvsem
--enable-sysvshm
-enable-pcntl
--enable-mbregex
--enable-exif
--enable-bcmath
--with-mhash
--enable-zip
--with-pcre-regex
--with-pdo-mysql
--with-mysqli
--with-jpeg-dir=/usr
--with-png-dir=/usr
--with-openssl
--with-libdir=/lib/x86_64-linux-gnu/
--enable-ftp
--with-gettext
--with-xmlrpc
--enable-opcache
--with-iconv
--enable-mysqlnd
--with-mysqli=mysqlnd
--with-iconv-dir
--with-kerberos
--with-pdo-sqlite
--with-pear
--enable-libxml
--enable-shmop
--enable-xml
--enable-opcache
```

### 4. 安装
```
[root@cloudhost php-7.2.16]# make && make install
```
安装成功后，显示如下信息
```
Build complete.
Don't forget to run 'make test'.

Installing shared extensions:     /usr/local/php/lib/php/extensions/no-debug-non-zts-20170718/
Installing PHP CLI binary:        /usr/local/php/bin/
Installing PHP CLI man page:      /usr/local/php/php/man/man1/
Installing PHP FPM binary:        /usr/local/php/sbin/
Installing PHP FPM defconfig:     /usr/local/php/etc/
Installing PHP FPM man page:      /usr/local/php/php/man/man8/
Installing PHP FPM status page:   /usr/local/php/php/php/fpm/
Installing phpdbg binary:         /usr/local/php/bin/
Installing phpdbg man page:       /usr/local/php/php/man/man1/
Installing PHP CGI binary:        /usr/local/php/bin/
Installing PHP CGI man page:      /usr/local/php/php/man/man1/
Installing build environment:     /usr/local/php/lib/php/build/
Installing header files:          /usr/local/php/include/php/
Installing helper programs:       /usr/local/php/bin/
  program: phpize
  program: php-config
Installing man pages:             /usr/local/php/php/man/man1/
  page: phpize.1
  page: php-config.1
Installing PEAR environment:      /usr/local/php/lib/php/
[PEAR] Archive_Tar    - installed: 1.4.4
[PEAR] Console_Getopt - installed: 1.4.1
[PEAR] Structures_Graph- installed: 1.1.1
[PEAR] XML_Util       - installed: 1.4.3
[PEAR] PEAR           - installed: 1.10.7
Wrote PEAR system config file at: /usr/local/php/etc/pear.conf
You may want to add: /usr/local/php/lib/php to your php.ini include_path
/root/php-7.2.15/build/shtool install -c ext/phar/phar.phar /usr/local/php/bin
ln -s -f phar.phar /usr/local/php/bin/phar
Installing PDO headers:           /usr/local/php/include/php/ext/pdo/
```

## 四、配置文件
从上一步的安装选项看出，我们将配置文件设置在了 ``/usr/local/php/etc`` 目录下，需要将配置文件拷贝到该目录。
```
[root@cloudhost php-7.2.16]# cp php.ini-development /usr/local/php/etc/php.ini

[root@cloudhost php-7.2.16]# cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf

[root@cloudhost php-7.2.16]# cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf
```

## 五、注册系统服务
当PHP编译安装完成后，``php-fpm``还不是系统服务。为了方便启动、停止、重启``php-fpm``，可以将其注册为系统服务。

1. 找到 ``init.d.php-fpm`` 文件
    ```
    [root@cloudhost ~]# find / -name init.d.php-fpm
    /root/php-7.2.16/sapi/fpm/init.d.php-fpm
    ```
2. 将它拷贝到``/etc/init.d``目录下
    ```
    [root@cloudhost ~]# cp /root/php-7.2.16/sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm
    ```
3. 修改权限
    ```
    [root@cloudhost ~]# chmod 755 /etc/init.d/php-fpm
    ```

4. 启动``php-fpm``
    ```
    [root@cloudhost ~]# service php-fpm start
    Gracefully shutting down php-fpm . done
    ```

5. 停止``php-fpm``
    ```
    [root@cloudhost ~]# service php-fpm stop
    Starting php-fpm  done
    ```

6. 重启``php-fpm``
    ```
    [root@cloudhost ~]# service php-fpm reload
    Reload service php-fpm  done
    ```

## 六、添加环境变量
当尝试使用``php -v``查看PHP版本时，提示命令未找到。
```
[root@cloudhost ~]# php -v
-bash: php: 未找到命令
```
此时，需要将php添加到环境变量中。

我们可以先通过 ``echo $PATH`` 查看一下环境变量。
```
[root@cloudhost ~]# echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin
```

添加环境变量有3种方法：
- 一次性的设置，只对当前会话有效，当注销时，刚刚设置的 ``PATH`` 就会失效
```
export PATH=$PATH:/usr/local/php/bin
```

- 永久性设置，对所有用户有效，需要重启生效或使用``source``命令，将上一种方式的导出操作添加到文件``/etc/profile``的末尾。

- 永久性设置，只针对一个用户，需要重启生效或使用``source``命令，优先级高于``2``，将方式1的导出操作添加到文件``~/.bashrc``的末尾


添加了环境变量之后，通过``php -v``命令查看PHP版本。
```
[root@cloudhost ~]# php -v
PHP 7.2.15 (cli) (built: Apr 10 2019 16:52:28) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
```
