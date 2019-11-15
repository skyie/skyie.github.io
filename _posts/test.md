[TOC]



# LINUX命令



## 传输类

### sftp

```
ssh  fyt@202.206.64.33 （其实sftp就是ssh 的一个程式。）
sftp> get /var/www/fuyatao/index.php  /home/fuyatao/
这条语句将从远程主机的  /var/www/fuyatao/目录下将 index.php 下载到本
地  /home/fuyatao/目录下。
get -r /var/www/fuyatao/  /home  目录下载到本地


sftp> put /home/fuyatao/downloads/Linuxgl.pdf /var/www/fuyatao/
```

### ssh

ssh自动连接的脚本

```
expect -c "set timeout -1;spawn ssh root@100.95.234.122;expect *password* { send \"huawei@123\r\"};  expect *Storage* {send \"exit\r\"}; expect  eof"

```

expect 和scp结合使用

expect -c "set timeout -1;spawn bash -c \"scp ./* root@100.95.234.122:~/\";expect *password* { send \"huawei@123\r\"}; expect  eof"

**ssh指定端口登录**

1、scp指定端口传输，端口需放在scp后面

scp -P 34543 -r spark xiaojp@120.26.233.3:~/

2、ssh指定端口登录：

ssh -p 34543 xiaojp@120.26.233.3

3、通过xshell登录

![1572424883822](D:\markdown\Linux.assets\1572424883822.png)



## 软件安装

### rpm

rpm查询安装软件包

－ivh：安装显示安装进度--install--verbose--hash

－Uvh：升级软件包--Update；

－qpl：列出RPM软件包内的文件信息[Query Package list]；

－qpi：列出RPM软件包的描述信息[Query Package install package(s)]；

－qf：查找指定文件属于哪个RPM软件包[Query File]；

－Va：校验所有的RPM软件包，查找丢失的文件[View Lost]；

－e：删除包

 

rpm -q samba //查询程序是否安装

 

rpm -ivh  /media/cdrom/RedHat/RPMS/samba-3.0.10-1.4E.i386.rpm //按路径安装并显示进度

rpm -ivh --relocate /=/opt/gaim gaim-1.3.0-1.fc4.i386.rpm    //指定安装目录

 

rpm -ivh --test gaim-1.3.0-1.fc4.i386.rpm　　　 //用来检查依赖关系；并不是真正的安装；

rpm -Uvh --oldpackage gaim-1.3.0-1.fc4.i386.rpm //新版本降级为旧版本

 

rpm -qa | grep httpd　　　　　 ＃[搜索指定rpm包是否安装]--all搜索*httpd*

rpm -ql httpd　　　　　　　　　＃[搜索rpm包]--list所有文件安装目录

 

rpm -qpi Linux-1.4-6.i368.rpm　＃[查看rpm包]--query--package--install package信息

rpm -qpf Linux-1.4-6.i368.rpm　＃[查看rpm包]--file

rpm -qpR file.rpm　　　　　　　＃[查看包]依赖关系

rpm2cpio file.rpm |cpio -div    ＃[抽出文件]

 

rpm -ivh file.rpm 　＃[安装新的rpm]--install--verbose--hash

rpm -ivh

 

rpm -Uvh file.rpm    ＃[升级一个rpm]--upgrade

rpm -e file.rpm      ＃[删除一个rpm包]--erase 

常用参数

-i, --install                     install package(s)

-v, --verbose                     provide more detailed output

-h, --hash                        print hash marks as package installs (good with -v)

-e, --erase                       erase (uninstall) package

-U, --upgrade=<packagefile>+      upgrade package(s)

－-replacepkge                    无论软件包是否已被安装，都强行安装软件包

--test                            安装测试，并不实际安装

--nodeps                          忽略软件包的依赖关系强行安装

--force                           忽略软件包及文件的冲突

 

Query options (with -q or --query):

-a, --all                         query/verify all packages

-p, --package                     query/verify a package file

-l, --list                        list files in package

-d, --docfiles                    list all documentation files

-f, --file                        query/verify package(s) owning file

**解压rpm包内容**

rpm2cpio xxx.rpm | cpio -div



## 编辑类

### vim

复制粘贴错位问题

:set paste 设置为粘贴模式，然后再粘贴



## 磁盘空间类

