LNMP环境搭建-安装MySQL
====================

## 一、安装准备
- MySQL官网 https://www.mysql.com/
- MySQL下载页 https://dev.mysql.com/downloads/mysql/


## 二、下载MySQL
在MySQL下载页，选择MySQL的版本。
1. 选择版本 **MySQL Community Server 5.7.23**
2. 选择 **Source Code**
3. 选择 **Generic Linux (Architecture Independent)**
4. 选择带boost版本的 **mysql-boost-5.7.23.tar.gz**
5. 复制链接地址

下载MySQL

```
yum -y install wget
wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-boost-5.7.23.tar.gz
```

## 三、环境依赖
源码方式安装MySQL所需的环境依赖：
- cmake
- make
- gcc
- gcc-c++
- bison
- ncurses
- ncurses-devel（devel是开发版本）

```
yum -y install cmake make gcc gcc-c++ bison ncurses ncurses-devel
```

## 四、安装MySQL
### 1. 解压mysql包
```
tar -zxvf mysql-boost-5.7.23.tar.gz
cd mysql-5.7.23/
```
### 2. 创建编译目录

```
mkdir configure
cd configure
```
### 3. 生成编译环境
```
cmake .. -DWITH_BOOST=../boost/boost_1_59_0/ -DWITH_EMBEDDED_SERVER=OFF
```
结果：
```
-- Configuring done
-- Generating done
-- Build files have been written to: /root/mysql-5.7.23/configure
```

#### 可能遇到的问题：
- 问题1
```
MySQL currently requires boost_1_59_0...
```
解决：因为下载的带boost的版本，只需指定正确的 **-DWITH_BOOST** 参数即可，如下

```
-DWITH_BOOST=../boost/boost_1_59_0/
```
如果是不带boost的版本，需要自己下载，并移动至解压的mysql-5.7.23目录下，在生成编译文件时，指定正确的 **-DWITH_BOOST** 参数即可

```
wget https://sourceforge.net/projects/boost/files/boost/1.59.0/boost_1_59_0.tar.gz/download
tar -zxvf boost_1_59_0.tar.gz
mv boost_1_59_0 mysql-5.7.23
```
或者指定cmake参数，系统会自己下载

```
-DDOWNLOAD_BOOST=1 -DWITH_BOOST 
```

- 问题2
```
make[2]: *** [libmysqld/examples/mysql_client_test_embedded] 错误 1
make[1]: *** [libmysqld/examples/CMakeFiles/mysql_client_test_embedded.dir/all] 错误 2
```
解决：添加以下参数

```
-DWITH_EMBEDDED_SERVER=OFF
```
### 4. 编译安装
整个过程可能需要点时间，耐心等待。
```
make && make install
```

### 5. 创建mysql用户组和用户

```
groupadd mysql
useradd -g mysql mysql
```
### 6. 设置权限
MySQL的安装目录为 **/usr/local/mysql**
```
chown -R mysql:mysql /usr/local/mysql
```
### 7. 初始化数据库

```
cd /usr/local/mysql/bin
./mysqld --initialize --user=mysql

2018-07-29T19:09:18.304497Z 0 [Warning] TIMESTAMP with implicit DEFAULT value is deprecated. Please use --explicit_defaults_for_timestamp server option (see documentation for more details).
2018-07-29T19:09:18.536280Z 0 [Warning] InnoDB: New log files created, LSN=45790
2018-07-29T19:09:18.586523Z 0 [Warning] InnoDB: Creating foreign key constraint system tables.
2018-07-29T19:09:18.649604Z 0 [Warning] No existing UUID has been found, so we assume that this is the first time that this server has been started. Generating a new UUID: e49ee151-9362-11e8-ab75-08002739fe2b.
2018-07-29T19:09:18.653045Z 0 [Warning] Gtid table is not ready to be used. Table 'mysql.gtid_executed' cannot be opened.
2018-07-29T19:09:18.653886Z 1 [Note] A temporary password is generated for root@localhost: A,uNFfDrd1yd
```
结果：生成了一个**临时密码，这个要记录下来**。同时有个警告

