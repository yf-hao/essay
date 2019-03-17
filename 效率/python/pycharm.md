# 1. pycharm中关掉ipython console/PyDev
在pycharm中无论运行什么样的python脚本，都会默认使用ipython的console运行，这种console非常恶心，前几行全是费话。
![](https://raw.githubusercontent.com/fray-hao/images/master/20190315134439.png)
而且运行完后，不会自动关闭，这样console越积越多，就像上图一样开了十几个。

如何回到原来默认的console呢？
![](https://i.loli.net/2019/03/15/5c8b3bedcbebf.png)
![](https://i.loli.net/2019/03/15/5c8b3bfbacf20.png)

把箭头指的钩去掉，就可以了。

这样关掉的只是一个文件，如果想全局关掉，就要把default中的钩去掉：
![](https://i.loli.net/2019/03/15/5c8b3c129aaa5.png)

这样一来，就清爽多了。

参考链接：https://intellij-support.jetbrains.com/hc/en-us/community/posts/115000752090-Disable-PyDev-IPython-console-message-in-python-debug-prompt-

https://stackoverflow.com/questions/47917952/how-to-disable-pydev-console-debugger-in-pycharm-when-not-debugging?rq=1

