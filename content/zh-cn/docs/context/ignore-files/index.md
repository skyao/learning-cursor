---
title: "忽略文件"
linkTitle: "忽略文件"
weight: 40
date: 2025-03-28
description: >
  了解如何使用 .cursorignore 和 .cursorindexingignore 在 Cursor 中控制文件访问和索引
---

## 概述

Cursor 提供了两个不同的忽略文件来控制文件的处理方式：

- `.cursorignore`：尽最大努力从 AI 功能和索引中排除文件

- `.cursorindexingignore`：仅控制为搜索和上下文索引哪些文件（与旧的 .cursorignore 相同）

## .cursorignore

.cursorignore 文件会尽最大努力将文件从 AI 功能和索引中排除。这对于以下情况很有用：

- 试图从 AI 访问和索引中排除敏感文件

- 排除包含机密的配置文件

- 限制对专有代码的访问

.cursorignore 中列出的文件将以最佳方式从 Cursor 的 AI 功能中排除：

- 不包含在标签页和聊天请求中

- 未包含在 AI 功能的上下文中

- 未为搜索或上下文功能编制索引

- 通过@-symbols 或其他上下文工具不可用

## .cursorindexingignore

.cursorindexingignore 文件仅控制为搜索和上下文功能索引哪些文件。这提供了与旧的 .cursorignore 相同的索引控件。当您需要执行以下操作时，请使用此文件：

- 从索引中删除生成的大型文件

- 跳过二进制文件的索引

- 控制代码库的哪些部分可搜索

- 优化索引性能

重要提示：.cursorindexingignore 中的文件仍然可以作为上下文手动包含或通过 AI 功能访问-它们不会自动索引或包含在搜索结果中。

### 默认索引忽略文件

仅对于索引，除了在 .gitignore、.cursorignore 和 .cursorindexignore 文件中指定的文件外，默认情况下还忽略以下文件。请注意，这些默认文件仅适用于索引，而不适用于其他 AI 功能。


```bash
package-lock.json
pnpm-lock.yaml
yarn.lock
composer.lock
Gemfile.lock
bun.lockb
.env*
.git/
.svn/
.hg/
*.lock
*.bak
*.tmp
*.bin
*.exe
*.dll
*.so
*.lockb
*.qwoff
*.isl
*.csv
*.pdf
*.doc
*.doc
*.xls
*.xlsx
*.ppt
*.pptx
*.odt
*.ods
*.odp
*.odg
*.odf
*.sxw
*.sxc
*.sxi
*.sxd
*.sdc
*.jpg
*.jpeg
*.png
*.gif
*.bmp
*.tif
*.mp3
*.wav
*.wma
*.ogg
*.flac
*.aac
*.mp4
*.mov
*.wmv
*.flv
*.avi
*.zip
*.tar
*.gz
*.7z
*.rar
*.tgz
*.dmg
*.iso
*.cue
*.mdf
*.mds
*.vcd
*.toast
*.img
*.apk
*.msi
*.cab
*.tar.gz
*.tar.xz
*.tar.bz2
*.tar.lzma
*.tar.Z
*.tar.sz
*.lzma
*.ttf
*.otf
*.pak
*.woff
*.woff2
*.eot
*.webp
*.vsix
*.rmeta
*.rlib
*.parquet
*.svg
.egg-info/
.venv/
node_modules/
__pycache__/
.next/
.nuxt/
.cache/
.sass-cache/
.gradle/
.DS_Store/
.ipynb_checkpoints/
.pytest_cache/
.mypy_cache/
.tox/
.git/
.hg/
.svn/
.bzr/
.lock-wscript/
.Python/
.jupyter/
.history/
.yarn/
.yarn-cache/
.eslintcache/
.parcel-cache/
.cache-loader/
.nyc_output/
.node_repl_history/
.pnp.js/
.pnp/
```

## 文件格式

这两个文件使用与 .gitignore 相同的语法。以下是一些示例：

### 基本模式

```properties
# Ignore all files in the `dist` directory
dist/

# Ignore all `.log` files
*.log

# Ignore specific file `config.json`
config.json
```

### 高级模式

只在 app 目录中包含 *.py 文件：

```properties
# ignore everything
*
# do not ignore app
!app/
# do not ignore directories inside app
!app/*/
!app/**/*/
# don't ignore python files
!*.py
```

## 故障排查

ignore 文件的语法完全遵循 .gitignore。如果您遇到问题：

1. 在搜索查询中将 “cursorignore” 替换为 “gitignore”
2. 为类似模式检查 Stack Overflow
3. 使用 git check-ignore -v [file] 测试模式以了解匹配

常见问题：

- 模式相对于 ignore 文件位置进行匹配

- 后来的模式覆盖了以前的模式

- 目录模式需要一个尾随斜杠

- 否定模式（！）必须否定以前的模式