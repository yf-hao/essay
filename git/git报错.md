- **提交时报错:Updates were rejected because the tip of your current branch is behind**

出现这样的问题是由于:自己当前版本低于远程仓库版本
有如下几种解决方法：
1. 强制push的方法：
```bash
 git push -u origin master -f
```
这样会使远程修改丢失，一般是不可取的，尤其是多人协作开发的时候。
2. push前先将远程repository修改pull下来
```bash
git pull origin master
git push -u origin master
```
3. 若不想merge远程和本地修改，可以先创建新的分支：

```bash
git branch [name]
git push -u origin [name]
```