---
title: "【建站2】在Hugo中发布内容（含图床使用教程）"
description: 
date: 2020-01-01T17:34:26+08:00
image: 
hidden: false
comments: true
toc: true
tags: 
    - 建站
categories: 建站记录
license: false
Wordcount: false
---


需要：git工具、VScode工具，少量[markdown语法知识](https://markdown.com.cn/basic-syntax/)  




# 发布纯文字的文章

<br>

## 创建新文章

导航到 Hugo 根目录，选中博客文件夹右键选中Open git bash here，运行以下代码：

```jsx
hugo new posts/my-first-post.md
```

这将在 content/posts/ 目录下创建一个名为 [my-first-post.md](http://my-first-post.md/) 的 Markdown 文件。

<br>

## 编辑文章

选中content/posts/my-first-post.md 文件右键使用VSCode打开，然后编辑内容保存。

Markdown 文件的开头通常包括一些元数据，比如标题、日期、标签等。

<br>

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
 

<br>

<br>

## 运行 Hugo 本地服务器进行预览

在git中输入以下代码：

```jsx
hugo server -D
```

然后，打开浏览器，访问 [http://localhost:xxxx/](http://localhost:xxxx/)（根据你自己的运行结果的网址）

能够在本地预览博客，包括新创建的文章。

如果预览一切正常，可以ctrl+c停止 Hugo 服务器，并输入以下代码来生成静态文件：

```jsx
hugo
```

这会在博客的根目录生成一个 public/ 目录，里面包含了整个博客的静态文件。

你可以将这些文件托管到GitHub（见下篇教程），使其在互联网上可访问。    


<br>

# 修改已经发布的 Hugo 文章

<br>

## 找到文章 

在 Hugo 项目的 content/posts/ 目录下找到你想修改的文章，以 .md 为扩展名格式。

<br>

## 编辑文章内容

使用VScode参考[Markdown 官方教程](https://markdown.com.cn/basic-syntax/)对内容进行修改。

<br>

## 添加并提交修改的文件，在git里输入以下代码    

```jsx
git add .
git commit -m "这里随便填，可以注明你的修改记录"
```

然后，再将 public/ 目录的内容部署到你的服务器上。

注意：输入””时要保证是英文输入法状态     


<br>

## 运行以下代码，在本地进行预览

```jsx
hugo server -D
```

打开浏览器，访问 [http://localhost:1313/](http://localhost:1313/)

查看你的修改是否生效。在预览中确认无误后，你可以继续下一步部署。

<br>

<br>

# 发布带图文章

如要在 Hugo 中发布有图片的文章，需要使用正确的Markdown语法来插入图片。

<br>

## 准备图片

确保图片已经放置在博客文件里的 static 文件夹下。
例如，图片 my-image.jpg放在 static/images/ 目录下。

<br>

## 用 Markdown 插入图片

使用以下语法插入图片：

（注：输入下列代码两边要加英文输入法状态下的<>）
imgsrc="/img/hugo version.png"alt="Alt Text"width="50"height="auto"

<br>

## 运行 Hugo 本地服务器进行预览

在Git中运行以下命令：

```jsx
hugo server -D
```

打开浏览器，访问 [http://localhost:xxxx/](http://localhost:xxxx/)

显示如下：

<img src="/images/1.png" alt="Alt Text" style="width: 50px; height: auto;">

<br>

## 调整图片大小

如果需要设置图片的大小，可以修改代码里 width 和 height 的数值。

显示如下：

<img src="/images/1.png" alt="Alt Text" style="width: 600px; height: auto;">

查看修改是否生效。在预览中确认无误后，可继续下一步部署。


<br>


# 使用图床PicGo+GitHub+jsDelivr写带图博客


<br>


在博客嵌入图片有两种形式：

## 本地形式

1. **准备图片文件：** 将图片文件放置在 Hugo 项目的 **`/static`** 文件夹中。
   
2. **编辑内容文件：** 在需要插入图片的内容文件中，你可以使用 Markdown 格式或者 HTML 格式插入图片。
   
    - **Markdown 格式：** 如果使用 Markdown 编写内容，可以使用类似以下格式插入图片：
        
        ```markdown
        
        ![替代文本](/路径/到/图片文件.jpg)
        ![图片描述](/images/example.jpg)
        ```
        
        这里的 **`/路径/到/图片文件.jpg`** 应该是相对于 **`/static`** 文件夹的路径。
        
    - **HTML 格式：** 如果你更喜欢使用 HTML，可以使用 **`<img>`** 标签插入图片：
        
        ```html
        
        <img src="/路径/到/图片文件.jpg" alt="替代文本">
        ```
        
这个方法缺点是图片容易加载缓慢。


## 图床CDN加速形式

### 图床的作用

图床是一种用于存储和管理图片的在线服务，帮助用户将图片从本地上传到云端存储空间，生成图片链接供引用。

这样做的好处是：

1. 可将大量图片存储在云端网盘，节省本地存储空间。
2. 提供稳定可靠的图片访问链接，可以一链接在多个网站、社交媒体或应用程序中分享。
3. 减轻主服务器的压力。
   
### 步骤


1. **上传图片到图床**：首先，你需要将图片上传到图床（例如GitHub等）。图床将为你提供一个图片的 URL。
2. **在 Hugo 内部引用图片**：一旦图片上传到图床，就会生成URL，可在 Hugo 内部的 Markdown 文件或其他内容文件中使用该 URL 来引用图片。例如：
    
    ```markdown
    
    ![图片描述](图片URL)
    ```
    
    其中，**`图片描述`** 是你想要显示的图片的描述文字，**`图片URL`** 是你从图床获得的图片链接
    

这样，当 Hugo 构建网站时，它将会把图片复制到最终生成的网站目录中。

**一言以蔽之，使用图床的正确思路即：**

<img src="/images/jianzhan3.png" >



## 如何配置图床

### Picgo+GitHub参考

[给博客配置图床](https://www.notion.so/2d16223d0c5f43fda0499fc65a88a99c?pvs=21)

[2022【保姆级教程】手把手带你使用PicGo+Github搭建自己的免费图床](https://zhuanlan.zhihu.com/p/553533337)

### jsdelivr加速教程参考

https://zhuanlan.zhihu.com/p/350598351

### 批量压缩图片的工具

[最齐全！26个图片压缩工具推荐，轻松帮网站减重](https://cn.eagle.cool/blog/post/26-best-free-image-optimization-tools-for-image-compression)