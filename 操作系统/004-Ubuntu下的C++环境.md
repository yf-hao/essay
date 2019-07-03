## 1.环境准备
首先需要,安装ｇcc和ｇ++环境

安装之前查看是否有安装,使用命令:
```bash
gcc --version
g++ --version
```
如果没有安装使用如下命令进行安装:
```bash
# 版本安装：这里选择的式版本5
sudo apt-get install gcc-5
sudo apt-get install g++-5
```
## 写源代码
```bash
#include<iostream>
 
using namespace std;
 
int main()
 
{
    cout<<"Hello world"<<endl;
    return 0;
}
```
## 3.编译
```bash
g++ -o helloWorld helloWorld.cpp
```
## 4. 运行：
```bash
$ ./helloWorld 
Hellow, world
```