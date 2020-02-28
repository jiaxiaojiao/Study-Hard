## Linux 安装 MySQL

> CentOS 7

### 目录
* [安装步骤](#安装步骤)
* [数据库授权](#数据库授权)

### 安装步骤
1. 检查是否安装过MySQL
```text
rpm -qa | grep mysql

# 如果安装过MySQL，可以执行删除命令
rpm -e --nodeps mysql... 
```
2. 检查mysql用户组和用户是否存在，如果没有，则创建
```text
cat /etc/group | grep mysql
cat /etc/passwd |grep mysql
groupadd mysql
useradd -r -g mysql mysql
```
3. 从官网下载是用于Linux的Mysql安装包
```text
wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.24-linux-glibc2.12-x86_64.tar.gz
```
4. 登录MySQL
```text
mysql -uroot -p
```

### 数据库授权
1. 添加用户，授权操作所有数据库，并允许远程访问
```text
grant select,insert,update,delete on *.* to test@"%" Identified by "123456";
flush privileges;
```
2. 授权添加数据库
```text
GRANT ALL PRIVILEGES ON *.* TO 'test'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;
flush privileges;
```