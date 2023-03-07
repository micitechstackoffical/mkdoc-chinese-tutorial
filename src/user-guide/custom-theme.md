# 自定义主题

根据自己的需求改变主题。

如果您想对现有主题进行一些调整，不需要从头开始创建自己的主题。只需要对CSS或JavaScript做一些小调整，您可以[使用docs_dir](#使用docs_dir)。但是，对于更复杂的定制化，比如需要覆盖模板，需要[使用主题custom_dir](#使用主题custom_dir)设置。

## 使用docs_dir

[extra_css]和[extra_javascript]配置选项可用于对现有主题进行调整和自定义。要使用这些，您只需在[文档目录]中包含CSS或JavaScript文件即可。

例如，要更改文档中标题的颜色，请创建一个名为`extra.css`的文件，并将其放在文档Markdown旁边。在该文件中添加以下CSS。

```css
h1 {
  color: red;
}
```

> 注意:
> 如果您正在使用[ReadTheDocs]主题部署文档。您需要明确列出要包含在配置文件中的CSS和JavaScript文件。为此，请将以下内容添加到mkdocs.yml中。
> 
> ```yaml
> extra_css: [extra.css]
> ```

进行这些更改后，当您运行`mkdocs serve`时，应该会看到CSS变更被自动加载，文档将被更新。

注意:
任何额外的CSS或JavaScript文件都将添加到HTML页面内容之后。如果希望引入JavaScript库，那么可以通过使用主题[custom_dir]来包含该库可能会更好。

## 使用主题custom_dir

[`theme.custom_dir`][custom_dir]配置选项可用于指向覆盖父主题中文件的文件目录。父主题将是[`theme.name`][name]配置选项中定义的主题。父主题中与`custom_dir`中同名的任何文件都将被替换。
`custom_dir`中的任何其他文件都将添加到父主题中。`custom_dir`的内容应反映父主题的目录结构。主题中可能包含模板、JavaScript文件、CSS文件、图像、字体或任何其他多媒体。

注意:
要使该配置生效，必须将`theme.name`配置设置为已安装的主题。如果`name`设置改为`null` （或未定义），则没有要覆盖的主题，`custom_dir`的内容必须是完整的独立主题。有关详细信息，请参阅[主题开发人员指南][custom theme]。


例如，[mkdocs]主题([浏览源码][browse source])包含以下目录结构（部分）：

```nohighlight
- css\
- fonts\
- img\
  - favicon.ico
  - grid.png
- js\
- 404.html
- base.html
- content.html
- nav-sub.html
- nav.html
- toc.html
```

要覆盖该主题中包含的任何文件，在`docs_dir`同级目录下创建一个新目录：

```bash
mkdir custom_theme
```

然后将`mkdocs.yml`配置文件指向新目录：

```yaml
theme:
    name: mkdocs
    custom_dir: custom_theme/
```

要覆盖404错误页面（"找不到文件"），请将名为`404.html`的新模板文件添加到`custom_theme`目录中。有关模板中可以包含的内容的信息，请查看[主题开发人员指南][custom theme]。

要覆盖图标，可以在`custom_theme/img/favicon.ico`添加一个新的图标文件。

要包含JavaScript库，请将库复制到`custom_theme/js/`目录下。

您的目录结构现在应该如下所示:

```nohighlight
- docs/
  - index.html
- custom_theme/
  - img/
    - favicon.ico
  - js/
    - somelib.js
  - 404.html
- config.yml
```

注意:
包含在父主题(在`name`中定义)中但未包含在`custom_dir`中的任何文件仍将被使用。`custom_dir`仅覆盖父主题中的文件。如果你想删除文件，或者从头开始构建主题，那么你应该查看[主题开发人员指南][custom theme]。

### 覆盖模板块

内置主题中实现了许多模板块，可以在`main.html`模板中单独覆盖这些部分。只需在`custom_dir`中创建一个`main.html`模板文件，并在该文件中定义替换块。只需确保`main.html`扩展`base.html`即可。例如，要更改MkDocs主题的标题，替换的`main.html`模板将包含以下内容：

```django
{% extends "base.html" %}
{% block htmltitle %}
<title>Custom title goes here</title>
{% endblock %}
```

在上面的示例中，将使用自定义`main.html`文件中的`htmltitle`块来代替父主题中定义的默认`htmltitle`块。可以根据需要重新定义其他任意多个块，只要这些块是在父对象中定义的。例如，您可以将Google Analytics脚本替换为其他服务的脚本，或将搜索功能替换为您自己的脚本。您将需要查阅您正在使用的父主题，以确定哪些块可以覆盖。`MkDocs`和`ReadTheDocs`主题提供以下模块：

* `site_meta`: 在文档头中包含元标记。
* `htmltitle`: 包含文档标题中的页面标题。
* `styles`: 包含样式表的链接标记。
* `libs`: 包含页面标题中的JavaScript库（如jQuery等）。
* `scripts`: 包含加载页面后应执行的JavaScript脚本。
* `analytics`: 包含分析脚本。
* `extrahead`: `<head>`中的一个空块，用于插入自定义tags/scripts等。
* `site_name`: 包含导航栏中的站点名称。
* `site_nav`: 包含导航栏中的站点导航。
* `search_button`: 包含导航栏中的搜索框。
* `next_prev`: 包含导航栏中的下一个和上一个按钮。
* `repo`: 包含导航栏中的存储库链接。
* `content`: 包含页面内容和页面目录。
* `footer`: 包含页脚。


您可能需要查看源模板文件，以确保您的修改与网站的结构相吻合。有关可以在自定义块中使用的变量列表，请参见[模板变量]。有关块的更完整的解释，请参阅[Jinja文档]。

### 组合custom_dir和模板块

将JavaScript库添加到`custom_dir`下就可以使用，但不会将其包含在`MkDocs`生成的页面中。因此，需要从HTML向库添加一个链接。

使用上面的目录结构（截断一部分）：

```nohighlight
- docs/
- custom_theme/
  - js/
    - somelib.js
- config.yml
```

A link to the `custom_theme/js/somelib.js` file needs to be added to the
template. As `somelib.js` is a JavaScript library, it would logically go in the
`libs` block. However, a new `libs` block that only includes the new script will
replace the block defined in the parent template and any links to libraries in
the parent template will be removed. To avoid breaking the template, a
[super block] can be used with a call to `super` from within the block:
需要将指向`custom_theme/js/somelib.js`文件的链接添加到模板中。由于`somelib.js`是一个JavaScript库，因此它在逻辑上会放在`libs`块中。但是，包含在新脚本的新`libs` 块将替换父模板中定义的块，并且父模板中指向库的任何链接都将被删除。为了避免破坏模板，可以在块内调用`super()`,以使用[super block]：

```django
{% extends "base.html" %}
{% block libs %}
    {{ super() }}
    <script src="{{ base_url }}/js/somelib.js"></script>
{% endblock %}
```

注意，[base_url]模板变量用于确保链接始终相对于当前页面。

现在，生成的页面将包含指向模板提供的库以及`custom_dir`中包含的库的链接。对于`custom_dir`中包含的任何其他CSS文件，都需要相同的设置。

[custom theme]: ../dev-guide/themes.md
[extra_css]: ./configuration.md#extra_css
[extra_javascript]: ./configuration.md#extra_javascript
[文档目录]: ./configuration.md#docs_dir
[ReadTheDocs]: ./deploying-your-docs.md#readthedocs
[custom_dir]: ./configuration.md#custom_dir
[name]: ./configuration.md#name
[mkdocs]: ./choosing-your-theme.md#mkdocs
[browse source]: https://github.com/mkdocs/mkdocs/tree/master/mkdocs/themes/mkdocs
[模板变量]: ../dev-guide/themes.md#template-variables
[Jinja文档]: http://jinja.pocoo.org/docs/dev/templates/#template-inheritance
[super block]: http://jinja.pocoo.org/docs/dev/templates/#super-blocks
[base_url]: ../dev-guide/themes.md#base_url