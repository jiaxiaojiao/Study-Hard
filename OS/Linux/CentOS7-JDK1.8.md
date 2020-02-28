## Linux 安装JDK1.8

> CentOS 7 

### 目录
* [下载JDK](#下载JDK)
* [安装](#安装)

### 下载JDK
* http://www.oracle.com/technetwork/java/javase/downloads/index.html
* http://www.oracle.com/technetwork/java/javase/archive-139210.html
下载Linux x64  jdk-8u241-linux-x64.tar.gz

### 安装
* 上传到 /usr/local/src/
* Java的安装目录： /usr/java
```text
cp jdk.tar.gz /usr/java
```
* 在Java目录下，解压JDK压缩文件。
```text
tar -zxvf jdk.tar.gz
```
* 删除JDK的压缩包
```text
rm -f jdk.tar.gz
```
* 配置JDK环境变量，编辑全局变量。
```text
vim /etc/profile

#java environment
export JAVA_HOME=/usr/java/jdk1.8.0_144
export CLASSPATH=.:${JAVA_HOME}/jre/lib/rt.jar:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar
export PATH=$PATH:${JAVA_HOME}/bin
```
* 设置的环境变量生效
```text
source /etc/profile
```
* 检查Java
```text
java -version
```