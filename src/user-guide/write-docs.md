# 编写文档

## 文件布局

文档使用Markdown文件编写（请参考下面的[使用Markdown编写](#使用markdown编写)），并放在文档目录中。默认情况下，该目录将命名为`docs`，并位于项目的根目录，与`mkdocs.yml`配置文件一起。

最简单的项目如下面所示：
```console
mkdocs.yml
docs/
    index.md
```

按照惯例，项目主页应该命名为`index.md`（详细信息请参见下面的[索引页面](#索引页面)）。
以下任何文件扩展名都可以用于Markdown源文件：`markdown`、`mdown`、`mkdn`、`mkd`、`md`。在没有特殊设置情况下，文档目录中包含的所有Markdown文件都将在站点中展现。

>***注意***
MkDocs会忽略以点开头的文件名和目录名（例如：`.foo.md`或`.bar/baz.md`），这与大多数web服务器的规则类似。没有覆盖此行为的选项。

可以通过创建多个Markdown文件来创建多页面文档：
```console
mkdocs.yml
docs/
    index.md
    about.md
    license.md
```
使用的文件布局决定了用于生成页面的URL。给定上述布局，将生成以下URL的页面：
```
/
/about/
/license/
```

如果有利于文档布局，还可以将Markdown文件嵌套到目录中。
```
docs/
    index.md
    user-guide/getting-started.md
    user-guide/configuration-options.md
    license.md
```
嵌套目录中的源文件将导致生成嵌套URL的页面，如下所示：
```
/
/user-guide/getting-started/
/user-guide/configuration-options/
/license/
```
MkDocs会将文档目录中的非Markdown文件（按文件扩展名）的任何文件原封不动地复制到构建站点。有关详细信息，请参阅以下如何链接到图像和媒体。

### 索引页面

当请求目录时，默认情况下，大多数web服务器将返回包含在该目录中的索引文件（通常命名为`index.html`）。因此，上面所有示例中的索引文件都被命名为`index.md`，MkDocs在构建网站时会将其呈现为`index.html`。


许多代码仓库在浏览目录时通常显示README文件的内容。因此，MkDocs允许将主页命名为`README.md`而不是`index.md`。这样，当用户浏览源代码时，就可以显示该目录的`README.md`，因为它是一个README文件。然而，当MkDocs展示站点时，该文件又被重命名为`index.html`，以便服务器将其作为适当的索引文件。

如果在同一目录中同时找到`index.md`文件和`README.md`文件，则使用`index.md`文件，并忽略`README.md`文件。

### 配置页面和导航

`mkdocs.yml`文件中的`nav`配置项定义了全局站点导航菜单中包含的页面以及该菜单的结构。如果未提供，将通过查找文档目录中的所有Markdown文件自动创建导航。自动创建的导航配置将始终按文件名的字母数字进行排序（除索引文件）。如果希望导航按不同的菜单排序，则需要手动定义导航配置。

最小导航配置如下所示：
```yaml
nav:
    - 'index.md'
    - 'about.md'
```

导航配置中的所有路径都是`docs_dir`配置项的相对路径。如果该选项设置为默认值`docs`，则上述配置的源文件将位于`docs/index.md`和`docs/about.md`。

以上示例将会在导航栏创建两个菜单项，其标题从Markdown文件的内容中推断，或者如果文件中未定义标题，则从文件名中推断。如果要覆盖导航设置的标题，请在文件名之前添加标题。
```yaml
nav:
    - Home: 'index.md'
    - About: 'about.md'
```
请注意，如果在导航中为页面定义了标题，则该标题将在该页面的整个站点中使用，并将覆盖页面本身中定义的任何标题。

可以通过在菜单标题下列出其他相关页面来创建子菜单。例如：
```yaml
nav:
    - Home: 'index.md'
    - 'User Guide':
        - 'Writing your docs': 'writing-your-docs.md'
        - 'Styling your docs': 'styling-your-docs.md'
    - About:
        - 'License': 'license.md'
        - 'Release Notes': 'release-notes.md'
```

通过以上配置，我们有三个顶级菜单：`Home`、`User Guide`和`About`。`Home`是网站主页的链接。在`User Guide`部分，列出了两个子菜单：`Writing your docs`和`Styling your docs`。在`About`部分，又列出了两个子菜单：`License`和`Release Notes`。

请注意，不能为分区指定页面。分区仅是子菜单和子分区的容器。您可以根据自己的喜好将分区嵌套得更深，这样会使得嵌套过于复杂，影响用户体验。

导航配置中未列出的任何页面仍将呈现并包含在构建的网站中，但是，它们不会从全局导航中链接，也不会包含在`上一个`和`下一个`链接中。除非直接链接到，否则此类页面将被"隐藏"。

## 使用Markdown编写

MkDocs页面必须使用Markdown编写，Markdown是一种轻量级的标记语言，可以生成易于阅读、易于编写的纯文本文档，并可以以可预测的方式转换为有效的HTML文档。

MkDocs使用[`Python-Markdown`][Python-Markdown]库将Markdown文档渲染为HTML。`Python-Markdown`几乎完全符合Markdown[参考实现]，尽管有一些非常小的[差异]。

除了支持Markdown的[基本语法]外，MkDocs还支持使用`Python-Markdown`[扩展]来延展Markdown语法。
有关如何开启扩展的详细信息，请参见MkDocs的`markdown_extensions`配置项。

MkDocs默认包含一些扩展，如下所示。

[Python-Markdown]:https://python-markdown.github.io/
[参考实现]:https://daringfireball.net/projects/markdown/
[差异]:https://python-markdown.github.io/#differences
[基本语法]:https://daringfireball.net/projects/markdown/syntax
[扩展]:https://python-markdown.github.io/extensions/
[markdown_extensions]:https://www.mkdocs.org/user-guide/configuration/#markdown_extensions

### 内部链接

MkDocs可以使用常规Markdown[链接]来链接文档。然而，针对MkDocs格式化这些链接还有一些其他的好处，如下所述。

#### 链接到页面

在文档中的页面之间进行链接时，您可以简单地使用常规Markdown[链接]语法，包括要链接到的Markdown文档的`相对路径`。

```markdown
Please see the [project license](license.md) for further details.
```

当MkDocs构建时，这些Markdown链接将自动转换为指向相应HTML页面的HTML超链接。


>***警告***
>官方不支持使用带有链接的绝对路径。MkDocs会调整相对路径，以确保它们始终相对于页面。绝对路径不会被修改。
>这意味着使用绝对路径的链接可能在本地环境中运行良好，但一旦将它们部署到生产服务器，它们可能就找不到了。

如果目标文档文件位于另一个目录中，则需要确保在链接中包含任何相对目录路径。

```markdown
Please see the [project license](../about/license.md) for further details.
```

[toc]扩展用于为Markdown文档中的每个标题生成一个ID。
使用该ID以锚链接的方式链接到目标文档中的标题。生成的HTML将正确转换链接的路径部分，并保持锚链接部分不变。

```markdown
Please see the [project license](about.md#license) for further details.
```

***注意:***
ID是根据标题的文本创建的。所有文本都将转换为小写，所有不允许的字符（包括空格）都转换为破折号。然后将连续的破折号减少为单个破折号。
`toc`扩展提供了一些配置项，可以在`mkdocs.yml`配置文件中设置这些值来更改默认行为：

- **`permalink`**  

  在每个标题的末尾生成永久链接。默认值：`False`。
  设置为True时，将使用段落符号(&para; 或 `&para;`)作为链接文本。当设置为字符串时，提供的字符串将用作链接文本。
  例如，要改用哈希符号(`#`)，执行以下操作：
  ```yaml
  markdown_extensions:
    - toc:
        permalink: "#"
  ```
- **`baselevel`**

  标题的基本级别。默认值：`1`。  
  此设置允许自动调整标题级别以适应HTML模板的层次结构。例如，如果页面的Markdown文本不应包含任何高于级别2 (`<h2>`)的标题，执行以下操作：
  ```yaml
  markdown_extensions:
    - toc:
        baselevel: 2
  ```
  然后，文档中的任何标题都将增加1。例如，标题`#header`将在HTML输出中呈现为2级标题（`<h2>`）。
  
- **`separator`**

  单词分隔符。默认值：`-`。  
  替换生成的ID中空白的字符。如果您更喜欢下划线，请执行以下操作：
  ```yaml
  markdown_extensions:
    - toc:
        separator: "_"
  ```
  
如果您想定义多个以上的设置，则必须在`markdown_extensions`配置项的单个toc条目下进行定义。

```yaml
markdown_extensions:
    - toc:
        permalink: "#"
        baselevel: 2
        separator: "_"
```


[链接]:https://daringfireball.net/projects/markdown/syntax#link
[toc]:https://python-markdown.github.io/extensions/toc/

#### 链接到图片和多媒体资源

除了Markdown源文件，还可以在文档中引入其他类型的文件，这些文件在生成文档站点时会复制到输出目录下。这些文件包括图像和其他媒体资源。

例如，如果项目文档需要包含[GitHub页面CNAME文件]和PNG格式的屏幕截图，那么文件布局可能如下所示：

```console
mkdocs.yml
docs/
    CNAME
    index.md
    about.md
    license.md
    img/
        screenshot.png
```

要在文档中包含图像，只需使用Markdown常规图像语法：

```markdown
Cupcake indexer is a snazzy new project for indexing small cakes.

![Screenshot](img/screenshot.png)

*Above: Cupcake indexer in progress*
```

现在，当您构建文档时，您的图像将被嵌入，如果您使用Markdown编辑器处理文档，也应该能够预览图像。

[GitHub页面CNAME文件]:https://help.github.com/articles/using-a-custom-domain-with-github-pages/

#### 从原始HTML链接

Markdown允许文档在Markdown语法不满足规范时返回原始HTML。MkDocs在这方面不限制Markdown。然而，由于Markdown解析器忽略了所有原始HTML，MkDocs无法验证或转换原始HTML中包含的链接。在原始HTML中包含内部链接时，需要为呈现的文档手动设置适当的链接格式。

### 元数据

MkDocs同时支持`YAML`和`MultiMarkdown`样式的元数据（通常称为front-matter）。
元数据由一系列在Markdown文档开头定义的关键字和值组成，这些关键字和值在`Python-Markdown`处理之前从文档中剥离。
键/值对由MkDocs传递到页面模板。因此，如果主题支持，则任何键的值都可以显示在页面上或用于控制页面呈现。有关可能支持哪些键的信息，请参阅主题文档。

除了在模板中显示信息外，MkDocs还支持一些预定义的元数据键，这些键可以改变MkDoc在特定页面上的行为。支持以下键：

-  **`template`**

	用于当前页面的模板。

	默认情况下，MkDocs使用主题的`main.html`模板来呈现Markdown页面。您可以使用`template`元数据键为该特定页面定义不同的模板文件。模板文件必须在主题环境中定义的路径上可用。
	
- **`title`**

	用于文档的"标题"。

	MkDocs将尝试用下列方式确定文档标题：

    1. 在文档的[nav]配置中定义的标题。
    2. 在文档的`title`元数据键中定义的标题。
    3. 文档正文第一行上的1级Markdown标题。请注意，不支持[Setext style]标头。
    4. 文档的文件名.

    找到页面标题后，MkDoc不会继续检查上述列表中的任何其他来源。

[Setext-style]: https://daringfireball.net/projects/markdown/syntax#header

#### YAML样式元数据

YAML样式的元数据由[YAML]键/值对组成，这些键值对封装在YAML样式分隔符中，以标记元数据的开始和结束。
文档的第一行必须是`---`。结束分隔符是`---`或`…`。分隔符之间的内容解析为[YAML]。

```text
---
title: My Document
summary: A brief description of my document.
authors:
    - Waylan Limberg
    - Tom Christie
date: 2018-07-10
some_url: https://example.com
---
This is the first paragraph of the document.
```

YAML能够检测数据类型。因此，在上面的示例中，`title`、`summary`和`some_url`的值是字符串，`authors`的值是一个字符串列表，`date`的值是`datetime.date`对象。
注意，YAML键区分大小写，MkDocs希望键都是小写的。YAML的顶层必须是键/值对的集合，这将导致返回Python `dict`类型。
如果返回任何其他类型或YAML解析器遇到错误，则MkDocs不会将该配置识别为元数据，页面的`meta`属性将为空，并且不会从文档中删除该部分。

#### MultiMarkdown样式元数据

MultiMarkdown样式的元数据使用[MultiMarkdown]项目首次引入的格式。数据由Markdown文档开头定义的一系列关键字和值组成，如下所示：

```text
Title:   My Document
Summary: A brief description of my document.
Authors: Waylan Limberg
         Tom Christie
Date:    January 23, 2018
blank-value:
some_url: https://example.com

This is the first paragraph of the document.
```
元数据的`键`不区分大小写，可以由字母、数字、下划线和破折号组成，并且必须以冒号结尾。
值由冒号后面的任何内容组成，甚至可以为空。
如果一行缩进了4个或更多空格，则该行被认为是上一个键值的附加行。键值可以有任意多的行。最终所有行都拼接到一个字符串中。
第一个空行结束文档的所有元数据。因此，文档的第一行不能为空。

>***注意***
>
>MkDocs不支持在`MultiMarkdown`样式元数据中使用YAML样式分隔符（`---`或`…`）。
>事实上，MkDocs通过分隔符的存在与否来判断是否使用了`YAML`样式的元数据或`MultiMarkdown`样式的元数据。
>如果检测到分隔符，但分隔符之间的内容不是有效的`YAML`元数据，MkDocs不会尝试将内容解析为`MultiMarkdown`样式的元数据。


[YAML]: http://yaml.org
[MultiMarkdown]: http://fletcherpenney.net/MultiMarkdown_Syntax_Guide#metadata
[nav]: configuration.md#nav


### 表格

[tables]扩展为Markdown添加了一个基本的表格语法，该语法在多个实现中都很通用。语法相当简单，但只支持一些简单的表格数据。

一个简单的表格如下：

```markdown
First Header | Second Header | Third Header
------------ | ------------- | ------------
Content Cell | Content Cell  | Content Cell
Content Cell | Content Cell  | Content Cell
```

可以向表格的每一行开头和结尾添加管道符：

```markdown
| First Header | Second Header | Third Header |
| ------------ | ------------- | ------------ |
| Content Cell | Content Cell  | Content Cell |
| Content Cell | Content Cell  | Content Cell |
```

通过在分隔线中添加冒号来指定每列的对齐方式：

```markdown
First Header | Second Header | Third Header
:----------- |:-------------:| -----------:
Left         | Center        | Right
Left         | Center        | Right
```

***注意***，表格单元格不能包含任何块级元素，也不能包含多行文本。然而，它们可以包括Markdown[语法]规则中定义的内联Markdown。

此外，表格必须用空行包围。表格前后必须有一个空行。

[tables]: https://python-markdown.github.io/extensions/tables/
[语法]: https://daringfireball.net/projects/markdown/syntax

### 代码块

[fenced code blocks]扩展添加了一种定义代码块而不缩进的替代方法。

第一行应包含3个或更多的反引号（\`）字符，最后一行应包含相同数量的反引号字符（\`）：

````markdown
```
Fenced code blocks are like Standard
Markdown’s regular code blocks, except that
they’re not indented and instead rely on
start and end fence lines to delimit the
code block.
```
````

使用这种方法，可以在反引号后的第一行指定代码块的语言，以提示按该语言显示语法高亮：

````markdown
```python
def fn():
    pass
```
````

注意，隔离代码块不能缩进。因此，它们不能嵌套在列表项、块引号等内。

[fenced code blocks]: https://python-markdown.github.io/extensions/fenced_code_blocks/