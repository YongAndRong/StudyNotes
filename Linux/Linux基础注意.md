## linux基础命令注意点滴
* `开发接口标准 `   
&ensp;&ensp;&ensp;&ensp;ABI:Application Binary Interface  
&ensp;&ensp;&ensp;&ensp;ABI描述了应用程序与OS之间的底层接口，允许编译好的目标代码在使用兼容ABI的系统中无需改动就能运行

&ensp;&ensp;&ensp;&ensp;API：Application programming Interface
&ensp;&ensp;&ensp;&ensp;API定义了源代码和库之间的接口，因此同样的源代码可以在支持这个API的任何系统中编译  

&ensp;&ensp;&ensp;&ensp;POSIX：Portable Operating System Interface  
&ensp;&ensp;&ensp;&ensp;POSIX兼容的程序可以在其他的POSIX操作系统编译执行  

* `用户空间和内核空间 ` 
> 示例  
```python
str = 'www.maagedu.com'   #用户空间
x += 10                   #用户空间
file.write(str)           #内核空间
y = x + 200               #用户空间
#第一行、第二行都是简单的赋值运算，在用户空间执行。
#第三行需要写入文件，就要切换到内核空间，因为用户不能直接写文件，必须内核安排
#第四行又是赋值运算，就又切换回用户空间
#这里可以关注下，程序中需要优化的一点，就是不要让程序经常性的在用户空间和内核空间切换，因为切换是需要花费资源的。。。有代价！
```  

* `命令提示符`  
    显示提示符格式  
    [root@localhost ~]#echo $PS1  
    修改提示符格式  
    PS1="\[\e[1;5;41;33m\][\u@\h \W]\\$\[\e[0m\]"  
    PS1="\[\e[1;32m\][\[\e[0m\]\t \[\e[1;33m\]\u\[\e[36m\]@\h\[\e[1;31m\] \W\[\e[1;32m\]]\[\e[0m\]\\$"    

    \e \033   
    \u 当前用户   
    \h 主机名简称   
    \H 主机名  
    \w 当前工作目录   
    \W 当前工作目录基名  
    \t 24小时时间格式   
    \T 12小时时间格式  
    \! 命令历史数        \# 开机后命令历史数  

* ##  可执行命令  
shell中有两种可执行的命令：内部命令、外部命令  
enable 可查看所有的内部命令  
enable -n  查看所有被禁用的内部命令  
enable -n CMD    禁用内部命令  
enable CMD   启用内部命令  
> 示例  
```bash
~]# enable
enable .     #记得什么用么？source
enable :     #这个也是命令哦
enable [     #记得这个是干什么的么？
enable alias
enable bg
enable bind
enable break
enable builtin
enable caller
enable cd
enable command
...

[root@centos7 home]# enable -n cd     #禁用掉cd命令
[root@centos7 home]# cd /data         #无法使用了
[root@centos7 home]# enable -n        #查看禁用列表，所以在禁用列表 
enable -n cd                          #里找到了刚才禁用的cd命令
[root@centos7 home]# enable cd        #重新启用cd命令
[root@centos7 home]# cd /data         #可以继续使用了
[root@centos7 data]# pwd
/data
```  
> `type COMMAND`    #可以查看命令是内部命令还是外部命令  

* ## hash 缓存表  
&ensp;&ensp;&ensp;&ensp;系统初始hash表为空，当外部命令执行时，默认会从PATH路径下寻找该命令，找到后会将这条命令的路径记录到hash表中，当再次使用该命令时，shell解释器首先会查看hash表，存在将执行之，如果不存在，将会去PATH路径下寻找。利用hash缓存表可大大提高命令的调用速率
> `hash -r #清除缓存`  
> `hash  显示hash缓存`  


* ## 命令别名 alias  
 撤销别名unalias  
> unalias -a   #取消所有的别名  
> 如果别名同原命令同名，如果要执行原命令，可使用如下方法：  
> 1. 在命令前加 '\\'       # \ALIASNAME  
> 2. 用引号将命令引起来    # 'ALIASNAME'  
> 3. 直接使用命令的绝对路径  

##  快捷键
ctrl + c   #强制取消命令的执行  
ctrl + d   #结束命令的执行  //这个要温和一点点

