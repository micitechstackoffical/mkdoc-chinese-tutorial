# 选择主题

MkDocs包括两个内置主题([mkdocs](#mkdocs)和[readthedocs](#readthedocs))，如下所述。然而，许多[第三方主题]也可供选择。

要选择主题，请在`mkdocs.yml`配置文件中设置`theme`配置选项。

```yaml
theme:
    name: readthedocs
```

## mkdocs

这是默认主题，作为自定义[Bootstrap]主题构建的，它支持MkDocs的大部分功能。

![](../images/mkdocs.png)

除了默认的[主题配置选项][theme]外，mkdocs主题还支持以下选项：

- __`highlightjs`__: 使用[highlight.js]JavaScript库在代码块中高亮显示源代码。默认值：`True`。

- __`hljs_style`__: highlight.js库提供了79种不同的[样式]，用于在代码块中高亮显示源代码。将其设置为所需样式的名称。默认值：`github`。

- __`hljs_languages`__: 默认情况下，highlight.js仅支持23种常用语言。在此列出其他语言以包括对它们的支持。

    ```yaml
    theme:
        name: mkdocs
        highlightjs: true
        hljs_languages:
            - yaml
            - rust
    ```
- __`analytics`__: 定义分析服务的配置选项。目前，通过`gtag`选项仅支持Google Analytics v4。

    - __`gtag`__: 要启用Google Analytics，请使用`G-`格式设置Google Analytics v4的跟踪ID。请参阅Google文档 [Set up Analytics for a website and/or app (GA4)][setup-GA4] 或
    [Upgrade to a Google Analytics 4 property][upgrade-GA4]。

        ```yaml
        theme:
            name: mkdocs
            analytics:
                gtag: G-ABC123
        ```

        当设置为默认值（null）时，将禁用站点的Google Analytics。
		
- __`shortcuts`__: 定义快捷键。

    ```yaml
    theme:
        name: mkdocs
        shortcuts:
            help: 191    # ?
            next: 78     # n
            previous: 80 # p
            search: 83   # s
    ```

    所有值必须是数字键编码。最好使用所有键盘上都可用的键。您可以访问<https://keycode.info/>以确定给定快捷键的编码。

    - __`help`__: 显示所有快捷键. 默认: `191` (&quest;)

    - __`next`__: 导航到"下一个"页面. 默认: `78` (n)

    - __`previous`__: 导航到"上一个"页面. 默认: `80` (p)

    - __`search`__: 显示搜索框. 默认: `83` (s)
	
	
- __`navigation_depth`__: 侧边栏中导航树的最大深度。默认: `2`.

- __`nav_style`__: 这将调整顶部导航栏的视觉样式；默认情况下，它设置为`primary`（默认值），但也可以设置为`dark` 或 `light`。

    ```yaml
    theme:
        name: mkdocs
        nav_style: dark
    ```

- __`locale`__{ #mkdocs-locale }: 用于构建主题的区域设置（语言/位置）。如果您的区域尚不受支持，将使用默认设置。

    此主题支持以下区域设置:

    - `en`: English (default)
    - `de`: German
    - `es`: Spanish
    - `fa`: Persian (Farsi)
    - `fr`: French
    - `it`: Italian
    - `ja`: Japanese
    - `nb`: Norwegian Bokmål
    - `nn`: Norwegian Nynorsk
    - `pt_BR`: Portuguese (Brazil)
    - `ru`: Russian
    - `tr_TR`: Turkish (Turkey)
    - `uk`: Ukrainian
    - `zh_CN`: Simplified Chinese

    有关详细信息，请参阅[主题本地化]指南。

## readthedocs

该主题是默认主题的克隆，[Read the Docs]服务在使用。该服务提供与其父主题相同的受限功能集，只支持两个级别的导航。

![](../images/readthedocs.png)

除了默认的[主题配置选项][theme]外，`readthedocs`主题还支持以下选项：

- __`highlightjs`__: 使用[highlight.js]JavaScript库在代码块中高亮显示源代码。默认值：`True`。

- __`hljs_languages`__: 默认情况下，highlight.js仅支持23种常用语言。在此列出其他语言以包括对它们的支持。

    ```yaml
    theme:
        name: mkdocs
        highlightjs: true
        hljs_languages:
            - yaml
            - rust
    ```
- __`analytics`__: 定义分析服务的配置选项。目前，通过`gtag`选项仅支持Google Analytics v4。

    - __`gtag`__: 要启用Google Analytics，请使用`G-`格式设置Google Analytics v4的跟踪ID。请参阅Google文档 [Set up Analytics for a website and/or app (GA4)][setup-GA4] 或
    [Upgrade to a Google Analytics 4 property][upgrade-GA4]。

        ```yaml
        theme:
            name: mkdocs
            analytics:
                gtag: G-ABC123
        ```

        当设置为默认值（null）时，将禁用站点的Google Analytics。
	- __`anonymize_ip`__: 为Google Analytics启用匿名IP地址, 设置为：`True`. 默认为: `False`.

- __`include_homepage_in_sidebar`__: 在侧边栏菜单中列出主页。由于MkDocs要求在`nav`配置项中列出主页，因此该设置允许在侧边栏中包含或排除主页。请注意，网站名称/Logo始终链接到主页。默认值：`True`。

- __`prev_next_buttons_location`__: 值为 `bottom`, `top`, `both` , 或 `none`。`下一个` 和 `上一个` 按钮的显示位置。 默认: `bottom`.

- __`navigation_depth`__: 侧边栏中导航树的最大深度。默认: `4`.

- __`collapse_navigation`__: 仅在当前页面的侧边栏中包含页面节标题。默认: `True`.

- __`titles_only`__: 仅在侧边栏中包含页面标题，不包括任何页面的任何段落标题。默认: `False`.

- __`sticky_navigation`__: 如果为`True`，则在滚动页面时使侧边栏与主页内容一起滚动。默认: `True`.

- __`locale`__{ #readthedocs-locale }: 用于构建主题的区域设置（语言/位置）。如果您的区域尚不受支持，将使用默认设置。

    此主题支持以下区域设置:

    * `en`: English (default)
    * `fr`: French
    * `es`: Spanish
    * `ja`: Japanese
    * `pt_BR`: Portuguese (Brazil)
    * `zh_CN`: Simplified Chinese
    * `de`: German
    * `fa`: Persian (Farsi)
    * `it`: Italian
    * `tr_TR`: Turkish (Turkey)
    * `ru`: Russian
    * `uk`: Ukrainian

    有关详细信息，请参阅[主题本地化]指南。

- __`logo`__: 要在项目上设置Logo而不是纯文本`site_name`，请将此变量设置为图像的位置。默认：`null`。


## 第三方主题

第三方主题列表可在MkDocs[社区wiki][community wiki]中找到。如果您已经创建了自己的，请随时将其添加到列表中。

[第三方主题]: #第三方主题
[theme]: configuration.md#theme
[Bootstrap]: https://getbootstrap.com/
[highlight.js]: https://highlightjs.org/
[样式]: https://highlightjs.org/static/demo/
[setup-GA4]: https://support.google.com/analytics/answer/9304153?hl=en&ref_topic=9303319
[upgrade-GA4]: https://support.google.com/analytics/answer/9744165?hl=en&ref_topic=9303319
[Read the Docs]: https://readthedocs.org/
[community wiki]: https://github.com/mkdocs/mkdocs/wiki/MkDocs-Themes
[主题本地化]: localize-theme.md

