Ubuntu16.04LTS安装了自带的Python3软件包，结果发现版本是3.5。心血来潮升级了Python到3.6,并且也成功地将默认Python版本换成了Python3.6.3。然后发现终端打不开了，点击图标显示正在打开但并不能打开，使用Ctrl+alt+T也打不开。于是开始查找解决办法，最终在以下贴中找到方法：
```
https://blog.csdn.net/u010395144/article/details/52794947
https://blog.csdn.net/jaket5219999/article/details/78465251
```
## 1. 寻找错误

首先，ctrl+alt+F1进入命令行模式，登录账号后，输入下面命令查找终端的问题：
```bash
gnome-terminal
```
报以下错误：
```bash
ImportError: cannot import name ‘_gi’
```
这是装Python时遗留下来的问题。
## 2.解决
进入路径：
```bash
cd /usr/lib/python3/dist-packages/gi/
```
备份以下文件：
```
sudo cp _gi_cairo.cpython-35m-x86_64-linux-gnu.so _gi_cairo
sudo _gi.cpython-35m-x86_64-linux-gnu.so _gi_cpython
```

然后重命名：
```
sudo mv _gi_cairo _gi_cairo.cpython-36m-x86_64-linux-gnu.so 
sudo mv _gi_cpython _gi.cpython-36m-x86_64-linux-gnu.so 
```

然后ctrl+alt+F7返回图形界面即可。