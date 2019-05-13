# 1. Mono安装

首先，Mac下需要使用.Net编译后的程序，需要用到跨平台的方案Mono(现阶段微软已推出跨平台的方案.Net Core，不过暂时只支持控制台程序)。安装程序可以从http://www.mono-project.com/download/#download-mac地址下载。

Mono框架有自己的可信根证书存储。目前（在单声道版本4.2.4），在OS X上安装Mono之后，该存储仍然为空。Fiddler使用该存储中的证书来验证所访问网站的证书。因此，您需要使用一组通常受信任的根权限来填充此存储，以避免从Fiddler获得持续的证书警告。cert-sync工具从Mozilla LXR导入受信任的权威机构。

我安装的最新的mono版本号为5.20.1 所以在终端里面输入的是：
```bash
/Library/Frameworks/Mono.framework/Versions/5.20.1/bin/cert-sync --import --sync
```
接下来还需要将Mono加入到环境变量中。编辑.bash_profile文件：
```bash
vim ~/.bash_profile
```
加入文本：
```bash
export MONO_HOME=/Library/Frameworks/Mono.framework/Versions/5.20.1
export PATH=$PATH:$MONO_HOME/bin
```
source保存后重新打开Terminal，Mono环境已装好。

## 2. Fiddler安装

从Fiddler官网https://www.telerik.com/download/fiddler下载fiddler-mac.zip的压缩包。解压到非中文字符的路径下。

打开Terminal，进入到刚才解压的Fiddler路径，执行命令运行：

```
ssudo mono --arch=32  Fiddler.exe
```