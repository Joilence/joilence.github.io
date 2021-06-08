---
title: Hexo 博客进阶配置与常见问题
date: 2016-07-14 21:26:45
tags:
---
【在 OS X 上操作，部分适用于 Linux】
# 2016.7.26
## 使 Hexo 支持脚注（Footnote）以及 Emoji

更换 Markdown 渲染插件。

`cd` 进入 Hexo Blog 主目录，移除 Hexo 默认的 `hexo-renderer-marked`，安装 `hexo-renderer-markdown-it`。

``` shell
$ npm un hexo-renderer-marked --save
$ npm i hexo-renderer-markdown-it --save
```

为了使 Hexo 支持 Emoji，还需要进入 `hexo-renderer-markdown-it` 目录里，安装支持 Emoji 的插件。

``` shell
$ cd node_modules/hexo-renderer-markdown-it/
$ npm i markdown-it-emoji --save
```

在博客根目录下的 `_config.yml` 中，添加以下字段（以下是我的配置）：

``` yaml
markdown:
  render:
    html: true
    xhtmlOut: false
    breaks: false
    linkify: true
    typographer: true
    quotes: '“”‘’'
  plugins:
    - markdown-it-footnote
    - markdown-it-sup
    - markdown-it-sub
    - markdown-it-abbr
    - markdown-it-emoji
  anchors:
    level: 1
    collisionSuffix: 'v'
    permalink: true
    permalinkClass: header-anchor
    permalinkSymbol: ' '
```

参考文献：
1. [让Hexo支持emoji表情](https://ppxu.me/2015/12/24/enable-emoji-in-hexo/)
2. [Github: hexo-renderer-markdown-it](https://github.com/celsomiranda/hexo-renderer-markdown-it)

## 删除文章

在使用 `hexo new` 生成新文章之后，想要删除，如果只是直接在 `/source/_post` 中将相关 md 文件删除，可能在生成网页后还会重现。删除文章比较完备的步骤如下：

1. 在 `/source/_post` 中删除相关 md 文件
2. 在博客根目录下使用 `sudo hexo clean`
3. 删除博客根目录下的 `db.json` 文件

再重新生成网页就可以了。

# 2016.7.23

## 去除 NexT-Mist 主题的图片边框

编辑 `Blog/themes/next/source/css/_common/components/post/post-expand.styl`，将 Line 52 处 border 后的像素数改为 0px。

# 2016.7.14

## 添加新文章后自动用文本编辑器打开

在 Blog 目录下创建 `scripts` 目录（如果没有的话），在该目录下创建一个 JavaScript 脚本监听 `hexo new` 命令即可，脚本文件名任意。

``` js
var exec = require('child_process').exec;

// Hexo 2.x
hexo.on('new', function(path){
    exec('open -a "Application/YourEditor.app" ' + path);
});
// Hexo 3
hexo.on('new', function(data){
    exec('open -a "Application/YourEditor.app" ' + data.path);
});
```
Github Hexo 相关 Issue：
[Open markdown file after running hexo new?](https://github.com/hexojs/hexo/issues/1007)

## 使用 MWeb 配合 Hexo 写博客
打开 MWeb，按下 `Cmd + E` 进入外部模式，将 Blog 目录下的 source 文件夹加入到 External Source 列表中。

![MWeb-external-table](/images/MWeb-external-table.png)

则右部列表如上图可见。双击 source 文件夹名，可进入编辑界面。

![MWeb-external-source-edit](/images/MWeb-external-source-edit.png)

修改 `Display Name` 可以修改 Library 展示的名称，但不会更改原目录的名称。
修改 `Media Folder Name` 以及 `Media Save Path` 可以修改博客图片存储的目录名及其路径。


