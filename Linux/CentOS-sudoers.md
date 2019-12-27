## CentOS 添加 sudoers 用户

* 使用root用户登录
* 进入路径 /etc 修改sudoers文件
    * sudoers默认只有只读权限，添加写权限
    ```text
    [root@bogon ~]# cd /etc
    [root@bogon etc]# chmod u+w sudoers
    [root@bogon etc]# vim sudoers
    ```
    * root ALL=(ALL) 下添加用户
    ```text
    ## Allow root to run any commands anywhere 
    root    ALL=(ALL)       ALL
    jxj     ALL=(ALL)       ALL
    ```
* 保存