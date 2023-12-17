---
title: "【建站2】在Hugo中发布内容"
description: 
date: 2023-12-09T17:34:26+08:00
image: 
hidden: false
comments: true
draft: false
toc: true
categories: 技能
tags: 
  - 建站记录
slug: "【建站2】在Hugo中发布内容"

---

# 1.发布纯文字的文章

### 1.1在命令行中创建新文章

打开终端，导航到你的 Hugo 项目根目录，并运行以下命令： 

hugo new posts/my-first-post.md  

这会在 content/posts/ 目录下创建一个名为 my-first-post.md 的 Markdown 文件。

### 1.2编辑文章内容

使用文本编辑器（比如VSCode）打开 content/posts/my-first-post.md 文件，然后编辑文章内容。

Markdown 文件的开头通常包括一些元数据，比如标题、日期、标签等。

**例如：** 

--- title: "我的第一篇博客"

date: 2023-11-30T09:00:00+00:00

draft: false

tags: ["Hugo", "博客"]

categories: ["技术"]

---

这是我的第一篇博客文章，使用 Hugo 搭建的博客系统。

其中，draft: false 表示这篇文章不是草稿，将被发布。你可以在编辑完文章后保存文件。

### 1.3运行 Hugo 本地服务器进行预览

在终端中运行以下命令：

hugo server -D  

-D 选项用于显示草稿（如果有）。

然后，打开浏览器，访问 [http://localhost:1313/](http://localhost:1313/)

你应该能够在本地预览你的博客，包括新创建的文章。

如果在预览中一切正常，你可以停止 Hugo 服务器，并运行以下命令来生成静态文件： 

hugo  

这会在项目根目录生成一个 public/ 目录，里面包含了你整个博客的静态文件。

你可以将这些文件上传到你的 Web 服务器或者托管服务上，使其在互联网上可访问。 

**# 如果使用 Git，可以添加并提交生成的文件**

git add .

git commit -m "Add my first post"

然后，再将 public/ 目录的内容部署到你的服务器上。

# 2.修改已经发布的 Hugo 文章

你需要编辑该文章的 Markdown 文件，然后重新生成静态文件并部署：

**2.1找到文章：** 

在 Hugo 项目的 content/posts/ 目录下找到你想修改的文章，以 .md 为扩展名。

**2.2编辑文章内容：** 

使用文本编辑器打开文章的 Markdown 文件，对内容进行修改。

你可以更新标题、正文、标签、日期等信息。保存文件。

**2.3运行 Hugo 本地服务器进行预览：** 

在终端中运行以下命令：

hugo server -D

打开浏览器，访问 [http://localhost:1313/](http://localhost:1313/)

查看你的修改是否生效。在预览中确认无误后，你可以继续下一步部署。 

# 3.发布带图文章

在 Hugo 中发布带有图片的文章需要你在 Markdown 文件中使用正确的语法来插入图片。

**3.1准备图片：** 

确保你的图片已经放置在 Hugo 项目中的 static 目录下，或者在 Markdown 文件所在的目录中。
例如，如果你有一张图片 my-image.jpg，可以将其放在 static/images/ 目录下。

**3.2使用 Markdown 插入图片：**

 在文章的 Markdown 文件中，使用以下语法插入图片：
 
 （注：输入下列代码两边要加英文输入法状态下的<>）
imgsrc="/img/hugo version.png"alt="Alt Text"width="50"height="auto"


**运行 Hugo 本地服务器进行预览：**

在终端中运行以下命令：
hugo server -D
打开浏览器，访问 [http://localhost:1313/](http://localhost:1313/)


显示如下：

<img src="/images/1.png" alt="Alt Text" style="width: 50px; height: auto;">


**3.3调整图片大小：** 

如果需要设置图片的大小，可以修改代码里 width 和 height 的数值。

显示如下：

<img src="/images/1.png" alt="Alt Text" style="width: 600px; height: auto;">

查看你的修改是否生效。在预览中确认无误后，你可以继续下一步部署。