du -h --max-depth=1

输出当前目录下各个子目录所使用的空间



## 压缩与解压缩

压缩

tar -zcvf /tmp/etc.tar.gz /etc

 

## 查询类

### find

\#!/bin/sh find . -type f -newermt '2019-05-07 00:00:00' ! -newermt '2019-05-07 18:00:00'



ln -s <src>  <dst>  dst是软连接



## 用户管理

### su

切换用户只执行一条命令的可以用:  su - oracle -c your_command 

切换用户执行一个shell文件可以用：su - oracle -s /bin/bash your_shell.sh

用户的信息





## 性能类

### top

![1572074253157](D:\markdown\Linux.assets\1572074253157.png)

09:28:33表示当前的系统时间；

1day 10:28 表示系统已运行1天10小时28分

15 users 表示当前有15个用户在登录

load average：28.95 24.34 14.00标识1分钟、5分钟、15分钟的负载情况。

load average数据是每隔5秒钟检查一次活跃的进程数，然后按特定算法计算出的数值。如果这个数除以逻辑CPU的数量，结果高于5的时候就表明系统在超负荷运转了。



**cpu状态**

![1572074426151](D:\markdown\Linux.assets\1572074426151.png)

24.6% us — 用户空间占用CPU的百分比。
13.3% sy — 内核空间占用CPU的百分比。
0.1% ni — 改变过优先级的进程占用CPU的百分比
59.1% id — 空闲CPU百分比
1.9% wa — IO等待占用CPU的百分比
0.3% hi — 硬中断（Hardware IRQ）占用CPU的百分比
0.6% si — 软中断（Software Interrupts）占用CPU的百分比

**swap分区**

![1572074534734](D:\markdown\Linux.assets\1572074534734.png)

16378M total — 交换区总量（1.6GB）
0M used — 使用的交换区总量（2.5M）
16378M free — 空闲交换区总量（1.6GB）
8652M cached — 缓冲的交换区总量（8GB）

 

不能用windows的内存概念理解这些数据：64G已使用35G。使用中的内存总量（used）指的是现在系统内核控制的内存数，空闲内存总量（free）是内核还未纳入其管控范围的数量。纳入内核管理的内存不见得都在使用中，还包括过去使用过的现在可以被重复利用的内存，内核并不把这些可被重新使用的内存交还到free中去，因此在linux上free内存会越来越少，但不用为此担心。

如果出于习惯去计算可用内存数，这里有个近似的计算公式：第四行的free + 第四行的buffers + 第五行的cached，按这个公式此台服务器的可用内存：27.5+0.55+1.6 = 29.65GB。

对于内存监控，在top里我们要时刻监控第五行swap交换分区的used，如果这个数值在不断的变化，说明内核在不断进行内存和swap的数据交换，这是真正的内存不够用了。



**查看某进程线程数量**

在Linux系统“一切都是文件”的思想贯彻指导下，所有进程的运行状态都可以用文件来获取。系统根目录/proc中，每一个数字子目录的名字都是运行中的进程的PID，进入任一个进程目录，可通过其中文件或目录来观察进程的各项运行指标，例如task目录就是用来描述进程中线程的，因此也可以通过下面的方法获取某进程中运行中的线程数量（PID指的是进程ID）

![1572074875732](D:\markdown\Linux.assets\1572074875732.png)



**查看进程内存占用情况**

pmap <pid>





# Git使用

## 基本命令



## 常见问题解决

### git删除本地存在远端不存在的分支

git fetch -p

### git 指定用户名和密码提交

git clone <https://username:password@git.oschina.net/wdm/familycloud.git>

### git提示unlink files

git config --global gc.auto 0  

ref <http://3ms.huawei.com/km/blogs/details/1992913>

### git merge 模拟

git merge --no-commit --no-off  <branch_name>

撤销合并 git merge --abort

### 比较本地和远端差异

git diff master foobar/master

### 已commit，还未push，回退代码

git  reset  --hard  HEAD^

HEAD^ 表示上一个版本  HEAD^^ 表示上两个版本  HEAD~100  表示上100个版本

### rebase

![1571904535018](D:\markdown\Linux.assets\1571904535018.png)

remote填要push的分支，同时勾选unkonwn
changes

### git pull branch diverged解决

git reset --hard origin/<分支名>

