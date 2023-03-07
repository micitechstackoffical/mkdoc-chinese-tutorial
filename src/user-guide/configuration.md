# 配置文件


所有可用配置设置指南。

## 介绍

默认情况下，项目使用目录中名为`mkdocs.yml`的YAML配置文件进行配置。您可以使用`-f`/`--config-file`选项为其指定另一个路径（请参见`mkdocs build --help`）。

此配置文件至少应该包含`site_name`，其他设置都是可选的。

## 项目信息

### site_name

这是一个**必填的设置**，应该是一个用作项目文档主标题的字符串。例如：

```yaml
site_name: Marshmallow Generator
```

当渲染主题时，此设置将传递给`site_name`上下文变量。

### site_url

设置网站的标准URL。这将在每个HTML页面的`head`部分添加一个带有`canonical`URL的`link`标记。如果MkDocs站点的'root'位于域的子目录中，请确保在设置中也要包含该子目录(`https://example.com/foo/`).

此设置也用于`mkdocs serve`：服务器将挂载到从URL的路径组件获取的路径上，例如`some/page.md` 将从`http://127.0.0.1:8000/foo/some/page/` URL获取以模拟预期的远程布局。

**default**: `null`

### repo_url

设置后，在每个页面上提供指向代码仓库（GitHub、Bitbucket、GitLab…）的链接。

```yaml
repo_url: https://github.com/example/repository/
```

**default**: `null`

### repo_name

设置后，在每个页面上提供指向代码仓库的链接的名称。

**default**: 如果`repo_url`与这些域相匹配，该值为`'GitHub'`, `'Bitbucket'` 或 `'GitLab'`，否则为`repo_url` 中的主机名。

### edit_uri

当直接查看页面时，从`repo_url`仓库到docs目录的路径，说明代码仓库（例如GitHub、Bitbucket等）、分支和docs目录本身的细节。MkDocs连接`repo_url`和`edit_uri`，并附加页面的输入路径。

设置后，如果您的主题能识别它，则会直接提供指向源代码仓库中页面的链接。这使查找和编辑页面的源变得更容易。如果未设置`repo_url` ，则忽略此选项。在某些主题上，设置此选项可能会导致将编辑链接代替为代码仓库链接。其他主题可能会显示这两个链接。

`edit_uri`支持查询('?')和片段('#')字符。对于使用查询或片段访问文件的代码仓库，`edit_uri`可能设置如下。（注意URI中的`?`和`#`…）

```yaml
# Query string example
edit_uri: '?query=root/path/docs/'
```

```yaml
# Hash fragment example
edit_uri: '#root/path/docs/'
```

对于其他代码仓库，只需指定docs目录的相对路径。

```yaml
# Query string example
edit_uri: root/path/docs/
```

例如，如下配置:

```yaml
repo_url: https://example.com/project/repo
edit_uri: blob/main/docs/
```

表示名为`foo/bar.md`的页面的编辑链接将指向
<https://example.com/project/repo/blob/main/docs/foo/bar.md>

`edit_uri`实际上可以是一个绝对URL，不一定是`repo_url`的相对地址，因此这可以实现相同的结果：

```yaml
edit_uri: https://example.com/project/repo/blob/main/docs/
```

