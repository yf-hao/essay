多版本python下的使用：
## 方式1：
```bash
# python2

python2 -m pip install 模块名
 # python3

python3 -m pip install 模块名
```
##  方式2：更改pip指向
命令如下：which pip

一般情况下会显示：
```bash
/usr/local/bin/pip
```
然后 
```bash
vim /usr/local/bin/pip
```
我们可以看到如下：
```bash
#!/usr/bin/python3

# -*- coding: utf-8 -*-
import re
import sys

from pip import main

if __name__ == '__main__':
    sys.argv[0] = re.sub(r'(-script\.pyw|\.exe)?$', '', sys.argv[0])
    sys.exit(main())


```
将第一行 "#!/usr/bin/python3"修改为
```
#!/usr/bin/python2
```
然后pip 就指向python2了
