## Maven

### 目录
* [Linux安装Maven](#Linux-安装Maven)
* [参考](#参考)

### Linux 安装Maven
跟Windows下安装Maven差不多。

* 下载Maven
`wget http://us.mirrors.quenda.co/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz`
* 解压
`tar -zxvf apache-maven-3.6.3-bin.tar.gz`
* 配置国内镜像仓库（国内下载会快一些），本地仓库。编辑./conf/settings.xml 添加镜像
```text
<localRepository>/usr/local/maven/repo</localRepository>
```
* 配置环境变量 /etc/profile
```text
# set Maven environment
export MAVEN_HOME=/usr/local/apache-maven-3.6.3/
export PATH=$MAVEN_HOME/bin:$PATH
```
* 刷新环境变量。 `source /etc/profile`
* 验证 `mvn –v`

### 参考
* 网站 https://maven.apache.org/
* 下载 https://maven.apache.org/download.cgi
* Maven Repository（推荐使用） https://mvnrepository.com/
* 查询 Maven https://search.maven.org/
