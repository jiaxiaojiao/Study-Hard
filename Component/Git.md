## Git

### 目录
* [在Linux上安装Git](#在Linux上安装Git)
* [](#)
* [](#)
* [](#)
* [](#)
* [参考](#参考)

### 在Linux上安装Git
如果你想在 Linux 上用二进制安装程序来安装 Git，可以使用发行版包含的基础软件包管理工具来安装。 
* 如果以 Fedora 上为例，你可以使用 yum： `$ sudo yum install git`
* 如果你在基于 Debian 的发行版上，请尝试用 apt-get： `$ sudo apt-get install git`

安装日志：
```text
【本地虚拟机-VM4】
[root@bogon local]# yum install git
已加载插件：fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.163.com
 * extras: mirrors.163.com
 * updates: mirrors.163.com
base                                                                                                           | 3.6 kB  00:00:00     
extras                                                                                                         | 2.9 kB  00:00:00     
updates                                                                                                        | 2.9 kB  00:00:00     
正在解决依赖关系
--> 正在检查事务
---> 软件包 git.x86_64.0.1.8.3.1-20.el7 将被 安装
--> 正在处理依赖关系 perl-Git = 1.8.3.1-20.el7，它被软件包 git-1.8.3.1-20.el7.x86_64 需要
--> 正在处理依赖关系 rsync，它被软件包 git-1.8.3.1-20.el7.x86_64 需要
--> 正在处理依赖关系 perl(Term::ReadKey)，它被软件包 git-1.8.3.1-20.el7.x86_64 需要
--> 正在处理依赖关系 perl(Git)，它被软件包 git-1.8.3.1-20.el7.x86_64 需要
--> 正在处理依赖关系 perl(Error)，它被软件包 git-1.8.3.1-20.el7.x86_64 需要
--> 正在检查事务
---> 软件包 perl-Error.noarch.1.0.17020-2.el7 将被 安装
---> 软件包 perl-Git.noarch.0.1.8.3.1-20.el7 将被 安装
---> 软件包 perl-TermReadKey.x86_64.0.2.30-20.el7 将被 安装
---> 软件包 rsync.x86_64.0.3.1.2-6.el7_6.1 将被 安装
--> 解决依赖关系完成

依赖关系解决

======================================================================================================================================
 Package                              架构                       版本                                  源                        大小
======================================================================================================================================
正在安装:
 git                                  x86_64                     1.8.3.1-20.el7                        base                     4.4 M
为依赖而安装:
 perl-Error                           noarch                     1:0.17020-2.el7                       base                      32 k
 perl-Git                             noarch                     1.8.3.1-20.el7                        base                      55 k
 perl-TermReadKey                     x86_64                     2.30-20.el7                           base                      31 k
 rsync                                x86_64                     3.1.2-6.el7_6.1                       base                     404 k

事务概要
======================================================================================================================================
安装  1 软件包 (+4 依赖软件包)

总下载量：4.9 M
安装大小：23 M
Is this ok [y/d/N]: y
Downloading packages:
(1/5): rsync-3.1.2-6.el7_6.1.x86_64.rpm                                                                        | 404 kB  00:00:07     
(2/5): perl-Error-0.17020-2.el7.noarch.rpm                                                                     |  32 kB  00:00:08     
(3/5): perl-Git-1.8.3.1-20.el7.noarch.rpm                                                                      |  55 kB  00:00:08     
(4/5): perl-TermReadKey-2.30-20.el7.x86_64.rpm                                                                 |  31 kB  00:00:08     
git-1.8.3.1-20.el7.x86_64.rpm  FAILED                                                               ]   53 B/s | 721 kB  22:59:41 ETA 
http://mirrors.nju.edu.cn/centos/7.7.1908/os/x86_64/Packages/git-1.8.3.1-20.el7.x86_64.rpm: [Errno 12] Timeout on http://mirrors.nju.edu.cn/centos/7.7.1908/os/x86_64/Packages/git-1.8.3.1-20.el7.x86_64.rpm: (28, 'Operation too slow. Less than 1000 bytes/sec transferred the last 30 seconds')
正在尝试其它镜像。
(5/5): git-1.8.3.1-20.el7.x86_64.rpm                                                                           | 4.4 MB  00:00:04     
--------------------------------------------------------------------------------------------------------------------------------------
总计                                                                                                  102 kB/s | 4.9 MB  00:00:49     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在安装    : 1:perl-Error-0.17020-2.el7.noarch                                                                                 1/5 
  正在安装    : rsync-3.1.2-6.el7_6.1.x86_64                                                                                      2/5 
  正在安装    : perl-TermReadKey-2.30-20.el7.x86_64                                                                               3/5 
  正在安装    : git-1.8.3.1-20.el7.x86_64                                                                                         4/5 
  正在安装    : perl-Git-1.8.3.1-20.el7.noarch                                                                                    5/5 
  验证中      : perl-Git-1.8.3.1-20.el7.noarch                                                                                    1/5 
  验证中      : 1:perl-Error-0.17020-2.el7.noarch                                                                                 2/5 
  验证中      : perl-TermReadKey-2.30-20.el7.x86_64                                                                               3/5 
  验证中      : git-1.8.3.1-20.el7.x86_64                                                                                         4/5 
  验证中      : rsync-3.1.2-6.el7_6.1.x86_64                                                                                      5/5 

已安装:
  git.x86_64 0:1.8.3.1-20.el7                                                                                                         

作为依赖被安装:
  perl-Error.noarch 1:0.17020-2.el7          perl-Git.noarch 0:1.8.3.1-20.el7          perl-TermReadKey.x86_64 0:2.30-20.el7         
  rsync.x86_64 0:3.1.2-6.el7_6.1            

完毕！
```
  
### 
### 
### 
### 
### 参考
* `https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git`
* `https://git-scm.com/download/linux`