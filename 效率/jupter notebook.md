# 修改默认目录
- 方式1
  打开Anaconda Prompt，输入如下命：
   ```
   jupyter notebook --generate-config
   ```
   如下图：
   ![](https://raw.githubusercontent.com/fray-hao/images/master/20190409144438.png)
   修改jupyter_notebook_config.py文件中的：
   ```
   ## The directory to use for notebooks and kernels. 
   #c.NotebookApp.notebook_dir = ''
   ``` 
   为：
   ```
   ## The directory to use for notebooks and kernels. 
   c.NotebookApp.notebook_dir = 'E:\Jupyter' 
   ```
- 方式2
  找到快捷方式：
  ![](https://raw.githubusercontent.com/fray-hao/images/master/20190409145516.png)
   右键属性进入，并修改起始位置的地址为E:\Jupyter，然后应用便可成功
  ![](https://raw.githubusercontent.com/fray-hao/images/master/20190409145614.png)
- 方式3
  打开Anaconda安装目录下的etc\jupyter文件下的jupyter_notebook_config.json：
  ```json
    {
    "NotebookApp": {
        "nbserver_extensions": {
        "jupyterlab": true
        },
        "notebook_dir": "D:\\github\\essay\\jupter"
    }
    }
  ```
 最后，查看Jupyter Notebook快捷方式的属性，注意到目标栏目里面，默认启动目录是%USERPROFILE%，也就是用户目录下的个人账户目录。
 ![](https://raw.githubusercontent.com/fray-hao/images/master/20190409150352.png)

 将其删掉即可。