```
TIMESTAMP with implicit DEFAULT value is deprecated。
```
解决：

```
vim /etc/my.cnf
```
编辑配置文件，然后将 **explicit_defaults_for_timestamp=true** 写入其中。


### 8. 将mysql加入系统服务
```
cd /usr/local/mysql/support-files
cp mysql.server /etc/init.d/mysql
chkconfig --add mysql # 加入系统服务
chkconfig mysql on # 开机启动
```
### 9. 尝试开启MySQL服务

```
service mysql start
```
遇到问题，如下：

```
Starting MySQL.2018-07-30T01:14:39.000931Z mysqld_safe error: log-error set to '/var/log/mariadb/mariadb.log', however file don't exists. Create writable for user 'mysql'.
 ERROR! The server quit without updating PID file (/var/lib/mysql/localhost.localdomain.pid).
```
解决：创建该文件即可

```
mkdir /var/log/mariadb
touch /var/log/mariadb/mariadb.log
chown -R mysql:mysql /var/log/mariadb/mariadb.log
```
再次开启mysql服务

```
[root@localhost support-files]# service mysql start
Starting MySQL. SUCCESS!
```
服务开启成功了!

### 10. 登录mysql
```
[root@localhost support-files]# mysql -u root -p
-bash: mysql: 未找到命令
```
#### 解决未找到命令问题
创建软链接
```
ln -s /usr/local/mysql/bin/mysql /usr/local/bin
```
结果：
```
[root@localhost ~]# ll -a /usr/local/bin
总用量 0
drwxr-xr-x.  2 root root  19 7月  30 16:36 .
drwxr-xr-x. 15 root root 169 7月  30 02:58 ..
lrwxrwxrwx.  1 root root  26 7月  30 16:36 mysql -> /usr/local/mysql/bin/mysql
```

#### 再次登录：
##### 遇到问题

```
[root@localhost ~]# mysql -u root -p
Enter password:
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)
```
##### 解决方法
查找 **mysql.sock** 文件，发现存在于 **/var/lib/mysql/** 目录下。
```
[root@localhost ~]# find / -name 'mysql.sock'
/var/lib/mysql/mysql.sock
```
再查看配置文件 **my.cnf**
```
[mysqld]
  2 datadir=/var/lib/mysql
  3 socket=/var/lib/mysql/mysql.sock
  4 explicit_defaults_for_timestamp=true
``` 
从配置文件看出**socket**值为 **/var/lib/mysql/mysql.sock**，那么可以创建软链接到 **/tmp/mysql.sock**
```
ln -s /var/lib/mysql/mysql.sock /tmp/mysql.sock
```

##### 重新登录mysql
如果在初始化数据库时，没有记录生成的临时密码，那就得**“暴力破解”**了。

首先，关闭mysql服务
```
service mysql stop
```
接着，修改``/etc/my.cnf``，添加``skip-grant-tables``，如下
```
[mysqld]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock

skip-grant-tables
```
然后，免密登录并修改登录密码
```
mysql
# 设置账户密码并退出
update user set authentication_string=password('PASSWORD') where user='root';
flush privileges;
```
最后，将``/etc/my.cnf``中的``skip-grant-tables``删除或注释掉。

重启服务，使用密码登录
```
[root@localhost support-files]# mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 4
Server version: 5.7.23

Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

#### 提示重置自动生成的密码：
```
mysql> show databases;
ERROR 1820 (HY000): You must reset your password using ALTER USER statement before executing this statement.
```

#### 修改root用户的密码
```
mysql> alter user 'root'@'localhost' identified by '123123';
Query OK, 0 rows affected (0.00 sec)
```
或者
```
mysql> set password for root@localhost=password('123123');
Query OK, 0 rows affected, 1 warning (0.00 sec)
```
#### 重新登录MySQL
```
mysql> exit
Bye
[root@localhost ~]# mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 3
Server version: 5.7.23 Source distribution

Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```
#### 操作数据库

```
show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.00 sec)

mysql>
```
