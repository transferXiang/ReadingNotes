# Jupyter 安装

## 安装jupyter

```
# 更新源
apt-get update

# 安装python pip
apt-get install -y python3
apt-get install -y python3-pip

# 安装jupter
pip3 install jupyter
```

## 配置jupyter
这时由于没有配置密码，所以仅允许本地进行访问，如果希望远程访问需要继续执行下面的脚本
```
# 生成配置文件
# 生成的路径一般为:/home/transfer/.jupyter/jupyter_notebook_config.py
# transfer为当前用户的用户名
jupyter notebook --generate-config --allow-root

# 启动ipython为了生成加密后的密码
ipython
```

这时进入ipython的运行环境，接着依次输入一下内容：
```
from notebook.auth import passwd
passwd()
# 输入密码，这时会生成一组加密后的字符串，拷贝下来
# 如输入jupyter加密后为'sha1:66acf0097398:0a0333384ee2c45a3dd6d9cb094ab98bff93184e'
```

将以下内容添加到jupyter_notebook_config.py文件中
```
c.NotebookApp.ip='*'
c.NotebookApp.password = u'sha:ce...刚才复制的那个密文'
c.NotebookApp.open_browser = False
c.NotebookApp.port =8888 #随便指定一个端口
```
