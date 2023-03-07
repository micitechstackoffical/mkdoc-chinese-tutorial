# 软件安装

### 前置条件

MkDocs需要安装最新版本的[Python](https://www.python.org/) 和Python包管理器[pip](https://pip.readthedocs.io/en/stable/installing/)。
可以通过以下命令行检查是否已经安装：

``` shell
$ python --version
Python 3.8.2
$ pip --version
pip 20.0.2 from /usr/local/lib/python3.8/site-packages/pip (python 3.8)
```

如果您已经安装了这些软件包，可以跳到[安装MkDocs](#安装mkdocs)。

#### 安装Python
使用包管理器安装[Python](https://www.python.org/) ，或者从[Python.org](https://www.python.org/downloads/) 下载对应版本的安装程序并运行它。

> ***注意*** 
>
>如果您在Windows上安装Python，需要将Python添加到PATH中。如果安装程序提供了这样的选项（默认情况下通常关闭），请确保选中该复选框。
>
>![add-to-path](../images/win-py-install.png)

#### 安装pip
如果您使用的是最新版本的Python，那么包管理器`pip`很可能是默认安装的。但是，您可能需要将`pip`升级到最新版本：

``` shell
pip install --upgrade pip
```
如果是第一次安装pip，请下载[get-pip.py](https://bootstrap.pypa.io/get-pip.py) 。然后运行以下命令安装它：

```shell
python get-pip.py
```


### 安装MkDocs

使用pip包管理器安装`mkdocs`:

```shell
pip install mkdocs
```

现在应该在系统上安装了`mkdocs`命令。运行`mkdocs--version`以检查一切是否正常。

```shell
$ mkdocs --version
mkdocs, version 1.2.0 from /usr/local/lib/python3.8/site-packages/mkdocs (Python 3.8)
```
>***注意***
>
>如果您希望为MkDocs安装手册页，[click-man]工具可以为您生成并安装手册页。只需运行以下两个命令：
>
>```
>pip install click-man
>click-man --target path/to/man/pages mkdocs
>```
>
> 有关pip未自动生成和安装手册页的原因，请参阅[click-man文档]。


[click-man]:https://github.com/click-contrib/click-man
[click-man文档]:https://github.com/click-contrib/click-man#automatic-man-page-installation-with-setuptools-and-pip


>***注意***
>
>如果您使用的是Windows，上面的一些命令可能无法开箱即用。
>
>一个快速的解决方案是在每个Python命令前面加上`python -m`，如下所示：
>
>``` shell
>python -m pip install mkdocs
>python -m mkdocs
>```
>
>对于更持久的解决方案，需要将Python安装的`Scripts`目录添加到`PATH`
>环境变量中。Python的最新版本包括一个脚本，可以为您执行此操作。进入到Python安装目录（例如C:\Python38\），打开`Tools`，然后打开`scripts`文件夹，双击运行
>`win_ad2path.py`文件。或者，您也可以下载脚本并运行它(`python win_ad2path.py`)。