在安装Ubuntu系统后发现与Windows系统的文件不能相互复制，网上查了很多教程，发现都是不能用的，能实现的方法如下所示：
```bash
sudo apt-get autoremove open-vm-tools
sudo apt-get install open-vm-tools
sudo apt-get install open-vm-tools-desktop
```
然后重启