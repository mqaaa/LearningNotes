# Jupyter

## 背景
昨天，想着用服务器搭个jupyter notebook 试试，毕竟服务器闲着也是闲着。

今天呢，就是把方法做个记录。省的以后走弯路，还有就是给我那个非CS的小伙伴写个简单的使用手册

## 使用工具
- Anaconda[官网](https://www.anaconda.com)、[文档](https://conda.io/docs/)
    ![Anaconda](../img/anaconda.png)
- Jupyer notebook [官网](https://jupyter.org/)[文档](https://jupyter-notebook.readthedocs.io/en/stable/)
    ![Jupyter](../img/jupyter.png)

## 操作
### 安装 Anaconda
 1、 安装Anaconda
  首先 `ssh` 到服务器上, 到一个非系统级的目录，下载anaconda安装脚本:

  下载
  `wget https://mirrors4.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-5.1.0-Linux-x86_64.sh`

  安装
  `sh Anaconda3-5.1.0-Linux-x86_64.sh`

 2、 设置软链接到`usr/local/bin`
  因为不设置环境变量，
  所以这一步是方便我们可以在命令行直接输入
  `anaconda3/bin` 下的可执行文件可执行文件名

 3、设置环境、并安装jupyer

```python
# 创建环境
conda create --name python3 python=3.6
# 进入环境
conda activate python3
# 退出环境
conda deactivate
# 环境列表查询
conda info --envs
```

### 服务器配置 jupyter
#### 首先生成 jupyter 配置文件
执行下面的命令: 
```
jupyter notebook --generate-config
```
配置文件会生成在以下路径:

- Windows: `C:\Users\USERNAME\.jupyter\jupyter_notebook_config.py`
- OS X: `/Users/USERNAME/.jupyter/jupyter_notebook_config.py`
- Linux: `/home/USERNAME/.jupyter/jupyter_notebook_config.py`

#### 生成密码与加密后的 hash 串
进入ipython,生成sha1加密后的密码:
```
from notebook.auth import passwd
passwd()
```
Copy下生成的加密字符串。

#### 配置 `jupyter_notebook_config.py`


先 `cd`进 `.jupyter`目录，

然后 `vim jupyter_notebook_config.py`进行修改

更改下面的配置: 
```python
# 允许所有的ip链接
c.NotebookApp.ip = '*'
# 启动时禁止打开浏览器
c.NotebookApp.open_browser = False
# 这里将jupyter_notebook_config.json里的sha1串复制过来,字符串前面的 u 是字符集（*）
c.NotebookApp.password = u"sha1:bb7b06..."
# 端口可设为其他，注意不要冲突
c.NotebookApp.port = 9999
# 默认目录
c.NotebookApp.base_url = '/ipython/'
# 配置域名
c.NotebookApp.tornado_settings = {
    'headers': {
        'Content-Security-Policy': "frame-ancestors https://mywebsite.example.com 'self' "
    }
}
```
[官方详情](https://jupyter-notebook.readthedocs.io/en/latest/public_server.html#embedding-the-notebook-in-another-website)

### 启动 jupyter
后台启动
`nohup jupyter notebook --allow-root &`

> Tips: jupyter 新的 jupyter lab 比 notebook 做了一些优化，界面也高端很多。只要在 url 后面加 /lab就能立即享用 
http://xxxx:8888/lab(这个还没试过)

