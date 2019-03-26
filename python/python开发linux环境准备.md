## python开发环境linux下搭建
### 软件准备
*  centos 6.5
*  python 3.6.6 和 python 3.5.3
*  虚拟机(安装省略)
### 系统准备  
*   1、虚拟机上最小化安装centos 6.5系统。关闭selinux、iptables   
*   2、配置本地yum源 等  
注意：  
    1、虚拟机中网络适配器采用NAT模式，python程序部署需要连接外网  
    2、/etc/sysconfig/network-scripts/ifcfg-eth0  
        BOOTPROTO=static  
        ONBOOT=yes  
        #设置ip地址、掩码、网关、DNS等即可  
    3、rm -rf /etc/udev/rules.d/70-persistent-net.rules #只有redhat系需要删除这个文件  
    4、重启系统并做快照  
### 开发环境-----Pyenv  
python多版本管理工具  
&ensp;&ensp;&ensp;&ensp;管理python解释器  
&ensp;&ensp;&ensp;&ensp;管理python多版本  
&ensp;&ensp;&ensp;&ensp;管理python的虚拟环境  
官网 https://github.com/pyenv/pyenv  
不支持windows，原因 https://github.com/pyenv/pyenv/issues/6  
### pyenv安装方式  
git安装  
1、安装git  
`#yum install git -y  `  
2、安装python编译依赖  
`#yum install gcc make patch gdbm-devel openssl-devel sqlite-devel readline-devel zlib-devel`  
3、创建用户python(建议使用一个权限小的用户进行程序开发)  
`~]#useradd python`  
`~]#echo python | passwd --stdin python`  
4、使用python用户登录后安装pyenv
pyenv官网 https://github.com/pyenv/pyenv  
pyenv-installer 插件 https://github.com/pyenv/pyenv-installer  
`~]#curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash`   
下载的是一个pyenv-installer的shell脚本  
注意：  
&ensp;&ensp;&ensp;&ensp;1、在 `https://github.com/pyenv/pyenv-installer` 有安装文档  
&ensp;&ensp;&ensp;&ensp;2、如果curl出现 `curl: (35) SSL connect error`,是nss版本低的问题，更新它。此时可能需要配置一个较新包的yum源
```
[update]
name=centos 6 update
baseurl=https://mirrors.aliyun.com/centos/6/os/x86_64/
gpgcheck=0
```
然后更新nss  
`~]#yum update nss`  
`~]#curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash` 
再次执行上面这句命令后即可完成安装，最后根据提示需要更新下~/.bashrc，将下面代码追加到文件末尾即可  
```
export PATH="/home/python/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```
`~]#source ~/.bashrc`    #使该文件马上生效，这样在用户启动的时候，会执行.bashrc中的脚本，就可以启动pyenv   
安装好的pyenv就在 `~/.pyenv` 目录中  
`pyenv-update` 有时也要用，因为pyenv如果是很久前安装的话，它就不会管理到python的新版本，使用  `pyenv install -l` 就看不到的，这时候如果需要新python版本，就需要升级下pyenv了  
```bash
pyenv help install
pyenv install -l #查看当前可以安装那些python版本
pyenv install 3.6.6 #安装python 3.6.6版本
```  
### pyenv的本地安装  
由于直接安装python解释器的话，会跑到python官网去下载安装包，就会很慢，这里我们可以将需要安装的python安装包放在python家目录下的~/.pyenv/cache/ 这个目录下，需要注意的是得将所有格式xz、gz、tgz的python安装压缩包都放在cache目录下，以便他自己随机选择安装包  
```bash
[python@localhost cache]$ ll
total 117104
-rw-r--r-- 1 python python 20832003 Mar 26 15:49 Python-3.5.3.tar.gz
-rw-r--r-- 1 python python 15213396 Mar 26 15:49 Python-3.5.3.tar.xz
-rw-r--r-- 1 python python 20656090 Mar 26 15:49 Python-3.5.3.tgz
-rw-r--r-- 1 python python 23117814 Mar 26 15:49 Python-3.6.6.tar.gz
-rw-r--r-- 1 python python 17156744 Mar 26 15:49 Python-3.6.6.tar.xz
-rw-r--r-- 1 python python 22930752 Mar 26 15:49 Python-3.6.6.tgz
[python@localhost ~]$ pyenv install 3.6.6 -v   #安装 python3.6.6
[python@localhost ~]$ pyenv install 3.5.3 -v   #安装python 3.5.3
#在哪个目录安装都是可以的，只要是python用户安装，且pyenv只有python这个用户可用
#此时运行如下命令会发现已经将python3.6.6 和3.5.3都已经安装上了
[python@localhost cache]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.5.3
  3.6.6

#但是默认还是使用的system的
[python@localhost cache]$ python -V
Python 2.6.6

#看看帮助文档
[python@localhost cache]$ pyenv help 
Usage: pyenv <command> [<args>]

Some useful pyenv commands are:
   commands    List all available pyenv commands
   local       Set or show the local application-specific Python version
   global      Set or show the global Python version
   shell       Set or show the shell-specific Python version
   install     Install a Python version using python-build
   uninstall   Uninstall a specific Python version
   rehash      Rehash pyenv shims (run this after installing executables)
   version     Show the current Python version and its origin
   versions    List all Python versions available to pyenv
   which       Display the full path to an executable
   whence      List all Python versions that contain the given executable

See `pyenv help <command> ` for information on a specific command.
For full documentation, see: https://github.com/pyenv/pyenv#readme
#------------------------------------------------------------------------------------
[python@localhost cache]$ pyenv global 3.6.6  #将全局改成python 3.6.6，这种操作影响的是当前用户所有的python配置，对其他用户没影响的，因为pyenv没有在其他用户下配置过
[python@localhost cache]$ pyenv versions
  system
  3.5.3
* 3.6.6 (set by /home/python/.pyenv/version)  
[python@localhost cache]$ python -V  #但是查看当前python版本时，却还是没有改变的，这个时候需要重新登录或者切换下当前环境
Python 2.6.6
[python@localhost cache]$ pyenv global system   #切换到system的python版本
[python@localhost cache]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.5.3
  3.6.6

[python@localhost cache]$ pyenv shell 3.5.3  #使用shell的话，只跟当前shell有关，退出当前shell，python版本就回到全局的python版本了，只作用于当前会话
[python@localhost cache]$ pyenv versions
  system
* 3.5.3 (set by PYENV_VERSION environment variable)
  3.6.6

#以上两种方法都有弊端，这个时候我们可以使用local设置本地的，首先在家目录下新建一个项目目录
[python@localhost ~]$ mkdir -pv projects/web
[python@localhost web]$ pwd
/home/python/projects/web
[python@localhost web]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.5.3
  3.6.6
[python@localhost web]$ pyenv local 3.5.3  #将本地切换到python3.5.3
[python@localhost web]$ python -V
Python 3.5.3
[python@localhost web]$ cd ..    #回到父目录时，python的版本却是2.6.6了
[python@localhost projects]$ python -V
Python 2.6.6
[python@localhost projects]$ cd web
[python@localhost web]$ python -V  #所以local影响的是这个目录
Python 3.5.3
#在这个目录的子目录下是可以继承这个python版本的，如果不想要父目录的python版本，可以另外在子目录local一下
#这里也有一个弊端，就是在使用pip安装第三方库的时候，会对全局的3.5.3版本造成影响，所以接下来我们需要使用虚拟环境的
[python@localhost web]$ ls -a   #在这个目录下还有一个隐藏文件，而里面的内容就是当前目录下pyenv管理的python版本了，通过该这个文件的内容，也可以更改pyenv管理的python版本
.  ..  .python-version
[python@localhost web]$ cat .python-version 
3.5.3
```
`pyenv local --unset` 取消local设置，取消一般不用，重新换就可以了，另外还可以改隐藏文件的内容以便指定版本

