1. 添加PPA：
   ```bash
    sudo add-apt-repository ppa:jonathonf/python-3.7
    sudo apt-get update
   ```
2. 安装：
   ```bash
    sudo apt-get install python3.7
   ```
3. 调整python3的优先级顺序，使得python3.7的优先级最高
   ```bash
    sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.5 1
    sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 2
   ```
4. 更改默认值，python默认为Python2，现在修改为Python3
   ```bash
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 100
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 150
   ```   
    