有关更多灵活性，请参见下面的[edit_uri_template](#edit_uri_template)。

> ***注意***:
> `edit_uri` configs setting.对于一些已知的代码托管平台（如：GitHub、Bitbucket和GitLab），`edit_uri`是从`repo_url`推断出来的，不需要手动设置。只需定义一个`repo_url`将自动填充`edit_uri`配置设置。
>
> 例如，对于GitHub或GitLab托管的代码仓库，`edit_uri`将自动设置为`edit/master/docs/`（请注意`edit`路径和`master`分支）
>
> 对于Bitbucket托管的代码仓库，同样的，`edit_uri`将自动设置为`src/default/docs/`（注意`src`路径和`default`分支）
>
> 如果不想使用默认的URI(如：其他分支)，只需将`edit_uri`设置为所需的字符串。如果您不希望页面上显示任何`编辑URL链接`，请将`edit_uri`设置为空字符串以禁用自动转换。

>***警告***:
>在GitHub和GitLab上，在线编辑器中使用默认的`编辑`路径（`edit/master/docs/`）打开编辑页面。
>此功能要求用户登录到GitHub/GitLab帐户。否则，用户将被重定向到登录/注册页面。或者，使用`blob`路径（`blob/master/docs/`）打开支持匿名访问的只读视图。

**default**: 如果`repo_url`与这些域匹配，GitHub和GitLab值为：`edit/master/docs/`，Bitbucket值为：`src/default/docs/`，否则为`null`

### edit_uri_template

[edit_uri](#edit_uri)更灵活的变体。这两者是等价的：

```yaml
edit_uri: 'blob/main/docs/'
edit_uri_template: 'blob/main/docs/{path}'
```

(它们也是互斥的——不要同时指定两者).

从现在开始，您可以更改路径的位置或格式，以防路径的默认值不满足要求。

`edit_uri_template`的内容是正常的[Python格式字符串](https://docs.python.org/3/library/string.html#formatstrings)， 只有以下字段可用：

* `{path}`, e.g. `foo/bar.md`
* `{path_noext}`, e.g. `foo/bar`

以及转换标志`!q`可用于对字段进行百分比编码：

* `{path!q}`, e.g. `foo%2Fbar.md`

> 注意: **一些有用配置:**
>
> *   GitHub Wiki:  
>     (e.g. `https://github.com/project/repo/wiki/foo/bar/_edit`)
>
>     ```yaml
>     repo_url: 'https://github.com/project/repo/wiki'
>     edit_uri_template: '{path_noext}/_edit'
>     ```
>
> *   BitBucket editor:  
>     (e.g. `https://bitbucket.org/project/repo/src/master/docs/foo/bar.md?mode=edit`)
>
>     ```yaml
>     repo_url: 'https://bitbucket.org/project/repo/'
>     edit_uri_template: 'src/master/docs/{path}?mode=edit'
>     ```
>
> *   GitLab Static Site Editor:  
>     (e.g. `https://gitlab.com/project/repo/-/sse/master/docs%2Ffoo%2bar.md`)
>
>     ```yaml
>     repo_url: 'https://gitlab.com/project/repo'
>     edit_uri_template: '-/sse/master/docs%2F{path!q}'
>     ```
>
> *   GitLab Web IDE:  
>     (e.g. `https://gitlab.com/-/ide/project/repo/edit/master/-/docs/foo/bar.md`)
>
>     ```yaml
>     edit_uri_template: 'https://gitlab.com/-/ide/project/repo/edit/master/-/docs/{path}'
>     ```
**default**: `null`

### site_description

设置站点描述。这将向生成的HTML header中添加一个元数据。

**default**: `null`

### site_author

设置作者的姓名。这将向生成的HTML header中添加一个元数据。

**default**: `null`

### copyright

设置要包含在文档中的版权信息。

**default**: `null`

### remote_branch

设置使用`gh-deploy`部署到GitHub Pages时要提交的远程分支。此选项可以被`gh-deploy`中的命令行选项覆盖。

**default**: `gh-pages`

### remote_name

设置使用`gh-deploy`部署到GitHub Pages时要推送的远程名称。此选项可以被`gh-deploy`中的命令行选项覆盖。

**default**: `origin`

## 文档布局

### nav

此设置用于确定站点的全局导航的格式和布局。最小导航配置如下所示：

```yaml
nav:
    - 'index.md'
    - 'about.md'
```

导航配置中的所有路径都必须是[`docs_dir`](#docs_dir)的相对路径。请参阅[配置页面和导航]一节，了解更详细的细分，包括如何创建子菜单。

导航项还可以包括指向外部站点的链接。对于内部链接标题是可选的，但对于外部链接是必需的。外部链接可以是完整URL或相对URL。在文件中找不到的任何路径都假定为外部链接。关于MkDocs如何确定文档的页面标题，请参见[元数据]一节。

```yaml
nav:
    - Introduction: 'index.md'
    - 'about.md'
    - 'Issue Tracker': 'https://example.com/'
```

在上面的示例中，前两项指向本地文件，而第三项指向外部站点。

然而，有时候MkDocs站点位于项目站点的子目录中，您可能希望链接到同一站点的其他部分，而不包括整个域。在这种情况下，您可以使用相对路径的URL。

```yaml
site_url: https://example.com/foo/
nav:
    - Home: '../'
    - 'User Guide': 'user-guide.md'
    - 'Bug Tracker': '/bugs/'
```

在上面的示例中，使用了两种不同样式的外部链接。首先，注意`site_url`表示MkDocs站点位于域的`/foo/`子目录中。因此，`Home`菜单是一个相对链接，它可以切换到服务器根目录，并有效地指向`https://example.com/`. `Bug Tracker`项使用服务器根目录的绝对路径，并有效地指向`https://example.com/bugs/`. 当然，`User Guide`指向本地MkDocs页面。

**default**: 
sub-directories. Index files will always be listed first within a sub-section.默认情况下，`nav`将包含`docs_dir`及其子目录中所有按字母数字顺序排序和嵌套的Markdown文件列表。索引文件总是在子节中首先列出。

## 构建目录

### theme

设置文档站点的主题和主题配置。可以是字符串或一组键/值对。

如果是字符串，则必须是已安装主题的字符串名称。有关可用主题的列表，请访问[选择主题]。

键/值对的示例集可能如下所示：

```yaml
theme:
    name: mkdocs
    locale: en
    custom_dir: my_theme_customizations/
    static_templates:
        - sitemap.html
    include_sidebar: false
```

如果是一组键/值对，则可以定义以下嵌套键：

> BLOCK:
>
> #### name
>
> 已安装主题的字符串名称。有关可用主题的列表，请访问[选择主题]
>
> #### locale
>
> 表示站点语言的编码。有关详细信息，请参阅[本地化主题]。
>
> #### custom_dir
>
> 包含自定义主题的目录。这可以是一个相对目录，在这种情况下，它是相对于包含配置文件的目录进行解析的，也可以是从本地文件系统的根目录开始的绝对目录路径。
>
> 如果您想调整现有主题，参见[自定义主题][theme_dir]获取详细信息。
>
> 如果您想从头开始构建自己的主题，请参阅[主题开发人员指南]。
>
> #### static_templates
>
> 用于渲染静态页面的模板列表。模板必须位于主题的模板目录或主题配置中定义的`custom_dir`中。
>
> #### (theme specific keywords)
>
> 还可以定义主题支持的任何其他关键字。有关详细信息，请参阅所使用主题的文档。  

**default**: `'mkdocs'`

### docs_dir

包含文档源文件的目录。这可以是相对目录，在这种情况下，它是相对于包含配置文件的目录进行解析的，也可以是从本地文件系统的根目录开始的绝对目录路径。

**default**: `'docs'`

### site_dir

输出站点HTML和其他文件的目录。这可以是相对目录，在这种情况下，它是相对于包含配置文件的目录进行解析的，也可以是从本地文件系统的根目录开始的绝对目录路径。

**default**: `'site'`

> 注意:
> 如果您使用的是源代码控制系统，则通常需要确保您的*构建输出*文件未提交到代码仓库中，并且只将*源*文件置于版本控制之下。例如，如果使用`git`，可以将以下行添加到`.gitignore`文件中：
>
> ```text
> site/
> ```
>
> 如果您使用的是另一个源代码控制工具，则需要查看其文档，了解如何忽略特定目录。
### extra_css

设置主题中引入的`docs_dir`中的CSS文件列表。例如，以下示例将在[docs_dir](#docs_dir)的css子目录中包含`extra.css`文件。

```yaml
extra_css:
    - css/extra.css
    - css/second_extra.css
```

**default**: `[]` (空列表).

### extra_javascript

Set a list of JavaScript files in your `docs_dir` to be included by the theme.
See the example in [extra_css] for usage.
设置主题中引入的`docs_dir`中的JavaScript文件列表。有关用法，请参见[extra_css]中的示例。

**default**: `[]` (空列表).

### extra_templates

在`docs_dir`中设置一个由MkDocs构建的模板列表。要了解有关为MkDocs编写模板的更多信息，请阅读有关[自定义主题]的文档，特别是有关模板的[可用变量]的章节。有关用法，请参见[extra_css]中的示例。

**default**: `[]` (空列表).

### extra

一组键值对，其中的值可以是任何有效的YAML结构，该值将传递给模板。这在创建自定义主题时提供了极大的灵活性。

例如，如果使用的主题支持显示项目版本，则可以将其传递给主题，如下所示：

```yaml
extra:
    version: 1.0
```

**default**: `extra` 默认是空的.

## 预览控件

## 实时重载

### watch

设置当运行`mkdocs serve`时要监视的其他目录。配置项是YAML列表。

```yaml
watch:
- directory_a
- directory_b
```

允许设置自定义默认值，而无需在每次调用`mkdocs serve`命令时通过`-w`/`--watch`选项进行传递。

> ***注意***:
> 此处设置的路径是配置文件的相对路径。
>
> 通过`-w`/`--watch`命令行参数提供的路径不是。
### use_directory_urls

此配置项控制文档中用于链接到页面的样式。

下表显示了将`use_directory_urls`设置为`true`或`false`时，网站上使用的URL的差别。

源文件      | use_directory_urls: true  | use_directory_urls: false
---------------- | ------------------------- | -------------------------
index.md         | /                         | /index.html
api-guide.md     | /api-guide/               | /api-guide.html
about/license.md | /about/license/           | /about/license.html


默认样式`use_directory_urls: true`创建了更多用户友好的URL，这通常是您想要使用的。

如果您希望文档在直接从文件系统打开页面时保持正确的链接，则另一种样式会很有用，因为它创建的链接直接指向目标`文件`而不是目标`目录`。

**default**: `true`

### strict

设置如何处理警告。设置为`true`可在发出警告时停止处理。设置为`false`以打印警告并继续处理。

也可以作为命令行参数: `--strict`.

**default**: `false`

### dev_addr

确定运行`mkdocs serve`时使用的地址。格式必须为`IP:PORT`。

允许设置自定义默认值，而无需在每次调用`mkdocs serve`命令时将其传递给`--dev-addr`选项。

**default**: `'127.0.0.1:8000'`

参考: [site_url](#site_url).

## 格式化选项

### markdown_extensions

MkDocs使用[Python Markdown][pymkd]库将Markdown文件转换为HTML。Python Markdown支持多种[extensions][pymdk-extensions]，可自定义页面的格式。此设置允许您使用MkDocs默认扩展之外的扩展列表(`meta`, `toc`, `tables`, 和 `fenced_code`)。

例如，启用[SmartyPants typography extension][smarty], 使用:

```yaml
markdown_extensions:
    - smarty
```

一些扩展提供了自己的配置选项。如果要设置任何配置选项，可以以键/值对（`option_name: option value`）的方式嵌套该扩展支持的任何选项。请参阅您正在使用的扩展的文档，以确定它们支持哪些选项。


例如，要启用`toc`扩展中的永久链接，请使用：

```yaml
markdown_extensions:
    - toc:
        permalink: True
```

注意，冒号(`:`)必须跟在扩展名(`toc`)后面，然后在新行上，选项名称和值必须缩进并用冒号分隔。如果要为单个扩展定义多个选项，则必须在单独的行上定义每个选项：

```yaml
markdown_extensions:
    - toc:
        permalink: True
        separator: "_"
```

每个扩展都添加到扩展列表中。如果没有为该扩展设置的配置项，那么省略即可：

```yaml
markdown_extensions:
    - smarty
    - toc:
        permalink: True
    - sane_lists
```

在上面的示例中，每个扩展都是一个列表项（以`-`开头）。作为替代方案，可以使用键/值对。但是，在这种情况下，必须为未定义选项的扩展提供空值。因此，上述最后一个示例也可以定义如下：

```yaml
markdown_extensions:
    smarty: {}
    toc:
        permalink: True
    sane_lists: {}
```
如果您打算通过[inheritance]覆盖某些选项，则需要使用此替代语法。

> 注意: **请参考:**
>
> Python-Markdown文档提供了一个开箱即用的[扩展列表][exts]。有关给定扩展的可用配置选项列表，请参阅该扩展的文档。
>
> 您还可以安装和使用各种[第三方扩展][3rd]。有关安装说明和可用配置选项，请参阅这些扩展提供的文档。

**default**: `[]` (空列表).

### hooks

新特性: **New in version 1.4.**

设置由[plugin](#plugins)实例加载并使用的Python脚本的路径列表（路径是`mkdocs.yml`的相对路径）。

例如:

```yaml
hooks:
    - my_hooks.py
```

然后，文件*my_hooks.py*可以包含任何[插件事件处理器](../dev-guide/plugins.md#events),(除了`self`) ，例如:

```python
def on_page_markdown(markdown, **kwargs):
    return markdown.replace('a', 'z')
```

> ***样例***: 
>
> 根据Markdown内容生成警告（在[strict](#strict)模式下警告是致命的）:
>
> ```python
> import logging, re
> import mkdocs.plugins
>
> log = logging.getLogger('mkdocs')
>
> @mkdocs.plugins.event_priority(-50)
> def on_page_markdown(markdown, page, **kwargs):
>     path = page.file.src_uri
>     for m in re.finditer(r'\bhttp://[^) ]+', markdown):
>         log.warning(f"Documentation file '{path}' contains a non-HTTPS link: {m[0]}")
> ```

与[plugins][]相比，这并没有启用任何新功能，它只是简化了一次性使用，因为这些功能不像插件那样需要`安装` 。

注意，对于`mkdocs serve`，钩子模块不会在每次构建时重新加载。

如果使用标准方法名称,您可能在[mkdocs-simple-hooks plugin](https://github.com/aklajnert/mkdocs-simple-hooks) 中看到了此功能, 例如：

```diff
-plugins:
-  - mkdocs-simple-hooks:
-      hooks:
-        on_page_markdown: 'my_hooks:on_page_markdown'
+hooks:
+  - my_hooks.py
```

### 插件

构建站点时要使用的插件列表（带有可选配置项）。有关详细信息，请参阅[Plugins]文档。

如果在`mkdocs.yml`配置文件中定义了`plugins`配置项，则会忽略任何默认值（如`search`），如果您想继续使用它们，则需要显式重新启用默认值：

```yaml
plugins:
    - search
    - your_other_plugin
```

要给插件定义配置项，可以使用一组嵌套的键/值对：

```yaml
plugins:
    - search
    - your_other_plugin:
        option1: value
        option2: other value
```

在上面的示例中，每个插件都是一个列表项（以`-`开头）。作为替代方案，可以使用键/值对。但是，在这种情况下，必须为未定义选项的插件提供空值。因此，上述最后一个示例也可以定义如下：

```yaml
plugins:
    search: {}
    your_other_plugin:
        option1: value
        option2: other value
```

如果您打算通过[inheritance]覆盖某些选项，则需要使用此替代语法。

要完全禁用所有插件（包括任何默认值），请将`plugins`配置项设置为空列表：

```yaml
plugins: []
```

**default**: `['search']` (MkDocs附带的"search"插件).

#### Search

MkDocs默认提供了一个搜索插件，它使用[lunr.js]作为搜索引擎。以下配置选项可用于更改搜索插件的行为：

##### **separator**

一个正则表达式，它与构建索引时用作单词分隔符的字符相匹配。默认情况下，使用空格和连字符（`-`）。要添加点（`.`）作为单词分隔符，可以执行以下操作：

```yaml
plugins:
    - search:
        separator: '[\s\-\.]+'
```

**default**: `'[\s\-]+'`

##### **min_search_length**

定义搜索查询的最小长度的整数值。默认情况下，长度小于3个字符的搜索将被忽略，因为短搜索项的搜索结果质量很差。但是，对于某些场景又需要设置一个较短的长度（例如：搜索文档中有关`MQ`的文档）。

```yaml
plugins:
    - search:
        min_search_length: 2
```

**default**: 3

##### **lang**

在构建搜索索引时使用的语言列表，由[ISO 639-1]语言代码标识。使用[Lunr Languages]，支持以下语言：

* `ar`: Arabic
* `da`: Danish
* `nl`: Dutch
* `en`: English
* `fi`: Finnish
* `fr`: French
* `de`: German
* `hu`: Hungarian
* `it`: Italian
* `ja`: Japanese
* `no`: Norwegian
* `pt`: Portuguese
* `ro`: Romanian
* `ru`: Russian
* `es`: Spanish
* `sv`: Swedish
* `th`: Thai
* `tr`: Turkish
* `vi`: Vietnamese

你也可以[贡献其他语言].

警告:
虽然搜索能同时支持多种语言，但最好不要这么做，除非确实需要。每增加一种语言都会增加大量资源消耗。通常，最好将MkDocs的每个实例设置为一种语言。

注意:
Lunr语言目前不支持中文或其他亚洲语言。然而，一些用户使用日语效果不错。

**default**: 设置了`theme.locale`的值，否则为`[en]`。

##### **prebuild_index**

生成所有页面的预建索引，该项为可选项。这为大型站点提供了一些性能改进。在启用之前，请确保使用的主题明确支持预建索引（内置主题支持）。设置为`true`以启用。

警告:
This option requires that [Node.js] be installed and the command `node` be
on the system path. If the call to `node` fails for any reason, a warning
is issued and the build continues uninterrupted. You may use the `--strict`
flag when building to cause such a failure to raise an error instead.
此选项要求安装[Node.js]，并且将`node`程序添加到系统路径上。如果执行`node`命令失败，则会发出警告，并且构建将不停地继续。您可以在构建时使用`--strict`标志，但引发错误时直接导致失败。

注意:
在较小的站点上，不建议使用预先构建索引，因为他会消耗很多资源，而对用户几乎没有明显的改善。然而，对于较大的站点（数百页），资源消耗相对较小，用户的搜索性能也有显著提高。

**default**: `False`

##### **indexing**

配置搜索索引器在为页面构建索引时使用的策略。如果项目规模较大，并且索引占用大量磁盘空间时，则此属性特别有用。

```yaml
plugins:
    - search:
        indexing: 'full'
```

###### 选项

|选项|描述|
|------|-----------|
|`full`|索引每页的标题、段落标题和全文|
|`sections`|索引每页的标题、段落标题|
|`titles`|索引每页的标题|

**default**: `full`

## 环境变量

在大多数情况下，配置选项的值直接在配置文件中设置。但是，作为一个选项，可以使用`!ENV`标记。例如，要将`site_name` 选项的值设置为变量`SITE_NAME`的值，YAML文件可以这样写：

```yaml
site_name: !ENV SITE_NAME
```

如果未定义环境变量，则将为配置设置分配一个`null`（或Python中的`None`）值。也可以设置一个默认值。如下：

```yaml
site_name: !ENV [SITE_NAME, 'My default site name']
```

也可以使用多个环境变量。请注意，最后一个值不是环境变量，但必须是一个可以作为默认值的值，当未定义任何环境变量时使用。

```yaml
site_name: !ENV [SITE_NAME, OTHER_NAME, 'My default site name']
```

在环境变量中定义的简单类型（如string、bool、integer、float、datestamp和null）可以直接被解析为YAML文件中定义的类型。但是，列表和键/值对等复杂类型不能在单个环境变量中定义。

如果想查看更多信息, 请参考[pyyaml_env_tag](https://github.com/waylan/pyyaml-env-tag)

## 配置继承

通常，一个文件可以保存站点的整个配置。但是，有些组织可能会维护多个站点，这些站点都共享一个相同的配置。公共配置选项可以在父配置文件中定义，而不是在每个站点各自的配置文件中定义。

要定义配置文件的父配置文件，请将`INHERIT`（全大写）键设置为父配置文件的路径。路径必须相对于当前配置文件的位置。

对于要与父配置合并的配置选项，这些选项必须定义为键/值对。具体来说，[markdown_extensions]和[plugins](#plugins)选项必须使用列表项的替代语法（使用`{}`的格式）。

例如，假设公共（父）配置定义在`base.yml`中：

```yaml
theme:
    name: mkdocs
    locale: en
    highlightjs: true
markdown_extensions:
    toc:
        permalink: true
    admonition: {}
```

然后，对于"foo" 站点，主配置文件定义在`foo/mkdocs.yml`:

```yml
INHERIT: ../base.yml
site_name: Foo Project
site_url: https://example.com/foo
```

运行`mkdocs build`时，`foo/mkdocs.yml`文件将作为配置文件传入。然后，MkDocs将解析该文件，检索并解析父文件`base.yml`，并将两者深度合并。这将导致MkDocs接收以下合并配置：

```yaml
site_name: Foo Project
site_url: https://example.com/foo
theme:
    name: mkdocs
    locale: en
    highlightjs: true
markdown_extensions:
    toc:
        permalink: true
    admonition: {}
```

深度合并允许您在主配置文件中添加或覆盖各种值。例如，假设您想为一个站点添加对列表的支持，为永久链接使用不同的符号，并定义不同的分隔符。在该站点的主配置文件中，您可以执行以下操作：

```yaml
INHERIT: ../base.yml
site_name: Bar Project
site_url: https://example.com/bar
markdown_extensions:
    def_list: {}
    toc:
        permalink: 
        separator: "_"
```

在这种情况下，上述配置将与`base.yml`深度合并，并生成以下配置：

```yaml
site_name: Bar Project
site_url: https://example.com/bar
theme:
    name: mkdocs
    locale: en
    highlightjs: true
markdown_extensions:
    def_list: {}
    toc:
        permalink: 
        separator: "_"
    admonition: {}
```

请注意，`admonition`扩展保留了父配置中的值，添加了`def_list`扩展名、替换了`toc.permalink`的值，并添加了`toc.separator`的值。

您可以替换或合并任何键的值。但是，任何非键都会被替换。因此，不能将新列表项追加到列表中。必须重新定义整个列表。

由于[nav]配置由嵌套列表组成，这意味着您无法合并导航项。当然，您可以用新的配置替换整个`nav`配置。但是，通常整个导航一般定义在项目的主配置文件中。

警告:
需要提醒的是，所有基于路径的配置选项都必须是主配置文件的相对路径，合并时MkDocs不会更改路径。因此，在由多个不同站点继承的父文件中定义路径可能无法生效。通常最好在主配置文件中定义跟路径相关的选项。

[主题开发人员指南]: ../dev-guide/themes.md
[pymdk-extensions]: https://python-markdown.github.io/extensions/
[pymkd]: https://python-markdown.github.io/
[smarty]: https://python-markdown.github.io/extensions/smarty/
[exts]: https://python-markdown.github.io/extensions/
[3rd]: https://github.com/Python-Markdown/markdown/wiki/Third-Party-Extensions
[配置页面和导航]: write-docs.md#配置页面和导航
[元数据]:write-docs.md#元数据
[theme_dir]: custom-theme.md#using-the-theme_dir
[选择主题]: choose-theme.md
[本地化主题]: localize-theme.md
[自定义主题]: custom-theme.md
[extra_css]: #extra_css
[Plugins]: ../dev-guide/plugins.md
[lunr.js]: https://lunrjs.com/
[ISO 639-1]: https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
[Lunr Languages]: https://github.com/MihaiValentin/lunr-languages#lunr-languages-----
[贡献其他语言]: https://github.com/MihaiValentin/lunr-languages/blob/master/CONTRIBUTING.md
[Node.js]: https://nodejs.org/
[markdown_extensions]: #markdown_extensions
[nav]: #nav
[inheritance]: #configuration-inheritance