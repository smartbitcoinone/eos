# SBC源代码编译指南

### 1、系统环境准备
  - 操作系统：Ubuntu 16.04.4 LTS 
  - 系统内存：至少8G
  - 磁盘空间：至少20G
  
### 2、软件环境准备
(1)、国内阿里源替换：(可选)

```
testsbcbuild@ubuntu:~$ sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak  #备份
testsbcbuild@ubuntu:~$ sudo vi /etc/apt/sources.list  #删除所有替换为16.04LTS阿里源
/////////////////////////////////////////////////////////////////////////////////////////////////
deb-src http://archive.ubuntu.com/ubuntu xenial main restricted 
deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted multiverse universe 
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted multiverse universe deb http://mirrors.aliyun.com/ubuntu/ xenial universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
deb http://mirrors.aliyun.com/ubuntu/ xenial multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb http://archive.canonical.com/ubuntu xenial partner
deb-src http://archive.canonical.com/ubuntu xenial partner
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted multiverse universe 
deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-security multiverse
/////////////////////////////////////////////////////////////////////////////////////////////////
testsbcbuild@ubuntu:~$ sudo apt-get update
```





(2)、源代码获取及构建

> GIT安装：sudo apt install git

SBC源代码克隆：

```
testsbcbuild@ubuntu:~$ pwd  #查看当前路径
testsbcbuild@ubuntu:~$ mkdir sbc-project #在当前路径下新建文件夹
testsbcbuild@ubuntu:~$ sudo git clone https://github.com/smartbitcoinone/sbc --recursive
testsbcbuild@ubuntu:~/sbc-project$ cd sbc
testsbcbuild@ubuntu:~/sbc-project/sbc$ ./eosio_build.sh 
```
	
```  
Beginning build version: 1.2
	Wed Jul 18 12:49:49 UTC 2018
	User: testsbcbuild
	git head id: 71420a4d65b5e0cf644c2a4b0fda5bf6bd1d84c7
	Current branch: master
	ARCHITECTURE: Linux
	OS name: Ubuntu
	OS Version: 16.04
	CPU speed: 2903.994Mhz
	CPU cores: 1
	Physical Memory: 7954 Mgb
	Disk install: /dev/sda1
	Disk space total: 11G
	Disk space available: 6G
	You must have at least 20GB of available storage to install EOSIO.
	Exiting now.
#以上信息说明空间不足20G，如果内存不够7G也会报相应内存不足的问题。

testsbcbuild@ubuntu:~/sbc-project/sbc$ ./eosio_build.sh 

Beginning build version: 1.2
	Wed Jul 18 13:10:35 UTC 2018
	User: testsbcbuild
	git head id: 71420a4d65b5e0cf644c2a4b0fda5bf6bd1d84c7
	Current branch: master
	ARCHITECTURE: Linux
	OS name: Ubuntu
	OS Version: 16.04
	CPU speed: 2903.994Mhz
	CPU cores: 1
	Physical Memory: 7954 Mgb
	Disk install: /dev/sda1
	Disk space total: 76G
	Disk space available: 68G
	Checking for installed dependencies.
	Package clang-4.0  NOT  found.
	Package lldb-4.0  NOT  found.
	Package libclang-4.0-dev  NOT  found.
	Package cmake  NOT  found.
	Package make found.
	Package automake  NOT  found.
	Package libbz2-dev  NOT  found.
	Package libssl-dev  NOT  found.
	Package libgmp3-dev  NOT  found.
	Package autotools-dev  NOT  found.
	Package build-essential found.
	Package libicu-dev  NOT  found.
	Package python2.7-dev  NOT  found.
	Package python3-dev  NOT  found.
	Package autoconf  NOT  found.
	Package libtool  NOT  found.
	Package curl  NOT  found.
	Package zlib1g-dev  NOT  found.
	Package doxygen  NOT  found.
	Package graphviz  NOT  found.

	The following dependencies are required to install EOSIO.

	1. clang-4.0
	2. lldb-4.0
	3. libclang-4.0-dev
	4. cmake
	5. automake
	6. libbz2-dev
	7. libssl-dev
	8. libgmp3-dev
	9. autotools-dev
	10. libicu-dev
	11. python2.7-dev
	12. python3-dev
	13. autoconf
	14. libtool
	15. curl
	16. zlib1g-dev
	17. doxygen
	18. graphviz
	Do you wish to install these packages?
1) Yes
2) No
#? 1 
######此处需要输入数字1或2进行安装依赖包######
如果中间下载断开重新执行构建命令：
testsbcbuild@ubuntu:~/sbc-project/sbc$ ./eosio_build.sh 
//////////////////////////////////////////////////////////////////////////////////////////////////
```

如果因为网络问题MongoDB 3.6.3不能下载安装，请尝试以下方法：
1. 修改源代码根目录scripts文件夹下的eosio_build_ubuntu.sh文件内容，在208行处`https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.6.3.tgz` 修改为`http://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.6.3.tgz`
2. 再次运行eosio_build.sh，在安装编译过程中，如果不是root用户，需要输入认证密码提权才能继续。
3. 编译完成图示

### 3、编译完成后注意事项
  1. 编译完成后程序生成目录在源代码根目录的build/programs目录下。
  2. nodeos程序是否可用:
```
testsbcbuild@ubuntu:~/sbc-project/sbc/build/programs/nodeos$ ./nodeos --help
Application Options:
Config Options for eosio::bnet_plugin:
  --bnet-endpoint arg (=0.0.0.0:4321)   the endpoint upon which to listen for 
                                        incoming connections
.......
```


显示以上片段信息证明执行成功。
