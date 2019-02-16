## 1.解释器执行
用python解释器执行源代码：
```python
# 使用 python 2.x 解释器
python xxx.py

# 使用 python 3.x 解释器
python3 xxx.py
```

Python 的解释器 如今有多个语言的实现，包括：

- CPython —— 官方版本的 C 语言实现
- Jython —— 可以运行在 Java 平台
- IronPython —— 可以运行在 .NET 和 Mono 平台
- PyPy —— Python 实现的，支持 JIT 即时编译

## 2. 交互式运行

### 2.1. python shell
直接在终端中运行解释器进入交互shell，在shell中直接输入 Python 的代码，会立即看到程序执行结果
```sheLl
fray_hao$ python

>>> print("Hello World")
Hello World
```
缺点： 代码无法保存，不适合运行太大的程序

退出python shell：

```python
exit()
```
### 2.2 ipython
IPython 中 的 “I” 代表 交互 interactive,是一个 python 的 交互式 shell，比默认的 python shell 好用得多
- 支持自动补全 : 按tab键
- 自动缩进
- 支持 bash shell 命令
- 内置了许多很有用的功能和函数

```python
fray_hao$ ipython


In [1]: print("hello World")
hello World
```
### 3. 集成开发环境（IDE）
集成开发环境（IDE，Integrated Development Environment）—— 集成了开发软件需要的所有工具，一般包括以下工具：
- 图形用户界面
- 代码编辑器（支持 代码补全／自动缩进）
- 编译器／解释器
- 调试器（断点／单步执行）

PyCharm 是 Python 的一款非常优秀的集成开发环境.PyCharm 除了具有一般 IDE 所必备功能外，还可以在 Windows、Linux、macOS 下使用,适合开发大型项目。

1. 在文件编辑区域编写代码
2. 右上角的 工具栏 能够 执行(SHIFT + F10) / 调试(SHIFT + F9) 代码
    ![image.png](https://upload-images.jianshu.io/upload_images/13764292-2f77803b4129c1b1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
3. 通过控制台上方的单步执行按钮(F8)，可以单步执行代码
![image.png](https://upload-images.jianshu.io/upload_images/13764292-3e4bf091eca5dd3c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