##  时间和日期 
```bash
date 命令  
date +%s   //显示从1970-1-1 到现在有多少秒  
date -s ‘string’  //string是日期或时间，修改到后面的string.  
~]# date -s '2018-03-12 12:30:12'  
Mon Mar 12 12:30:12 CST 2018
~]# date -s '2017-01-22'   #这种修改日期的会将时间默认设置为0:0:0
Sun Jan 22 00:00:00 CST 2017 
~]# date -s '1 year'       #增加一年
Tue Mar 12 12:31:25 CST 2019 

date -d @SECONDS   #seconds为从1979年到你要改到的时间的秒数
```
```bash
timedatactl  查看时间时区
~]# timedatectl status
      Local time: Tue 2019-03-12 12:35:29 CST
  Universal time: Tue 2019-03-12 04:35:29 UTC
        RTC time: Thu 2019-03-21 00:37:01
       Time zone: Asia/Shanghai (CST, +0800)
     NTP enabled: no
NTP synchronized: no
 RTC in local TZ: no
      DST active: n/a
```
####  简单命令
* screen 命令  
screen -S  [SESSION]   #创建新会话  
screen -ls             #显示所有已经打开的screen会话(貌似只能同用户查看)  
screen -x [SESSION]    #加入screen会话  
exit                   #退出会话  
ctrl a ,d              #临时剥离会话，以便离开当前会话做点其他的
screen -r  [SESSION]   #恢复某会话，如果只有一个会话可以不用加SESSION

* 命令扩展{}  
```bash
[root@centos7 ~]# echo {1..10}
1 2 3 4 5 6 7 8 9 10
[root@centos7 ~]# echo {a..z}
a b c d e f g h i j k l m n o p q r s t u v w x y z
[root@centos7 ~]# echo {0..10..2}   #这个可以哦
0 2 4 6 8 10
```
* 命令行历史  
`ctrl + r #在命令历史中搜索命令`  
`ctrl + g #从历史搜索模式退出`

* makewhatis  和  mandb    后者只在centos7上有
* ]# ls  ~-/DIR/FILENAME    #查看上一次工作目录里的文件  ~- 上一次的工作目录  

### 文件通配符
```bash
#第一部分
* 匹配0、多个字符
？ 匹配任何单个字符
~ 当前用户家目录
~USERNAME 用户USERNAME的家目录
~+ 当前工作目录
~- 前一个工作目录
[0-9] 匹配数字范围
[a-z] 字母
[A-Z] 
[^] 匹配列表中以外的字符
```
> 示例 
```bash 
[root@centos7 test]# ll f[a-d].txt  #注意最后一个D文件未显示
-rw-r--r--. 1 root root 0 Jan 22 01:03 fa.txt
-rw-r--r--. 1 root root 0 Jan 22 01:03 fA.txt
-rw-r--r--. 1 root root 0 Jan 22 01:03 fb.txt
-rw-r--r--. 1 root root 0 Jan 22 01:03 fB.txt
-rw-r--r--. 1 root root 0 Jan 22 01:03 fc.txt
-rw-r--r--. 1 root root 0 Jan 22 01:03 fC.txt
-rw-r--r--. 1 root root 0 Jan 22 01:03 fd.txt
[root@centos7 test]# ll f[A-D].txt  #注意最前一个a文件未显示
-rw-r--r--. 1 root root 0 Jan 22 01:03 fA.txt
-rw-r--r--. 1 root root 0 Jan 22 01:03 fb.txt
-rw-r--r--. 1 root root 0 Jan 22 01:03 fB.txt
-rw-r--r--. 1 root root 0 Jan 22 01:03 fc.txt
-rw-r--r--. 1 root root 0 Jan 22 01:03 fC.txt
-rw-r--r--. 1 root root 0 Jan 22 01:03 fd.txt
-rw-r--r--. 1 root root 0 Jan 22 01:03 fD.txt
#顺序为aAbBcCdD小写字母和大写字母交叉的
```
```
#第二部分  man 7 glob
[:digit:]   任意数字，相当于0-9
[:lower:]   任意小写字母
[:upper:]   任意大写字母
[:alpha:]   任意大小写字母
[:alnum:]   任意数字或字母
[:punct:]   标点符号
[:blank:]   水平空白字符
[:space:]   水平或垂直空白字符
[:print:]   可打印字符
[:cntrl:]   控制(非打印)字符
[:graph:]   图形字符
[:xdigit:]  十六进制字符
```

