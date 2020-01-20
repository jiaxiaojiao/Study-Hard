## Linux 常用命令行脚本

> Linux /ˈlɪnʌks/

### 目录
* [查看Linux内核版本](#查看Linux内核版本)
* [安装命令](#安装命令)
* [操作文件](#操作文件)
* [操作文件夹](#操作文件夹)

### 查看Linux内核版本

1. `uname -a`
2. `lsb_release -a`
3. `cat /etc/issue`

### 安装命令
* 安装sodo `yum install sudo`
* 安装wget `yum -y install wget`

*yum 安装软件必须在联网的情况下才能操作。


### 操作文件
* 移动文件到指定目录
```text
mv xx /usr/local/
```

* 修改文件名称或文件夹名称
```text
mv xx1 xx2
```

* 解压缩
```text
tar xvzf xx.tar.gz
```

### 操作文件夹
* 删除文件夹 `rm -r` `rm -rf`
