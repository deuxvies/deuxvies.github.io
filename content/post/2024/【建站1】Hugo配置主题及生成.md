---
title: "【建站1】Hugo配置主题及生成"
date: 2024-01-01T17:34:26+08:00
tags: 
    - 建站记录
categories: 技能
toc: true
hidden: false
comments: true
draft: false

---

hugo和其他各类博客类型了解：
[https://cloud.tencent.com/developer/article/1917500](https://cloud.tencent.com/developer/article/1917500)
<p>这里我选的是用Hugo搭建，比较简洁，wordpress对我来说太臃肿了访问也慢。Hugo内容可以在本地，备份比较方便和稳定。<p>

**注：**

博主非计算机专业，对代码一窍不通；

此搭建记录使用的电脑系统为windows，不适用Linux、mac人群；

建博用的工具为Git、Hugo、VScode（写代码工具）；部署用的是GitHub   

搭建过程需要：稳定的魔法工具、能访问Github、少量英语阅读能力以及基础的信息检索能力、电脑操作能力、足够的本地磁盘容量。    

---

# 前期准备

## 安装 Git

**何为git？**

Git就是一个搭建博客时用来推送源代码、跟踪文件的变化、记录每次修改、保存历史版本的工具。你后期更新博客的样式、文章等等都是修改后通过Git来推送。

**Git安装步骤：**

1）去 [Git 官网](https://git-scm.com/download/win) 下载 Git 的最新版本，根据你的电脑系统类型选择版本。

2）下载完后在本地右键安装程序，按照默认的设置一路安装就好，注意在 "Select Components" 阶段，确保要选中 "Git Bash Here" 选项。

## 安装VScode  

**何为VScode？**

Visual Studio Code（VSCode）为Microsoft开发的免费、开源的源代码编辑器。就是用来帮你修改hugo的主题文件代码的一个编辑工具，比如你文本一般是用word编辑，代码就是用VScode来编辑。

**VScode安装步骤：**

1）访问[Visual Studio Code官网](https://code.visualstudio.com/)
<p>2）选择适用于你的电脑系统的版本下载。<p>
<p>3）运行安装程序：按照提示进行安装。在Windows上，点击“Next”点到底，接受许可协议，并选择安装位置（可以自定义安装在哪个盘，避免让c盘负担过重）。<p>

4）启动VSCode： 安装完成后，你可以在开始菜单（Windows）中找到Visual Studio Code。双击启动它，就会看到一个编辑器界面。之后修改博客的代码文件时，只要右键选择“打开方式”-选择vscode即可。

## 安装 Hugo

**何为Hugo？**

Hugo就是我们用来生成静态博客网页的网站生成器，我们可以用前面安装的Git通过代码的配合，将想要呈现的内容转换为HTML网页。

**Hugo安装步骤：**

1）访问 [Hugo GitHub Releases](https://github.com/gohugoio/hugo/releases) 页面。

2）在 Assets 下找到适合 Windows 的 ZIP 文件（通常是 hugo_extended_X.XX.X_windows-64bit.zip）。

3）下载 ZIP 文件，并解压到一个你喜欢的磁盘里。

### （重要！）添加环境变量

解压得到的 hugo.exe 文件的路径一定要添加到系统的 PATH 变量中，否则有时写代码时会出现访问不了 Hugo的情况。

添加环境变量步骤：

1）获取 Hugo 的执行文件路径：  

用wins+E快捷键打开 File Explorer（文件资源管理器），找到你解压 Hugo ZIP 文件的地方，找到 hugo.exe 文件；

鼠标点击上方的栏目，变成光标即可看到你的 hugo.exe 的完整路径，比如 D:\Downloads\Hugo。

<img src="/images/Untitled.png" alt="Alt Text" style="width: 600px; height: auto;">
<img src="/images/Untitled 1.png" alt="Alt Text" style="width: 600px; height: auto;">


2）打开系统环境变量设置：  

右键点击计算机图标，选择 "属性"。

<img src="/images/Untitled 2.png" alt="Alt Text" style="width: 600px; height: auto;">

在面板中找到 "高级系统设置"。

<img src="/images/Untitled 3.png" alt="Alt Text" style="width: 600px; height: auto;">

在打开的窗口中，点击 "环境变量" 按钮。

<img src="/images/Untitled 4.png" alt="Alt Text" style="width: 600px; height: auto;">

3）编辑系统 PATH 变量：  

在环境变量的面板中，找到下方的 "系统变量" 部分，选中 "Path" 变量点击 "编辑" 按钮。

<img src="/images/Untitled 5.png" alt="Alt Text" style="width: 600px; height: auto;">

3）添加 Hugo 可执行文件路径：  

在 "编辑环境变量" 窗口中，点击右上方第一个 "新建" 按钮。
输入 前面你复制的Hugo 执行文件的路径（例如，D:\Downloads\Hugo）。
确认并关闭所有打开的窗口。

4）验证是否添加成功：  

在Windows 操作系统中，在任务栏的搜索框中，键入
"cmd" 或 "命令提示符"。
<img src="/images/Untitled 6.png" alt="Alt Text" style="width: 600px; height: auto;">
或者是按下快捷键 Win + R ，打开运行面板，在里面输入cmd就可以弹出命令提示符的面板
<img src="/images/Untitled 7.png" alt="Alt Text" style="width: 600px; height: auto;">

在命令提示符的面板输入 hugo version ，然后按回车。
如果安装成功，你应该能够看到 Hugo 的版本信息，表示安装成功。

通过以上步骤，你就成功将 Hugo可执行文件的路径添加到系统的 PATH 变量中。这样，你可以在任何地方使用命令提示符运行Hugo。如果出现问题，记得检查你的路径是否正确。

## 安装go语言

Hugo 是使用 Go 语言开发的静态网站生成器，因此在运行 Hugo 之前，确保 Go 语言环境已经安装。

**安装步骤：**

1）打开 [Go 的官网](https://www.notion.so/by-mealin564-7e0ddfb6240347328003ea868799da39?pvs=21)[。](https://golang.org/dl/%E3%80%82)

2）选择适合你电脑的 Windows 最新版本，然后选择带有 **.msi 后缀**的安装程序下载

3） 双击下载的安装程序（.msi 文件），然后按提示操作。你可以接受默认设置，也可以根据需要进行自定义配置。

4）检查安装： 安装完成后，打开命令提示符或 PowerShell 窗口，并运行以下命令来验证 Go 是否正确安装：


```jsx
go version
```

如果一切正常，你应该看到 Go 的版本信息。

注：

在安装 Go 语言时，确保将 Go 的 bin 目录添加到系统的 PATH 环境变量中，以便在命令行中直接运行 go 命令。

若没有添加，你需要手动将 C:\Go\bin（或你选择安装的路径）添加到 PATH 中（步骤和上述操作相似）。
安装完成后，你就可以在 Windows 上使用 Go 语言了


# 2.创建博客

## 打开Git Bash

新建一个你想要放博客内容和修改样式的文件，右键单击并选择 "Git Bash Here"。  
<img src="/images/Untitled 8.png" alt="Alt Text" style="width: 600px; height: auto;">

1. **创建 Hugo 站点，输入代码：**
    
    ```jsx
    hugo new site myblog
    ```
    
    这将在这个路径创建一个新博客。
    
2. **进入博客目录，输入代码：**
    
    ```jsx
    cd myblog
    ```
    

- **Tips代码指令解释**
    
    1.查看当前目录：
    在 Git Bash 终端中，可以输入以下命令来查看当前所在的目录：
    
    ```jsx
    pwd
    ```
    
    这会显示当前文件夹的完整路径。
    
    2.进入博客目录（就是找到你新建的那个要放博客内容的那个文件）， 假设你的博客文件夹名为 myblog，你可以执行以下命令：
    
    ```jsx
    cd myblog
    ```
    
    如果博客文件夹不在当前工作目录，你需要替换成完整路径，例如：
    
    ```jsx
    cd /d/blog/myblog
    ```
    
    例如，这个就是我的博客文件的“根目录路径”↑
    
    3.验证是否成功进入博客目录：
    输入 pwd 命令确认当前工作目录是否为你的博客目录。
    使用 ls 命令查看博客目录中的文件和子目录：
    
    ```jsx
    ls
    ```
    
    通过这些步骤，你就能够在 Git Bash 中成功进入 Hugo 博客的目录。
    
    注（基础操作知识）：在Git Bash界面里输代码时，    
    
      $： 一般用户的默认提示符。
      #： 超级用户（root）的默认提示符。
      对于默认用户，通常显示 $。
      在 Bash 中输入 cd 命令时，不用管前面的 $，只要复制上述的代码输入就行！
     
    

# 3.配置Hugo主题模板

## 选择主题

在[Hugo Themes](https://themes.gohugo.io/)网站上选择一个喜欢的主题。

在该主题的详情页面找到download，跳转到 GitHub 界面，点击绿色的按键code。

方法1：直接连接github（坑：有时会因防火墙问题配置失败，不推荐！！）

方法2：SSH密钥法链接（坑： .gitmodules 文件中的行尾符 (line endings) 与系统默认设置不一致，可能导致在 Windows 系统上的一些问题，所以也不推荐！！）

**（所以推荐）方法3：直接点击绿色code按键下方的Download Zip，下载github仓库zip压缩包到你的博客文件夹的themes文件夹里。**

<img src="/images/Untitled 9.png" alt="Alt Text" style="width: 600px; height: auto;">

<img src="/images/Untitled 10.png" alt="Alt Text" style="width: 600px; height: auto;">


## 在博客目录中添加主题

将下载的 ZIP 文件在博客文件夹的themes 文件夹中右键解压

**编辑主题配置文件：**

打开博客根目录（即你的博客文件夹）中的 config.toml 或者config.yaml文件，这是 Hugo 的配置文件。 

在文件中添加或修改与主题相关的配置段，需要根据主题的文档查看如何配置。

config文件主要改动的是你想要的博客模板，比如你的主页标题、导航栏文字、链接地址、语言、版权信息、url等等。

可以参考主题文件里的示例配置文件，例如 exampleSite文件夹里的config.toml 或 config.yaml，也可以自己google搜索“你的hugo主题名+装修”，看看其他博主的博客装修步骤记录和教程。

- **注：编辑config文件时，baseURL应该填什么？**

baseURL 是 Hugo 博客网站的基本网址链接，帮你生成网站。

当你还没购买域名，在本地修改博客测试时，可以将 baseURL 设置为本地服务器的地址，通常是 [http://localhost:1313/](http://localhost:1313/%EF%BC%8C%E8%BF%99%E6%A0%B7%E5%8F%AF%E7%A1%AE%E4%BF%9D%E6%9C%AC%E5%9C%B0%E9%A2%84%E8%A7%88%E3%80%82)
这样可确保本地同步预览。将代码换成以下↓

```jsx
code baseURL= "[http://localhost:1313/](http://localhost:1313/)"
```

当你有购买的域名和托管的网址时，可将 baseURL 设置为相应的域名。如果你使用自定义域名，确保包括协议（https 或 http）。

```jsx
code baseURL= "[https://www.这里填入你的域名.com/](https://www.yourdomain.com/)"
```

总之，根据你的实际情况和计划，选择适当的 baseURL 设置。在网站发布之前，确保在本地测试环境中检查生成的链接是否正确。

## 保存配置文件

修改好文件后，Ctrl+S 保存对 config.toml 文件的修改。

# 四.运行 Hugo

在博客根目录运行 Hugo，右键点击你的博客根目录（博客文件），选择git bash here，在git里输入以下代码：

```
hugo server -D
```

如果成功会显示如下：  
<img src="/images/Untitled 11.png" alt="Alt Text" style="width: 600px; height: auto;">

比如，如上图所示，你可以在 [http://localhost:5090/](http://localhost:5090/%EF%BC%8C%E8%BF%99%E6%A0%B7%E5%8F%AF%E7%A1%AE%E4%BF%9D%E6%9C%AC%E5%9C%B0%E9%A2%84%E8%A7%88%E3%80%82)中预览网站，查看是否成功应用了主题的配置和样式。（*http://localhost:后面的数字根据你自己运行的结果而改变）