# 调试类

## gdb



info symbol  <十六进制地址>  显示地址对应的函数名称

set solib-search-path /opt/dsware/eds/eds/lib   堆栈中的问号使用这个命令找到对应库的路径



Program received signal SIG61, Real-time event 61

**handle** <signal_name>  nostop

### 设置进程启动参数

show args

gdb -args ./a.out a b c



忽略信号

handle SIG60 noprint nostop

handle SIG61 noprint nostop

handle SIGUSR2 noprint nostop



### 打印进程所有线程堆栈

cd /OSM/bin/gdb_lwt/

sudo /OSM/bin/gdb_lwt/gdb -q -nx /proc/`pidof app_data`/exe -p `pidof app_data` <<< "thread apply all bt"

sudo /OSM/bin/gdb_lwt/gdb -q -nx /proc/`pidof djob`/exe -p `pidof djob` <<< "thread apply all bt"







## valgrind



## addr2line

addr2line -e ./upf-unit-test -f 0x51507f  打印地址对应的行号



# makefile



# Python

## Python起HTTP server

python -m SimpleHTTPServer 8080

  





# docker



sftp



ssh



addr2line

# shell语法

## if使用

**字符串判断**

str1 = str2　　　　　　当两个串有相同内容、长度时为真

str1 != str2　　　　　 当串str1和str2不等时为真

-n str1　　　　　　　 当串的长度大于0时为真(串非空)

-z str1　　　　　　　 当串的长度为0时为真(空串)

str1　　　　　　　　   当串str1为非空时为真

**数字的判断** 

int1 -eq int2　　　　两数相等为真

int1 -ne int2　　　　两数不等为真

int1 -gt int2　　　　int1大于int2为真

int1 -ge int2　　　　int1大于等于int2为真

int1 -lt int2　　　　int1小于int2为真

int1 -le int2　　　　int1小于等于int2为真

**文件的判断**

-r file　　　　　用户可读为真

-w file　　　　　用户可写为真

-x file　　　　　用户可执行为真

-f file　　　　　文件为正规文件为真

-d file　　　　　文件为目录为真

-c file　　　　　文件为字符特殊文件为真

-b file　　　　　文件为块特殊文件为真

-s file　　　　　文件大小非0时为真

-t file　　　　　当文件描述符(默认为1)指定的设备为终端时为真

逻辑判断

-a 	与

-o	或

！	非



**遍历**

带空格字符串遍历

```
for ((i = 0; i < ${#FILES[@]}; i++)) do     echo "${FILES[$i]}" done
```



## 特殊符号含义

| 变量 | 含义                                                         |
| ---- | ------------------------------------------------------------ |
| $0   | 当前脚本的文件名                                             |
| $n   | 传递给脚本或函数的参数。n   是一个数字，表示第几个参数。例如，第一个参数是$1，第二个参数是$2。 |
| $#   | 传递给脚本或函数的参数个数。                                 |
| $*   | 传递给脚本或函数的所有参数。                                 |
| $@   | 传递给脚本或函数的所有参数。被双引号("   ")包含时，与 $* 稍有不同，下面将会讲到。 |
| $?   | 上个命令的退出状态，或函数的返回值。                         |
| $$   | 当前Shell进程ID。对于   Shell 脚本，就是这些脚本所在的进程ID。 |
| $!   | Shell最后运行的后台Process的PID                              |

$* 和$@区别

![1571905148848](D:\markdown\Linux.assets\1571905148848.png)



shell显示时间，纳秒级别

date +"%Y-%m-%d %H:%M:%S.%N"

2019-10-25 16:51:14.445769126



## 每过100ms shell执行

```
#!/bin/bash

for ((i=1;i<=100;i++));
do
        echo `date +"%Y-%m-%d %H:%M:%S.%N"` $i
        usleep 100000  # 100 ms
done

```

![1571993763621](D:\markdown\Linux.assets\1571993763621.png)



## 数组

第一种

```
for element in ${array[@]}
do
	echo $element
done
```



## echo





## 数字计算

```
echo "a + b = $((a + b))"
echo "a * b = $((a * b))"
echo "a - b = $((a - b))"
echo "a / b = $((a / b))"
echo "a % 3 = $((a % b))"
echo "a++ = $((a++))"
```



