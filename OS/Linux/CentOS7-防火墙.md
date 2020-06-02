### CentOS7 防火墙

```text
Service firewalld restart 重启
Service firewalld start  开启
Service firewalld stop  关闭
systemctl status firewalld  查看状态
systemctl stop firewalld  关闭
systemctl start firewalld 开启
systemctl  restart firewalld 重启
systemctl  disable firewalld  关闭开机启动

firewall-cmd --state 查看状态

firewall-cmd --list-all 查看防火墙规则
```

### 参考
* https://www.cnblogs.com/xxoome/p/7115614.html
* https://www.jianshu.com/p/dbf2f49fb9cc