#### virtualenv 虚拟环境设置
为什么要使用虚拟环境？  
因为刚才使用的python环境都是一个公共的空间，如果多个项目使用不同的pytho版本开发，或者使用不同的python版本部署运行，或者使用同样的版本开发，但不同项目使用了不同版本的库，等等这些问题都会带来冲突，最好的解决办法就是每一个项目独立运行自己的“独立环境”中。
使用插件，在plugins/pyenv-virtualenv 中
$pyenv virtualenv 3.6.6 mag366

```bash
[python@localhost web]$ pyenv virtualenv 3.6.6 mag366
Looking in links: /tmp/tmpq5s594zd
Requirement already satisfied: setuptools in /home/python/.pyenv/versions/3.6.6/envs/mag366/lib/python3.6/site-packages (39.0.1)
Requirement already satisfied: pip in /home/python/.pyenv/versions/3.6.6/envs/mag366/lib/python3.6/site-packages (10.0.1)
[python@localhost web]$ pyenv versions
* system (set by /home/python/projects/web/.python-version)
  3.5.3
  3.6.6
  3.6.6/envs/mag366
  mag366
[python@localhost web]$ pyenv local mag366
(mag366) [python@localhost web]$ python -V
Python 3.6.6
(mag366) [python@localhost web]$ cd ..
[python@localhost projects]$ python -V
Python 2.6.6
[python@localhost projects]$ mkdir test
[python@localhost projects]$ cd test
[python@localhost test]$ python -V
Python 2.6.6
[python@localhost test]$ pyenv local 3.6.6
[python@localhost test]$ cd ../web
(mag366) [python@localhost web]$ pip list
Package    Version
---------- -------
pip        10.0.1 
redis      3.2.1  
setuptools 39.0.1 
(mag366) [python@localhost web]$ cd ../test
[python@localhost test]$ python -V
Python 3.6.6
[python@localhost test]$ pip list
Package    Version
---------- -------
pip        10.0.1 
setuptools 39.0.1 
#看看，test目录下和web目录下的环境互不影响
```

