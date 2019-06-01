## 一 虚拟环境 virtual environment

它是一个虚拟化，从电脑独立开辟出来的环境。通俗的来讲，虚拟环境就是借助虚拟机docker来把一部分内容独立出来，我们把这部分独立出来的东西称作“容器”，在这个容器中，我们可以只安装我们需要的依赖包，各个容器之间互相隔离，互不影响。譬如，本次学习需要用到Django，我们可以做一个Django的虚拟环境，里面只需要安装Django相关包就可以了，需要Scrapy库，就在开辟一个独立空间来学习Scrapy库相关就行了。

## 二  前言：为什么要用虚拟环境

在实际项目开发中，我们通常会根据自己的需求去下载各种相应的框架库，如Scrapy、Beautiful Soup等，但是可能每个项目使用的框架库并不一样，或使用框架的版本不一样，这样需要我们根据需求不断的更新或卸载相应的库。直接怼我们的Python环境操作会让我们的开发环境和项目造成很多不必要的麻烦，管理也相当混乱。如一下场景：

场景1：项目A需要某个框架1.0版本，项目B需要这个库的2.0版本。如果没有安装虚拟环境，那么当你使用这两个项目时，你就需要 来回 的卸载安装了，这样很容易就给你的项目带来莫名的错误；

场景2：公司之前的项目需要python2.7环境下运行，而你接手的项目需要在python3环境中运行，想想就应该知道，如果不使用虚拟环境，这这两个项目可能无法同时使用，使用python3则公司之前的项目可能无法运行，反正则新项目运行有麻烦。而如果虚拟环境可以分别为这两个项目配置不同的运行环境，这样两个项目就可以同时运行。

Tips:其实虚拟环境好处也确实比较多，会给我们项目的开发带来许多的好处，但是初学者，建议还是不要这么折腾，我们的首要目的是更快的掌握更多的知识，研究virtualenv会花费一些额外的经历，而且意志不强的同学很容易遭受打击，但是这个优点我们还是要记下来的方便以后要用的时候能很快的想起。

## 三 Python2 虚拟环境的安装和使用

1. 安装virtualenv
    ```bash
    pip install virtualenv  # 卸载 pip uninstall virtualenv
    ```
2. 查看当前系统Python的环境下，已经安装的库：    
    ```bash
    frayhaoiMac:~ fray_hao$ pip list
        Package    Version 
        ---------- --------
        certifi    2019.3.9
        chardet    3.0.4   
        idna       2.8     
        pip        19.1.1  
        requests   2.22.0  
        selenium   3.141.0 
        setuptools 28.8.0  
        urllib3    1.25.2  
        virtualenv 16.6.0  
    ```
3. 创建虚拟环境
    ```bash
    mkdir python_book_env
    cd python_book_env/
    vitualenv python_book # 创建名为python_book的虚拟环境
    ```
4. 激活虚拟环境
   ```bash
    cd ~/python_book_env/python_book/bin/
    source ./activate # 激活环境
    pip list

    Package    Version
    ---------- -------
    pip        19.1.1 
    setuptools 41.0.1 
    wheel      0.33.4 

   ```
5. 测试：
    ```bash
    pip install requests
    ```
    结果：
    ```bash
    pip list
    Package    Version 
    ---------- --------
    certifi    2019.3.9
    chardet    3.0.4   
    idna       2.8     
    pip        19.1.1  
    requests   2.22.0  
    setuptools 41.0.1  
    urllib3    1.25.2  
    wheel      0.33.4  
    ```
6. 退出环境
   ```bash
    cd ~/python_book_env/python_book/bin/
    deactivate # 退出环境
   ```
7. 自动加载虚拟环境
   ```bash
    vim ~/.bash_profile
    # 自动加载python虚拟环境
    source ~/book_env/bin/activate
   ```

virtualenv创建环境时的重要参数：
- --system-site-packages： 安装在系统的Python环境中的库，也复制到这个虚拟环境中来了
- --python=PYTHON_EXE ： 当存在多个python环境中时，可以指定根据哪个python创建环境。例如： --python=python2.7
  

## 四.python3
Python3.3以上的版本通过venv模块原生支持虚拟环境，可以代替Python之前的virtualenv。

该venv模块提供了创建轻量级“虚拟环境”，提供与系统Python的隔离支持。每一个虚拟环境都有其自己的Python二进制（允许有不同的Python版本创作环境），并且可以拥有自己独立的一套Python包。他最大的好处是，可以让每一个python项目单独使用一个环境，而不会影响python系统环境，也不会影响其他项目的环境。

优点：
- 使不同应用开发环境独立
- 环境升级不影响其他应用，也不会影响全局的python环境
- 防止系统中出现包管理混乱和版本冲突

1. 创建环境
   ```bash
    pytyon -m venv book_env # 创建名为 book_env的环境
   ```
2.  激活与退出方法与virtualenv类似。先进入bin目录，激活或退出
