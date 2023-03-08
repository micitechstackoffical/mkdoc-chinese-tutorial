# 命令行


## mkdocs

### 用法

``` shell
mkdocs [OPTIONS] COMMAND [ARGS]...
```
### 选项

| 名称 | 类型 | 描述 | 默认值 |
| ------------ | ------------- | ------------ | -------- |
| `-V`, `--version` | boolean  | 显示版本  |  `False`  |
| `-q`, `--quiet` | boolean    | 忽略警告  |  `False`  |
| `-v`, `--verbose` | boolean    | 显示日志输出  |  `False`  |
| `--help` | boolean    | 显示日志输出  |  `False`  |

### 子命令

- [build](#mkdocs-build): 构建MkDocs文档
- [gh-deploy](#mkdocs-gh-deploy): 将文档部署到GitHub页面
- [new](#mkdocs-new): 创建新的MkDocs工程
- [serve](#mkdocs-serve): 运行内置开发服务器

## mkdocs build
构建MkDocs文档

### 用法
``` shell
mkdocs build [OPTIONS]
```

### 选项

| 名称 | 类型 | 描述 | 默认值 |
| ------------ | ------------- | ------------ | -------- |
| `-c`, `--clean` / `--dirty` | boolean  | 在构建之前从site_dir中删除旧文件（默认）。  |  `True`  |
| `-f`, `--config-file` | filename    | 提供特定的MkDocs配置  |  `None`  |
| `-s`, `--strict` | boolean    | 启用严格模式。这将导致MkDocs根据任何警告中止构建。  |  `None`  |
| `-t`, `--theme` | 枚举 (mkdocs \| readthedocs)    | 指定构建文档的主题  |  `None`  |
| `--use-directory-urls`/ `--no-directory-urls` | boolean    | 构建页面时使用目录URL（默认）。  |  `None`  |
| `-d`, `--site-dir` | path    | 输出文档生成结果的目录。  |  `None`  |
| `-q`, `--quiet` | boolean    | 忽略警告  |  `False`  |
| `-v`, `--verbose` | boolean    | 显示日志输出  |  `False`  |
| `--help` | boolean    | 显示日志输出  |  `False`  |


## mkdocs gh-deploy
将文档部署到GitHub页面

### 用法
``` shell
mkdocs gh-deploy [OPTIONS]
```

### 选项

| 名称 | 类型 | 描述 | 默认值 |
| ------------ | ------------- | ------------ | -------- |
| `-c`, `--clean` / `--dirty` | boolean  | 在构建之前从site_dir中删除旧文件（默认）。  |  `True`  |
| `-m`, `--message` | text    | 提交到GitHub Pages远程分支时使用的提交消息。Commit｛sha｝和MkDocs｛version｝作为扩展提供  |  `None`  |
| `-b`, `--remote-branch` | text    | 要提交到GitHub Pages的远程分支。这将覆盖config中指定的值  |  `None`  |
| `-r`, `--remote-name` | text    | 要提交到GitHub Pages的远程名称。这将覆盖config中指定的值  |  `None`  |
| `--force` | boolean    | 强制提交  |  `False`  |
| `--no-history` | boolean    | 用一个新提交替换整个Git历史记录  |  `False`  |
| `--ignore-version` | boolean    | 忽略检查是否使用旧版本部署  |  `False`  |
| `--shell` | boolean    | 调用Git时使用shell  |  `False`  |
| `-f`, `--config-file` | filename    | 提供特定的MkDocs配置  |  `None`  |
| `-s`, `--strict` | boolean    | 启用严格模式。这将导致MkDocs根据任何警告中止构建。  |  `None`  |
| `-t`, `--theme` | 枚举 (mkdocs \| readthedocs)    | 指定构建文档的主题  |  `None`  |
| `--use-directory-urls`/ `--no-directory-urls` | boolean    | 构建页面时使用目录URL（默认）。  |  `None`  |
| `-d`, `--site-dir` | path    | 输出文档生成结果的目录。  |  `None`  |
| `-q`, `--quiet` | boolean    | 忽略警告  |  `False`  |
| `-v`, `--verbose` | boolean    | 显示日志输出  |  `False`  |
| `--help` | boolean    | 显示日志输出  |  `False`  |


## mkdocs new

创建新的MkDocs工程

### 用法
``` shell
mkdocs new [OPTIONS] PROJECT_DIRECTORY
```

### 选项

| 名称 | 类型 | 描述 | 默认值 |
| ------------ | ------------- | ------------ | -------- |
| `-q`, `--quiet` | boolean    | 忽略警告  |  `False`  |
| `-v`, `--verbose` | boolean    | 显示日志输出  |  `False`  |
| `--help` | boolean    | 显示日志输出  |  `False`  |

## mkdocs serve

运行内置开发服务器

### 用法
``` shell
mkdocs serve [OPTIONS]
```

### 选项

| 名称 | 类型 | 描述 | 默认值 |
| ------------ | ------------- | ------------ | -------- |
| `-a`,`--dev-addr` | text    | 本地提供文档的IP地址和端口（默认值：localhost:8000）  |  `None`  |
| `--livereload` | text    | 在开发服务器中启用实时重新加载（这是默认设置）。  |  `True`  |
| `--no-livereload` | text    | 禁用开发服务器中的实时重载。  |  `False`  |
| `--dirtyreload` | text    | 在开发服务器中启用实时重载，但仅重新生成已更改的文件  |  `False`  |
| `--watch-theme` | boolean    | 将主题包含在文件列表中，以监视变化时实时重载。未使用实时重载时忽略。  |  `False`  |
| `-w`, `--watch` | path    | 监视需要实时加载的目录或文件。可多次提供。  |  `[]`  |
| `-f`, `--config-file` | filename    | 提供特定的MkDocs配置  |  `None`  |
| `-s`, `--strict` | boolean    | 启用严格模式。这将导致MkDocs根据任何警告中止构建。  |  `None`  |
| `-t`, `--theme` | 枚举 (mkdocs \| readthedocs)    | 指定构建文档的主题  |  `None`  |
| `--use-directory-urls`/ `--no-directory-urls` | boolean    | 构建页面时使用目录URL（默认）。  |  `None`  |
| `-q`, `--quiet` | boolean    | 忽略警告  |  `False`  |
| `-v`, `--verbose` | boolean    | 显示日志输出  |  `False`  |
| `--help` | boolean    | 显示日志输出  |  `False`  |
