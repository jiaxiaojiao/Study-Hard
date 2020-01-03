## CentOS7 SELinux 安全权限

### 目录
* [查看SELinux](#查看SELinux)
* [临时关闭](#临时关闭)
* [永久关闭](#永久关闭)
* [参考](#参考)

### 查看SELinux
* `getenforce`
* `/usr/sbin/sestatus -v`

### 临时关闭
```text
## 设置SELinux 成为permissive模式
## setenforce 1 设置SELinux 成为enforcing模式
setenforce 0
```

### 永久关闭
`vi /etc/selinux/config`

将SELINUX=enforcing改为SELINUX=disabled 

设置后需要重启才能生效

###  参考
* `https://blog.csdn.net/xinluke/article/details/51925293`