```bash
]# df | tr -s ' '   //tr -s ' '将相邻的空格压缩成一个空格
Filesystem 1K-blocks Used Available Use% Mounted on
/dev/sda2 104806400 3943208 100863192 4% /
devtmpfs 915768 0 915768 0% /dev
tmpfs 931612 0 931612 0% /dev/shm
tmpfs 931612 18968 912644 3% /run
tmpfs 931612 0 931612 0% /sys/fs/cgroup
/dev/sda3 52403200 33060 52370140 1% /data
/dev/sda1 1038336 178100 860236 18% /boot
tmpfs 186324 4 186320 1% /run/user/42
tmpfs 186324 28 186296 1% /run/user/0
/dev/sr0 10491772 10491772 0 100% /run/media/root/CentOS 7 x86_64
/dev/loop0 10491772 10491772 0 100% /mnt/dvd
```
> ` # echo f{1..9999999} | xargs touch  可以创建大数量的文件`  
直接touch是不会成功的  
> `删除大文件时，最好不要直接使用rm   而是先使用>填充0 然后使用rm删除`

 ### 软连接  
```bash
[root@centos7 data]# ln -s f1 /root/f1
[root@centos7 data]# ll /root/f1
lrwxrwxrwx. 1 root root 2 Jan 22 02:24 /root/f1 -> f1   #错误的
[root@centos7 data]# ln -s ../data/f1 /root/ff1
[root@centos7 data]# ll /root/ff1
lrwxrwxrwx. 1 root root 10 Jan 22 02:24 /root/ff1 -> ../data/f1  #正确的
#注意建立软连接时，使用相对路径时，是相对于你要针对的文件建立软连接，而不是针对当前目录建立软连接，后者会错
```
> 软连接到目录的注意
```bash
[root@centos7 data]# ln -s dir dir2
[root@centos7 data]# rm -rf dir2   #这种只是删除软连接目录dir2
[root@centos7 data]# ls dir
a  b  c
[root@centos7 data]# ln -s dir dir2 
[root@centos7 data]# rm -rf dir2/  # 这种删除的是连接的原始目录里的文件，但是软连接目录未删，还是存在的
[root@centos7 data]# ls dir
[root@centos7 data]# ll
total 0
drwxr-xr-x. 2 root root 6 Jan 22 02:30 dir
lrwxrwxrwx. 1 root root 3 Jan 22 02:30 dir2 -> dir

#现在的centos7上的/bin 目录连接到/usr/bin的，如果需要删除/bin目录时，千万别输入/bin/ 这样的，因为rm -rf /bin/ 的话，会将/usr/bin 下的文件全删掉,最后的'/' 千万别带！！！
```

```bash
#批量计算，将需要计算的表达式存在文件中，然后用重定向输入
[root@centos7 data]# vim bc.txt
[root@centos7 data]# bc <bc.txt
6
5
2
[root@centos7 data]# cat bc.txt
2*3
2+3
4/2
```
```
> 运用管道时，需要注意的是，前一个命令需要有标准输出，后一个命令需要有标准输入
> 错误的输出也是传不到下一个命令的，所以要求是正确的标准输出到下一个命令

合并标准输出和错误输出为同一个数据流进行重定向
 &> 覆盖重定向
 &>> 追加重定向
COMMAND > /path/to/file.out 2>&1 （顺序很重要）
COMMAND >> /path/to/file.out 2>&1
示例：
>ls /data /error 2>all2.log >&2  #这个也是可以的，要学会举一反三哦  
>ls /data /error >all.log 2>&1
```

### COMMAND | tee -a 
```bash
#关于管道使用tee命令的覆盖和追加说明
[root@centos7 data]# cat /etc/issue | tee tee.log
\S
Kernel \r on an \m

[root@centos7 data]# cat tee.log
\S
Kernel \r on an \m

[root@centos7 data]# who |tee tee.log    #这样子会直接覆盖掉原来tee.log 的内容
root     :0           2019-03-19 19:56 (:0)
root     pts/0        2019-03-19 19:56 (:0)
root     pts/1        2019-03-21 08:15 (192.168.20.1)
root     pts/2        2019-03-12 12:37 (192.168.20.1)
stephen  :1           2017-01-22 01:38 (:1)
[root@centos7 data]# cat tee.log 
root     :0           2019-03-19 19:56 (:0)
root     pts/0        2019-03-19 19:56 (:0)
root     pts/1        2019-03-21 08:15 (192.168.20.1)
root     pts/2        2019-03-12 12:37 (192.168.20.1)
stephen  :1           2017-01-22 01:38 (:1)
[root@centos7 data]# hostname | tee -a tee.log   #加-a参数可以在tee.log中进行追加内容,避免覆盖文件中的内容
centos7.localdomain
[root@centos7 data]# cat tee.log 
root     :0           2019-03-19 19:56 (:0)
root     pts/0        2019-03-19 19:56 (:0)
root     pts/1        2019-03-21 08:15 (192.168.20.1)
root     pts/2        2019-03-12 12:37 (192.168.20.1)
stephen  :1           2017-01-22 01:38 (:1)
centos7.localdomain
```