#### pip通用配置  
pip是python的包管理工具，3.x版本直接带了，可以直接使用。和yum一样为了使用国内镜像，配置如下：
LInux系统，在家目录下
```bash
[python@localhost ~]$ mkdir .pip
[python@localhost ~]$ vi .pip/pip.conf
[global]
index-url=https://mirrors.aliyun.com/pypi/simple/
trusted-host=mirrors.aliyun.com
#在此  我们去 /home/python/projects/test下安装ipython
[python@localhost ~]$ cd -
/home/python/projects/test
[python@localhost test]$ pip install ipython
...
[python@localhost test]$ pip list
Package          Version
---------------- -------
backcall         0.1.0  
decorator        4.4.0  
ipython          7.4.0  
ipython-genutils 0.2.0  
jedi             0.13.3 
parso            0.3.4  
pexpect          4.6.0  
pickleshare      0.7.5  
pip              10.0.1 
prompt-toolkit   2.0.9  
ptyprocess       0.6.0  
Pygments         2.3.1  
setuptools       39.0.1 
six              1.12.0 
traitlets        4.3.2  
wcwidth          0.1.7   #可以看到 现在多了很多第三方的东西了
#这里我们有两个目录，每个目录下都有一个python的版本，但是在web下无法运行ipython的，因为它没有这些包，如果是在实际的开发项目中时，我们要把这些代码和第三方包发布到线上，我们就得把这些打包给运维，让其部署环境，可以这样做：
[python@localhost test]$ pip freeze > requirements   #冻结
[python@localhost test]$ pip freeze > requirements   #查看下内容
You are using pip version 10.0.1, however version 19.0.3 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
[python@localhost test]$ cat requirements 
backcall==0.1.0
decorator==4.4.0
ipython==7.4.0
ipython-genutils==0.2.0
jedi==0.13.3
parso==0.3.4
pexpect==4.6.0
pickleshare==0.7.5
prompt-toolkit==2.0.9
ptyprocess==0.6.0
Pygments==2.3.1
six==1.12.0
traitlets==4.3.2
wcwidth==0.1.
[python@localhost test]$ cd ../web
(mag366) [python@localhost web]$ pip install -r ../test/requirements
(mag366) [python@localhost web]$ pip list  # 这时可以看到刚才冻结的包都已经安装到web目录下了
(mag366) [python@localhost web]$ pip install jupyter  #在虚拟机环境下安装一个jupyter
(mag366) [python@localhost web]$ jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser  #运行jupyter即可
```
另外我们刚才安装的redis、ipython、jupyter等安装包存放在哪里呢？
```bash
[python@localhost versions]$ pwd
/home/python/.pyenv/versions       #这个目录下
[python@localhost versions]$ ls
3.5.3  3.6.6  mag366               #因为只安装了两个python版本，所有这里有两个版本的目录，和一个虚拟环境的
[python@localhost mag366]$ pwd 
/home/python/.pyenv/versions/3.6.6/envs/mag366  #去这里看看
[python@localhost mag366]$ cd lib
[python@localhost lib]$ ls
python3.6
[python@localhost lib]$ cd python3.6/
[python@localhost python3.6]$ ls
site-packages
[python@localhost python3.6]$ cd site-packages/
[python@localhost site-packages]$ ls
attr                                parso
attrs-19.1.0.dist-info              parso-0.3.4.dist-info
backcall                            pexpect
backcall-0.1.0-py3.6.egg-info       pexpect-4.6.0.dist-info
bleach                              pickleshare-0.7.5.dist-info
... #可以看到很多包都在这里了
/home/python/.pyenv/versions/3.5.3/lib/python3.5/site-packages #全局的包在这里
/home/python/.pyenv/versions/3.6.6/lib/python3.6/site-packages
```
### ipython  
ipython是增强的交互式python命令行工具
### jupyter  
jupyter是基于web的交互式笔记本，其中可以非常方便的使用python。
安装jupyter，也会依赖安装ipython的。
