# MkDocs入门

## 安装

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


## 新建项目

环境搭建好后，开始创建一个新项目，运行以下命令：
```shell
mkdocs new my-project
cd my-project
```
很快，初始化的模板工程就创建好了。

![](../images/initial-layout.png)

模板工程包含一个名为`mkdocs.yml`的配置文件和一个名为`docs`的文件夹，其中`docs`包含该文档的源文件(`docs`是`docs_dir`配置项的默认值)。现在，`docs`文件夹只包含一个名为`index.md`的页面。

MkDocs附带了一个内置的开发服务器(dev-server)，可以使用它在开发时预览文档。切换到`mkdocs.yml`配置文件的同级目录下，然后通过运行`mkdocs serve`命令启动服务器：

```shell
$ mkdocs serve
INFO    -  Building documentation...
INFO    -  Cleaning site directory
[I 160402 15:50:43 server:271] Serving on http://127.0.0.1:8000
[I 160402 15:50:43 handlers:58] Start watching changes
[I 160402 15:50:43 handlers:60] Start detecting changes
```

浏览器中打开`http://127.0.0.1:8000`,预览初始化生成的首页。

![](../images/screenshot.png)

开发服务器支持自动重载，当配置文件、文档目录或主题目录中的任何内容发生变更时重新生成文档。

在文本编辑器中打开`docs/index.md`文档，将初始标题更改为`MkLorum`，然后保存更改。浏览器将自动重新加载，您应该能立即看到更新的文档。

现在尝试编辑配置文件：`mkdocs.yml`。将[`site_name`][site_name]设置为`MkLorum`并保存该文件。

```yaml
site_name: MkLorum
site_url: https://example.com/
```
您的浏览器应立即重新加载，并且看到新的网站名称生效。

![](../images/site-name.png)

>***注意：***`site_name`和`site_url`配置选项是配置文件中仅有的两个必需选项。创建新项目时，会为`site_url`选项指定占位符值：https://example.com, 如果知道最终的站点地址，可以替换成最终的地址。但在将站点部署到生产服务器之前，请确保是正确的。


[site_name]:../user-guide/configuration/#site_name


## 添加页面

现在添加文档的第二个页面：
```shell
curl 'https://jaspervdj.be/lorem-markdownum/markdown.txt' > docs/about.md
```

由于我们的文档站点将包含一些导航标题，您需要编辑配置文件，并在导航标题中添加导航设置，包括每个页面的顺序、标题和嵌套的信息：

```yaml
site_name: MkLorum
site_url: https://example.com/
nav:
    - Home: index.md
    - About: about.md
```

保存配置文件，现在将会看到一个导航栏，左侧显示`主页`和`关于`菜单，右侧显示`搜索`、`上一个`和`下一个`菜单。

![](../images/multipage.png)

尝试点击菜单并在页面之间来回切换。然后单击`搜索`。将出现一个搜索对话框，您可以搜索任何页面上的任何文本。请注意，搜索结果包括网站上搜索词的每次出现，并直接链接到搜索词出现的页面部分。您不需要再做其他的开发和配置即可使用该功能。

![](../images/search.png)


## 设置主题

现在更改配置文件，通过更改`主题`来更改文档的显示方式。编辑`mkdocs.yml`文件并添加[`主题`][theme]设置：
```yaml
site_name: MkLorum
site_url: https://example.com/
nav:
    - Home: index.md
    - About: about.md
theme: readthedocs
```

保存配置文件，可以看到ReadTheDocs主题的显示样式。

![](../images/readthedocs.png)

[theme]:https://www.mkdocs.org/user-guide/configuration/#theme

## 改变图标

默认情况下，MkDocs使用[MkDoc favicon][favicon]图标。
要想使用不同的图标，请在`docs`目录中创建一个`img`子目录，然后将自定义的`favicon.ico`文件复制到该目录。MkDocs将自动检测并使用该文件作为您的收藏夹图标。

[favicon]:https://www.mkdocs.org/img/favicon.ico


## 构建站点

一切就绪后，就具备了初次部署MkLorum文档的条件。首先要构建文档：
```shell
mkdocs build
```

这将会创建一个名为`site`的新目录。查看目录结构：

```console
$ ls site
about  fonts  index.html  license  search.html
css    img    js          mkdocs   sitemap.xml
```

请注意，已经将源文档编译为`index.html`和`about/index.html`两个HTML文件。也会将其他各种多媒体文件作为文档主题的一部分复制到`site`目录中。您甚至有一个`sitemap.xml`文件和`mkdocs/search_index.json`。

如果您使用的是git等源代码控制工具，如果不想将编译构建的产出物(如`site`)上传到仓库中，需要将`site/`添加到`.gitignore`文件中。

```shell
echo "site/" >> .gitignore
```

如果您使用的是另一款源代码控制工具，则需要查看其文档，了解如何忽略特定目录。


## 其他命令

还有各种其他命令和选项可用。要获得完整的命令列表，请使用`--help`标志：

```shell
mkdocs --help
```

要查看特定命令的可用选项列表，请在该命令中使用`--help`标志。例如，要获取`build`命令可用的所有选项的列表，请运行以下命令：

```shell
mkdocs build --help
```

## 部署站点

因为构建的文档站点只有静态文件，因此可以在几乎任何地方托管它。只需将整个站点的目录上传到托管网站的任何位置，即可完成。有关其他常见主机的具体说明，请参阅[部署文档]页面。

[部署文档]:https://www.mkdocs.org/user-guide/deploying-your-docs/

## 获得帮助

有关MkDocs所有功能的更完整文档，请参阅《用户指南》。
要获得MkDocs的帮助，请使用[GitHub讨论](https://github.com/mkdocs/mkdocs/discussions) 或[GitHub问题](https://github.com/mkdocs/mkdocs/issues)。



