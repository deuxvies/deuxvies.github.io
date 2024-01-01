---
title: "【建站2】在Hugo中发布内容"
description: 
date: 2023-12-13T17:34:26+08:00
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


需要：前面建站1里的git工具、VScode工具，少量markdown语法知识  

# 1.发布纯文字的文章

## 创建新文章

导航到你的 Hugo 根目录，选中博客文件夹右键选中Open git bash here，运行以下代码：

```jsx
hugo new posts/my-first-post.md
```

这将在 content/posts/ 目录下创建一个名为 [my-first-post.md](http://my-first-post.md/) 的 Markdown 文件。

## 编辑文章

使用VSCode打开 content/posts/my-first-post.md 文件，然后编辑内容保存。

Markdown 文件的开头通常包括一些元数据，比如标题、日期、标签等。

**例如：**

```jsx

-- title: "我的第一篇博客"

date: 2023-11-30T09:00:00+00:00

draft: false

tags: ["Hugo", "博客"]

categories: ["技术"]

---

这是我的第一篇博客文章，使用 Hugo 搭建的博客系统。
```
 

## 运行 Hugo 本地服务器进行预览

在git中输入以下代码：

```jsx
hugo server -D
```

然后，打开浏览器，访问 [http://localhost:1313/](http://localhost:1313/)

你应该能够在本地预览你的博客，包括新创建的文章。

如果预览中一切正常，你可以停止 Hugo 服务器，并输入以下代码来生成静态文件：

```jsx
hugo
```

这会在博客的根目录生成一个 public/ 目录，里面包含了你想要呈现的整个博客的静态文件。

你可以将这些文件托管到GitHub（见下篇教程），使其在互联网上可访问。    


# 修改已经发布的 Hugo 文章

## 找到文章 

在 Hugo 项目的 content/posts/ 目录下找到你想修改的文章，以 .md 为扩展名格式。

## 编辑文章内容

使用VScode打开文章，参考[Markdown 官方教程](https://markdown.com.cn/basic-syntax/)，对内容进行修改。

## 添加并提交修改的文件，在git里输入以下代码    

```jsx
git add .
git commit -m "这里随便填，可以注明你的修改记录"
```

然后，再将 public/ 目录的内容部署到你的服务器上。

注意：输入””时要保证是英文输入法状态     


## 运行以下代码，在本地进行预览

```jsx
hugo server -D
```

打开浏览器，访问 [http://localhost:1313/](http://localhost:1313/)

查看你的修改是否生效。在预览中确认无误后，你可以继续下一步部署。

# 3.发布带图文章

如要在 Hugo 中发布有图片的文章，需要使用正确的Markdown语法来插入图片。

## 准备图片

确保你的图片已经放置在博客文件里的 static 文件夹下。
例如，如果你有一张图片 my-image.jpg，可以将其放在 static/images/ 目录下。

## 用 Markdown 插入图片

在文章中，使用以下语法插入图片：

（注：输入下列代码两边要加英文输入法状态下的<>）
imgsrc="/img/hugo version.png"alt="Alt Text"width="50"height="auto"

## 运行 Hugo 本地服务器进行预览

在Git中运行以下命令：

```jsx
hugo server -D
```

打开浏览器，访问 [http://localhost:1313/](http://localhost:1313/)

显示如下：

<img src="/images/1.png" alt="Alt Text" style="width: 50px; height: auto;">

## 调整图片大小

如果需要设置图片的大小，可以修改代码里 width 和 height 的数值。

显示如下：

<img src="/images/1.png" alt="Alt Text" style="width: 600px; height: auto;">

查看你的修改是否生效。在预览中确认无误后，你可以继续下一步部署。