### rpm的用法补充
> 查看二进制程序所依赖的库文件  
`ldd /PATH/TO/BINARY_FILE`  
```bash
]# ldd /bin/ls
	linux-vdso.so.1 =>  (0x00007ffd00d47000)
	libselinux.so.1 => /lib64/libselinux.so.1 (0x00007fc23d4ac000)
	libcap.so.2 => /lib64/libcap.so.2 (0x00007fc23d2a7000)
	libacl.so.1 => /lib64/libacl.so.1 (0x00007fc23d09e000)
```


###  `yum history`  
#查看安装历史
```bash
]# yum history
Loaded plugins: fastestmirror, langpacks
ID     | Login user               | Date and time    | Action(s)      | Altered
-------------------------------------------------------------------------------
     7 | root <root>              | 2019-03-22 20:40 | Install        |    1   
     6 | root <root>              | 2019-03-22 15:39 | Install        |    1   
     5 | root <root>              | 2019-03-22 15:38 | Install        |    5   
     4 | root <root>              | 2019-03-22 14:19 | Install        |    5  <
     3 | root <root>              | 2019-03-19 20:22 | Install        |    1 > 
     2 | root <root>              | 2019-03-18 21:57 | Install        |    1   
     1 | System <unset>           | 2019-03-19 05:04 | Install        | 1382   
history list
```

~]#yum history info 2  #查看ID为2这个安装历史，当时做了什么  
#这里查看的是第五个当时安装了什么，如果后悔了，不要这次安装的了可以按下面的做
```bash
[root@centos7 yum.repos.d]# yum history info 5
Loaded plugins: fastestmirror, langpacks
Transaction ID : 5
Begin time     : Fri Mar 22 15:38:30 2019
Begin rpmdb    : 1390:c9a30b04f18bd8335037bf01aa1b69b116d92203
End time       :            15:38:39 2019 (9 seconds)
End rpmdb      : 1395:cddac2445f26137d1634685456d5d9cf413fff3f
User           : root <root>
Return-Code    : Success
Command Line   : install gcc
Transaction performed with:
    Installed     rpm-4.11.3-35.el7.x86_64                      @anaconda
    Installed     yum-3.4.3-161.el7.centos.noarch               @anaconda
    Installed     yum-plugin-fastestmirror-1.1.31-50.el7.noarch @anaconda
Packages Altered:
    Dep-Install cpp-4.8.5-36.el7.x86_64              @iso
    Install     gcc-4.8.5-36.el7.x86_64              @iso
    Dep-Install glibc-devel-2.17-260.el7.x86_64      @iso
    Dep-Install glibc-headers-2.17-260.el7.x86_64    @iso
    Dep-Install kernel-headers-3.10.0-957.el7.x86_64 @iso
history info

]# yum history undo 5  #后悔了，这种操作会把依赖的库也卸载掉
Loaded plugins: fastestmirror, langpacks
Undoing transaction 5, from Fri Mar 22 15:38:30 2019
    Dep-Install cpp-4.8.5-36.el7.x86_64              @iso
    Install     gcc-4.8.5-36.el7.x86_64              @iso
    Dep-Install glibc-devel-2.17-260.el7.x86_64      @iso
    Dep-Install glibc-headers-2.17-260.el7.x86_64    @iso
    Dep-Install kernel-headers-3.10.0-957.el7.x86_64 @iso
Resolving Dependencies
--> Running transaction check
---> Package cpp.x86_64 0:4.8.5-36.el7 will be erased
---> Package gcc.x86_64 0:4.8.5-36.el7 will be erased
---> Package glibc-devel.x86_64 0:2.17-260.el7 will be erased
---> Package glibc-headers.x86_64 0:2.17-260.el7 will be erased
---> Package kernel-headers.x86_64 0:3.10.0-957.el7 will be erased
--> Finished Dependency Resolution
.....等等....

#如果刚才撤销错了，又后悔了 可以这样做
#yum history redo 5   #这样的话就有安装了刚才的包

```
