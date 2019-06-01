前言：mac系统自带python，不过以当前mac系统的最新版本为例，自带的python版本都是2.*版本，虽然不影响老版本项目的运行，但是python最新的3.*版本的一些语法与2.*版本并不相同，网上的教程大神们也肯定都更新出了最新版的教程，我们不论是学习还是使用，当然用最新版会更好一点。

1、在安装最新版Python3.*之前，我们先熟悉一下系统自带的python。

Mac系统自带python路径为／System／Library／Frameworks／Python.framework/Version,我们先来打开目录看一下：
```bash
open /System/Library/Frameworks/Python.framework/Versions
```
我们看到这里有多个python版本，而在Current目录下存放的是系统当前的python版本。

mac既然自带了python，当然肯定配置好了python的全局命令，我们直接在终端运行：
```bash
$ python

Python 2.7.10 (default, Jul 15 2017, 17:16:57) 
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.31)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
```
 运行正常。到这里也差不多对mac系统自带的python有所了解，接下来我们开始安装最新版本的python。

 2. 使用brew安装。

安装前先搜索一下是否已经存在python3的包：

```bash
$ brew search python3
==> Formulae
python3 ✔                                homebrew/linuxbrew-core/boost-python3
```
已经存在，我们可以直接安装了：
```bash
brew install python3
```
所有的包都下载完毕，但是我们却发现最后报了两条错误:
```
Error: An unexpected error occurred during the `brew link` step
The formula built, but is not symlinked into /usr/local
Permission denied @ dir_s_mkdir - /usr/local/Frameworks
Error: Permission denied @ dir_s_mkdir - /usr/local/Frameworks
```
这是因为没有创建目录/usr/local/Frameworks的权限，我们需要创建该目录，并授权：
```bash
sudo mkdir /usr/local/Frameworks
sudo chown $(whoami):admin /usr/local/Frameworks
```
修改好权限之后，还需要手动执行一下安装时未完成的创建连接：
```bash
brew link python3
```
连接成功。咱们来查看一下当前系统下的python3的信息：
```bash
brew info python3

python3: stable 3.6.4 (bottled), devel 3.7.0a3, HEAD
Interpreted, interactive, object-oriented programming language
https://www.python.org/
/usr/local/Cellar/python3/3.6.4_2 (3,049 files, 48.6MB) *
  Poured from bottle on 2019-05-26 at 10:47:55
From: https://mirrors.ustc.edu.cn/homebrew-core.git/Formula/python3.rb
==> Dependencies
Build: pkg-config ✘, sphinx-doc ✘
Required: openssl ✔
Recommended: readline ✔, sqlite ✔, gdbm ✔, xz ✔
Optional: tcl-tk ✘, sphinx-doc ✘
==> Options
...
```
发现python3被安装到了/usr/Cellar/python3目录下，有兴趣的小伙伴自行前往查看想过配置文件。
到这里python3的安装就算完成了，不过可能有小伙伴已经发现，不管是在终端运行python -V查看版本号还是直接运行python启动python命令行模式，默认的python版本还是系统自带的2.*版本。其实这时候只运行命令时需要把python改为python3就行了，当然，我们可以配置一下默认版本，把当前系统的默认版本修改为3.*版本。
首先，查看python3命令所在：
```bash
which python3
/usr/local/bin/python3
```
起别名：
```bash
sudo vim ~/.bash_profile
alias python="/usr/local/bin/python3"
```
立即生效：
```bash
source ~/.bash_profile
```

输入：
```bash
python
Python 3.6.4 (default, Jan  6 2018, 11:51:59) 
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.39.2)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
```