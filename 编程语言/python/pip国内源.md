## 一、anaconda配置镜像
查看源：conda config --show-sources
在Mac and Linux下：
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes

在Windows下，直接在user目录中创建一个pip目录，如：C:\Users\xx\pip，新建文件pip.ini，内容如下
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple

换回默认源：conda config --remove-key channels

详细：https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/

或者：
执行conda命令：conda config
会创建conda的配置文件，使用search everything 查找 .condarc 并打开，在里面添加
channels:
- https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
- defaults
show_channel_urls: true


## 二、pip配置镜像 
Linux下：
修改 ~/.pip/pip.conf (没有就创建一个)， 修改 index-url至tuna，内容如下：
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple

在Windows下：
直接在user目录中创建一个pip目录，如：C:\Users\xx\pip，新建文件pip.ini，内容如下
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple

在mac下：
```
mdkir ~/.pip
cd .pip
vim pip.conf
```
配置如下：
```bash
[global]
trusted-host =  pypi.douban.com
index-url = http://pypi.douban.com/simple
```
临时使用：
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pandas