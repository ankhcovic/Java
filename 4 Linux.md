# 1 Linux 常用命令

![img](https://img-blog.csdn.net/20180524222515956?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thaV96b25l/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

## 1.1 切换目录命令：cd

cd app  切换到app目录

cd ..       切换到上一层目录

cd /        切换到系统根目录

cd ~       切换到用户主目录

cd -        切换到上一个所在目录

## 1.2 列出文件列表：ls

在linux中以 . 开头的文件都是隐藏的文件

​	ls[参数] [路径或文件名]

​	ls -a 显示所有文件或目录（包含隐藏的文件）

​	ls -l (缩写成ll) 罗列出当前文件或目录的详细信息，含有时间、读写权限、大小、时间等信息

## 1.3 创建目录和移除目录：mkdir rmdir

mkdir(make directory)	用来创建子目录。

mkdir app						  在当前目录下创建app目录

mkdir –p app2/test 		 级联创建aap2以及test目

***

rmdir(remove directory) 用来删除“空”的子目录：

rmdir app 						  删除app目录

## 1.4 浏览文件：cat more less tail

cat		显示文件的内容		格式：cat[参数]<文件名>

​				cat yum.conf

***

more	显示的内容超过一个画面长度，按空格键显示下一个画，回车显示下一行内容，按 q 键退出查看。

​				more yum.conf

***

less	   用法和more类似，不同的是less可以通过PgUp、PgDn键来控制。

​				less yum.conf

***

tail		用于显示文件后几行的内容。

tail -10 /etc/passwd 	查看后10行数据

tail -f catalina.log 		动态查看日志(*****)

ctrl+c 							 结束查看

## 1.5 文件操作：rm cp mv tar

rm 删除文件

​	用法：rm [选项]... 文件...

​		rm a.txt 		删除a.txt文件，删除需要用户确认，y/n

***

rm 删除不询问

​		rm -f a.txt	 不询问，直接删除

***

rm 删除目录

​		rm -r a 		  递归删除

***

不询问递归删除（慎用）

​		rm -rf a 		 不询问递归删除

​		rm -rf * 		 删除所有文件

​		rm -rf /*		 自杀

***

cp(copy)命令可以将文件从一处复制到另一处。一般在使用cp命令时将一个文件复制成另一个文件或复制到某目录时，需要指定源文件名与目标文件名或目录。

​		cp a.txt b.txt 	 将a.txt复制为b.txt文件

​		cp a.txt ../ 		  将a.txt文件复制到上一层目录中

***

mv 移动或者重命名

​		mv a.txt ../ 		 将a.txt文件移动到上一层目录中

​		mv a.txt b.txt     将a.txt文件重命名为b.txt

****

tar 打包或解压

tar命令位于/bin目录下，它能够将用户所指定的文件或目录打包成一个文件，但不做压缩。一般Linux上常用的压缩方式是选用tar将许多文件打包成一个文件，再以gzip压缩命令压缩成xxx.tar.gz(或称为xxx.tgz)的文件。

​		-c：创建一个新tar文件

​		-v：显示运行过程的信息

​		-f：指定文件名

​		-z：调用gzip压缩命令进行压缩

​		-t：查看压缩文件的内容

​		-x：解开tar文件

打包：

​		tar –cvf xxx.tar ./*

打包并且压缩：

​		tar –zcvf xxx.tar.gz ./* 

解压 

   	tar –xvf xxx.tar

​	   tar -xvf xxx.tar.gz -C /usr/aaa

***

grep：查找符合条件的字符串。

​	 grep [选项]... PATTERN [FILE]...

​	 grep lang anaconda-ks.cfg 在文件中查找lang

​	 grep lang anaconda-ks.cfg –color 高亮显示

## 1.6 其他常用命令

pwd		   显示当前所在目录

touch		创建一个空文件

​					touch a.txt

ll-h			 友好显示文件大小

wget		  下载资料wget http://nginx.org/download/nginx-1.9.12.tar.gz

***

z		 systemctl get-default

 		命令行模式  :multi-user.target
 	
 		图形界面模式:graphical.target

设置为图形界面模式

​		 systemctl set-default graphical.target

设置为命令行模式

 		systemctl set-default multi-user.target

***

man *** 帮助命令

***

firewall-cmd --state  *#查看防火墙* 

systemctl status firewalld *#查看防火墙* 

systemctl stop firewalld *#临时关闭防火墙* 

systemctl start firewalld *#临时打开防火墙* 

systemctl disable firewalld *#开机禁止启动防火墙* 

systemctl enable firewalld *#开机启动防火墙*



# 2 Vi和Vim编辑器

​		命令行模式 插入模式 底行模式

## 2.1 Vim编辑器

光标移动

行首：shift+6

行尾：shift+4

首行：gg(good game)

翻屏：上ctrl+b(before)	下ctrl+f(after)

***

复制操作

复制当前行：yy 

以当前行为准，向下复制n行：数字 yy 

***

粘贴：p 

可视化复制：ctrl+v

剪切/删除光标所在行：dd

以当前行为准，向下剪切/删除n行：数字 dd 

剪切/删除光标所在行但不上移：D

替换：R

***

撤销：:u(不属于命令模式)/u(undo)

恢复：ctrl+r((recovery)

***

打开文件：vim file

退出：esc/q

修改文件：输入i进入插入模式

保存并退出：esc/wq

不保存退出：esc/q!

***

切换到命令行模式：按Esc键；

切换到插入模式：按 i 、o、a键；

  i 在当前位置前插入

  I 在当前行首插入

  a 在当前位置后插入

  A 在当前行尾插入

  o 在当前行之后插入一行

  O 在当前行之前插入一行

切换到底行模式：按 :（冒号）；

***

## 2.2 重定向输出>和>>

\> 重定向输出，覆盖原有内容；

\>> 重定向输出，又追加功能；

示例：

​	cat /etc/passwd > a.txt 将输出定向到a.txt中

​	cat /etc/passwd >> a.txt 输出并且追加

​	ifconfig > ifconfig.txt

***

## 2.3 管道

管道是Linux命令中重要的一个概念，其作用是将一个命令的输出用作另一个命令的输入。

示例

​	ls --help | more 分页查询帮助信息

​	ps –ef | grep java 查询名称中包含java的进程

​	ifconfig | more

​	cat index.html | more

​	ps –ef | grep aio-

***

## 2.4 &&命令执行控制

命令之间使用 && 连接，实现逻辑与的功能。 

​	只有在 && 左边的命令返回真（命令返回值 $? == 0），&& 右边的命令才会被执行。 

​	只要有一个命令返回假（命令返回值 $? == 1），后面的命令就不会被执行。

​	mkdir test && cd test

***

## 2.5 网络通讯命令

ifconfig 显示或设置网络设备。

​	ifconfig 显示网络设备

​	ifconfig eth0 up 启用eth0网卡

​	ifconfig eth0 down 停用eth0网卡

ping  探测网络是否通畅。

​	ping 192.168.0.1

netstat 查看网络端口。

​	netstat -an | grep 3306 查询3306端口占用情况

***

##2.6 系统管理命令

date 显示或设置系统时间

​	date 显示当前系统时间

​	date -s “2014-01-01 10:10:10“ 设置系统时间

df 显示磁盘信息

​	df –h 友好显示大小

free 显示内存状态

​	free –m 以mb单位显示内存组昂头

top 显示，管理执行中的程序



clear 清屏幕



ps 正在运行的某个进程的状态

​	ps –ef 查看所有进程

​	ps –ef | grep ssh 查找某一进程



kill 杀掉某一进程

​	kill 2868 杀掉2868编号的进程

​	kill -9 2868 强制杀死进程

 

du 显示目录或文件的大小。

​	du –h 显示当前目录的大小



who 显示目前登入系统的用户信息。



hostname 查看当前主机名

​	修改：vi /etc/sysconfig/network



uname 显示系统信息。

​	uname -a 显示本机详细信息。

​	依次为：内核名称(类别)，主机名，内核版本号，内核版本，内核编译日期，硬件名，处理器类型，硬件平台类型，操作系统名称



# 3 Linux的用户和组 

## 3.1 用户的管理
useradd 添加一个用户
		useradd test 添加test用户
		useradd test -d /home/t1  指定用户home目录 

passwd  设置、修改密码
		passwd test  为test用户设置密码



切换登录：
		ssh -l test -p 22 192.168.19.128



su – 用户名

userdel 删除一个用户
		userdel test 删除test用户(不会删除home目录)
		userdel –r test  删除用户以及home目录

## 3.2 组管理
当在创建一个新用户user时，若没有指定他所属于的组，就建立一个和该用户同名的私有组 

创建用户时也可以指定所在组 

groupadd  创建组
		groupadd public  创建一个名为public的组
		useradd u1 –g public  创建用户指定组 

groupdel 删除组，如果该组有用户成员，必须先删除用户才能删除组。
		groupdel public

## 3.3 id，su命令
【id命令】
功能：查看一个用户的UID和GID 

用法：id [选项]... [用户名]

![img](file:///C:/Users/94307/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

直接使用id
直接使用id 用户名

【su命令】
功能：切换用户

用法：su [选项]... [-] [用户 [参数]... ] 

示例：
		su u1  切换到u1用户
		su - u1 切换到u1用户，并且将环境也切换到u1用户的环境（推荐使用）

***

【账户文件】
		/etc/passwd  用户文件

​		/etc/shadow  密码文件

​		/etc/group  组信息文件

***

【用户文件】
root:x:0:0:root:/root:/bin/bash 

账号名称：						在系统中是唯一的 

用户密码：						此字段存放加密口令 

用户标识码(User ID)： 	系统内部用它来标示用户 

组标识码(Group ID)：  	系统内部用它来标识用户属性 

用户相关信息：				 例如用户全名等 

用户目录：						用户登录系统后所进入的目录 

用户环境:						   用户工作的环境

***

【密码文件】
shadow文件中每条记录用冒号间隔的9个字段组成. 

用户名：					用户登录到系统时使用的名字，而且是惟一的 

口令：  					  存放加密的口令 

最后一次修改时间:    标识从某一时刻起到用户最后一次修改时间 

最大时间间隔:  		  口令保持有效的最大天数，即多少天后必须修改口令 

最小时间间隔：		 再次修改口令之间的最小天数 

警告时间：				 从系统开始警告到口令正式失效的天数

不活动时间：			 口令过期少天后，该账号被禁用 

失效时间：				 指示口令失效的绝对天数(从1970年1月1日开始计算) 

标志：					     未使用 

***

【组文件】
root:x:0: 

组名：用户所属组 

组口令：一般不用 

GID：组ID 

用户列表：属于该组的所有用户



# 4 Linux的权限命令

## 4.1 文件权限

读取权r 写入权w 执行权x 无操作权限-

4：100

2：010

1：001

-rwx rwx r-- —— 774

文件类型 属主权限 属组权限 其他用户

| 属主（user） |      |      | 属组（group） |      |      | 其他用户 |      |      |
| ------------ | ---- | ---- | ------------- | ---- | ---- | -------- | ---- | ---- |
| r            | w    | x    | r             | w    | x    | r        | w    | x    |
| 4            | 2    | 1    | 4             | 2    | 1    | 4        | 2    | 1    |

## 4.2 Linux三种文件类型

普通文件： 包括文本文件、数据文件、可执行的二进制程序文件等。 

目录文件： Linux系统把目录看成是一种特殊的文件，利用它构成文件系统的树型结构。 

设备文件： Linux系统把每一个设备都看成是一个文件

## 4.3 文件类型标识

​	普通文件（-）

​	目录（d）

​	符号链接（l）

​	\* 进入etc可以查看，相当于快捷方式

​	字符设备文件（c）

​	块设备文件（s）

​	套接字（s）

​	命名管道（p）

## 4.4 文件权限管理

chmod 变更文件或目录的权限。

​		chmod 755 a.txt 

​		chmod u=rwx,g=rx,o=rx a.txt

​		chmod 000 a.txt / chmod 777 a.txt

chown 变更文件或目录改文件所属用户和组

​		chown u1:public a.txt ：变更当前的目录或文件的所属用户和组

​		chown -R u1:public dir ：变更目录中的所有的子目录及文件的所属用户和组



# 5 安装jdk1.8

卸载旧文件

​	java –version

​	rpm -qa | grep java

创建安装路径

​	mkdir /usr/local/src/java

打开安装路径

​	cd /usr/local/src/java

将压缩包放到当前路径下，然后解压缩

​	tar -xvf

解压完成后配置环境变量

​	\# set java environment

​	\# jdk1.8.0_281

​	echo "export JAVA_HOME=/usr/local/src/java/jdk1.8.0_281" >> /etc/profile;
​	echo "export JRE_HOME=${JAVA_HOME}/jre" >> /etc/profile;
​	echo "export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib" >> /etc/profile;
​	echo "export  PATH=${JAVA_HOME}/bin:$PATH" >> /etc/profile;

可以打开配置文件看是否配置成功

​	vim /etc/profile

重新加载配置文件：

​	source /etc/profile

ls command not found，vim都不能使用，环境变量配置错误 的解决办法

​	export PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin



# 6 安装mysql5.6

检查是否安装mysql

​	rpm -qa | grep mysql

删除mysql

​	yum remove mysql mysql-server mysql-libs mysql-server;

​	find / -name mysql 将找到的相关东西delete掉；

创建安装目录并且打开安装目录

​	mkdir /usr/local/src/mysql

​	cd /usr/local/src/mysql

下载mysql安装包

​	wget

或者将利用xftp将安装包上传到安装目录

解压缩安装文件

​	tar -xvf

安装server
	 rpm -ivh MySQL-server-5.6.22-1.el6.i686.rpm

安装client

​	rpm -ivh MySQL-client-5.6.22-1.el6.i686.rpm

切换到主目录

​	cd ~

查询mysq服务运行状态

​	service mysqld status

启动mysql

​	service mysqld start

利用root账户登录mysql

​	mysql -uroot -p（password）

修改root密码

​	set password = password('root')

系统启动时自动启动mysql服务

​	加入到系统服务：

​		chkconfig --add mysql

​	自动启动：

​		chkconfig mysql on

​	查询列表：

​		chkconfig

开启远程访问

​	firewall-cmd --zone=public --add-port=3306/tcp --permanent

![](C:\Users\94307\AppData\Roaming\Typora\typora-user-images\image-20210130203505472.png)

​	firewall-cmd --reload

​	firewall-cmd --query-port=8080/tcp

![image-20210130203518301](C:\Users\94307\AppData\Roaming\Typora\typora-user-images\image-20210130203518301.png)

阿里云服务器：n：JavaWebgyx  	u：root 	p：Aliyungyx@25007

在navicat中开启远程连接

![image-20210131015111142](C:\Users\94307\AppData\Roaming\Typora\typora-user-images\image-20210131015111142.png)

# 7 创建用户 

一般情况下，发布应用程序都不是使用root用户的，需要创建一个普通用户来发布程序； 

创建ucenter用户：

​	useradd gyx -d /ucenter

设置密码：

​	passwd gyx （密码 gyx1202）

切换用户：

​	su - gyx



# 8 安装tomcat

## 创建ucenter用户

一般情况下，发布应用程序都不是使用root用户的，需要创建一个普通用户来发布程序； 

创建ucenter用户：

​	useradd -d /ucenter ucenter

设置密码：

​	passwd ucenter （密码 ucenter）

切换用户：

​	su - ucenter

## 安装tomcat

创建web目录

​	mkdir /ucenter/web

利用xftp上传安装包

​	apache-tomcat-8.5.61.tar.gz

在web目录下解压

​	tar -xvf apache-tomcat-8.5.61.tar.gz

重命名当前文件夹

​	mv apache-tomcat-8.5.61 gyx-javaweb

启动tomcat

​	cd itcast-usermanage/bin/

​	./startup.sh 或者 sh startup.sh

切换到root用户打开8080端口

​	firewall-cmd --zone=public --add-port=8080/tcp --permanent

​	firewall-cmd --reload

​	firewall-cmd --query-port=8080/tcp

在服务器控制台添加安全组规则，开放8080端口![image-20210130201529375](C:\Users\94307\AppData\Roaming\Typora\typora-user-images\image-20210130201529375.png)

在浏览器中输入公网IP地址+8080，如果跳出如下页面，则配置成功	![image-20210130201640959](C:\Users\94307\AppData\Roaming\Typora\typora-user-images\image-20210130201640959.png)



# 9 nginx

