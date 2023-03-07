# 本地化主题

用您喜欢的语言显示主题。

>***注意***:
>
>主题本地化仅翻译主题本身的文本元素（例如`下一个`和`上一个`链接），而不是文档的实际内容。如果您希望创建多语言文档，则需要将此处描述的`主题本地化`与`第三方国际化/本地化插件`相结合。

## 安装

要使主题本地化有效，必须使用支持它的主题，通过安装`mkdocs[i18n]`启用`i18n`（国际化）来支持：

```bash
pip install mkdocs[i18n]
```

## 支持的区域设置

在大多数情况下，区域设置由您语言的[ISO-639-1]（2个字母）缩写指定。然而，区域设置也可能包括地区(区域或国家)代码。
语言和地区必须用下划线分隔。例如，一些可能的英语语言环境可能包括`en`、`en_AU`, `en_GB`, 和 `en_US`。

有关所使用主题支持的区域设置列表，请参阅该主题的文档。

- [mkdocs]
- [readthedocs]

>**警告**:  
>如果您配置的语言区域该主题不支持，MkDocs将使用主题的默认区域设置。

## 用法

要指定MkDocs应使用的语言环境，请将[主题]配置选项的[locale]参数设置为适当的代码。

例如，要用法语构建`mkdocs`主题，您可以在`mkdocs.yml`配置文件中使用以下内容：

```yaml
 theme:
     name: mkdocs
     locale: fr
```

## 贡献主题翻译

如果主题尚未翻译成您的语言，请随时使用[翻译指南]进行翻译。

[翻译指南]: ../dev-guide/translations.md
[mkdocs]: choose-theme.md#mkdocs
[readthedocs]: choose-theme.md#readthedocs
[locale]: configuration.md#locale
[主题]: configuration.md#theme
[ISO-639-1]: https://en.wikipedia.org/wiki/ISO_639-1