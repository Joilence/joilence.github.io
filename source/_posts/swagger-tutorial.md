---
title: 编写 API 设计文档：Swagger、OpenAPI
date: 2018-07-07 15:22:04
tags:
- api
---

> 因为团队协作需要，接触到了 Swagger 用以进行 API 设计说明并生成页面。Swagger 的用处并不仅限于此，不过本文仅仅进行对于「API 设计文档」这一主题的总结。

## OpenAPI Specification

[OpenAPI Specification](https://github.com/OAI/OpenAPI-Specification) 是 Linux 基金会的一个项目，试图用一套标准规范的语言描述 RESTful API，提升工程师协作效率，同时使得计算机也能快速理解（解析）。Swagger 使用的就是 OpenAPI 规范。

## 遵循 OAS 编写 Swagger YAML 文件

格式规范不再复制粘贴了，可参考 [Swagger Live Editor](https://editor.swagger.io/) 中默认显示的 PetStore 样例，以及 [Swagger 官方文档](https://swagger.io/docs/specification/about/) 

可以使用 [Swagger Live Editor](https://editor.swagger.io/) 或者 VS Code 的 Swagger Previewer 插件进行实时编辑和预览。

## 生成一个可访问的静态页面

通常一个项目会有一个 Dashboard 之类的主页对项目进行一系列说明，包括 API 设计说明，这时就可以把 Swagger 的 yaml 文件生成一个静态页面。找了好几个生成工具如 `swagger-to-html` 效果都不如人意，十分简陋，都不如 Swagger Editor 的 Preview 好看；但 Swagger 官方却又没提供一个简单的工具。

于是我采用了一个比较简陋的办法，将 Swagger 官方的样例网站 [Swagger PetStore](https://petstore.swagger.io/) 的静态资源下载下来，放入到 Github Pages 的静态目录里去，把默认加载的 yaml 文件 URL 改成自己需要的，即可生成一个效果与 Swagger Editor Preview 相同的静态页面。

注：之后又找到一个工具叫做 [Spectacle](https://github.com/sourcey/spectacle) 似乎效果也不错，可以一试。