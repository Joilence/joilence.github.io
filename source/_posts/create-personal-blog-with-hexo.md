---
title: 搭建个人博客：Hexo & GitHub Pages
date: 2016-07-11 02:51:22
tags:
---
【在 OS X 上操作，部分适用于 Linux】

# 相关

- Hexo

  Hexo 是一个静态博客框架。你只需要在本地使用 Hexo 生成静态页面，并部署到代码托管平台，即可通过网站访问博客页面。

- GitHub Pages

  GitHub 的免费静态页面托管服务，可以使用 username.github.io 或者自定义域名来访问站点。

# 准备

## GitHub 账户

[注册 GitHub 账户](https://github.com/join)

## 安装 Git，Node.js

建议先安装 Homebrew，一个包管理器 (Package Manager)。

``` bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

之后可以通过 Homebrew 来安装 Git，Node.js。

``` bash
$ brew install git node.js
```

## 安装 Hexo

安装 Node.js 的过程中也会自动安装 npm，另一个包管理器。在 Terminal 使用 npm 安装 Hexo。同时因为我们希望用 GitHub Pages 来托管静态网页，所以需要安装 hero-generator-git。

``` bash
$ npm install hexo hexo-generator-git
```

# 配置 Hexo

选择一个目录创建一个新的文件夹，通过 Terminal 使用 cd 命令访问这个文件夹，在该文件夹完成 Hexo 的初始化配置。

``` bash
$ hexo init
```

此时运行以下指令进行测试。

``` bash
$ hexo server
```

此时 Terminal 中会显示访问页面的方式，通常是 `localhost:4000`，访问即可看见 Hexo 初始的页面。

# [配置 GitHub Pages](https://pages.github.com)

# 部署 Hexo 静态页面

进入你的博客文件夹，使用文本编辑器打开 _config.yml 文件，编辑最下面的 deploy 部分。

如果配置 GitHub Pages 中你选择使用 User site，修改为以下样式。

``` yaml
deploy:
  type: git
  repository: https://github.com/[username]/[username].github.io.git
  branch: master
```

如果配置 GitHub Pages 中你选择使用 Project Site，则修改为以下样式。

``` yaml
deploy:
  type: git
  repository: https://github.com/[username]/[repository name].git
  branch: gh-pages
```

通过 Terminal 进入你的博客文件夹，先生成静态页面，再部署到 GitHub Pages。

``` bash
$ hexo generate
$ hexo deploy
```

某些情况下，当你遇到`Fatal`,`Error` 等字眼时，可以重新使用 `sudo` 运行以上指令。

``` bash
$ sudo hexo generate
$ sudo hexo deploy
```

# 更多

发布博文，以及 Hexo 的详细配置，推荐 [Hexo 官方文档](https://hexo.io/zh-cn/docs/)

推荐 Hexo 博客主题 [NexT](http://theme-next.iissnan.com/getting-started.html)，同样有详细说明。

