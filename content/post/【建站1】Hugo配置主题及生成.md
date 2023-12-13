---
title: "【建站1】Hugo配置主题及生成"
description: 此为针对不懂代码的小白的懒人版教程。
date: 2023-12-08T17:34:26+08:00
image: 
hidden: false
comments: true
draft: false
toc: true
tags: 
  - 建站记录

---


hugo和其他各类博客类型了解：
https://cloud.tencent.com/developer/article/1917500
这里我选的是hugo。


# 一.前期准备

1. **安装 Git:**
    访问 [Git 官网](https://git-scm.com/download/win) 下载 Git 的最新版本。
    执行下载的安装程序，并按照提示进行安装。在 "Select Components" 阶段，确保选中 "Git Bash Here" 选项。
1. **安装 Hugo:**
    访问 [Hugo GitHub Releases](https://github.com/gohugoio/hugo/releases) 页面。
    在 Assets 下找到适合 Windows 的 ZIP 文件（通常是 hugo_extended_X.XX.X_windows-64bit.zip）。
    下载 ZIP 文件，并解压到一个你喜欢的目录中（比如 C:\Hugo）。
  
2. **（重要！）添加环境变量:**

    将解压得到的 hugo.exe 文件的路径（比如 C:\Hugo\hugo.exe）添加到系统的 PATH 变量中，以便在任何地方都能够在命令提示符中访问 Hugo。

    在 Windows 上将 Hugo可执行文件的路径添加到系统的 PATH 变量中可以通过以下步骤完成：

    获取 Hugo 可执行文件路径：

      打开 File Explorer（资源管理器），导航到你解压 Hugo ZIP 文件的目录。
      找到 hugo.exe 文件。记住 hugo.exe 的完整路径，
      比如 C:\Hugo\hugo.exe。

    打开系统环境变量设置：

      右键点击计算机（桌面上或开始菜单中），选择 "属性"。
      在左侧面板中，点击 "高级系统设置"。
      在打开的窗口中，点击 "环境变量" 按钮。

    编辑系统 PATH 变量：

      在环境变量窗口中，找到 "系统变量" 部分，找到并选中 "Path" 变量，然后点击 "编辑" 按钮。

    添加 Hugo 可执行文件路径：

      在 "编辑环境变量" 窗口中，点击 "新建" 按钮。
      输入 Hugo 可执行文件的完整路径（例如，C:\Hugo）。
      确认并关闭所有打开的窗口。

    验证是否添加成功：

      打开命令提示符（Command Prompt）

      在Windows 操作系统中，你可以通过以下步骤打开命令提示符：

      在任务栏的搜索框中，键入
      "cmd" 或 "命令提示符"。

      从搜索结果中选择
      "命令提示符" 或 "Command Prompt"。

       运行对话框。

        **或**：按下 Win + R 组合键，打开运行对话框。  

        输入"cmd" 或 "cmd.exe"，然后按 Enter 键。
      无论你使用哪种方法，都会打开一个命令提示符窗口，你可以在其中输入命令。在这个窗口中，你可以执行各种命令和操作系统交互。

    输入 hugo version 并按回车键。
      如果安装成功，你应该能够看到 Hugo 的版本信息，表示安装成功。

  通过这些步骤，你就成功将 Hugo可执行文件的路径添加到系统的 PATH 变量中了。这样，你可以在任何地方使用命令提示符运行Hugo。如果有任何问题，记得检查路径是否正确，确保没有拼写错误。


# 二.创建博客

  1. **打开Git Bash：**

    在你想要创建博客的文件夹中，右键单击并选择 "Git Bash Here"。

  2. **创建 Hugo 站点，输入代码：**
    hugo new site myblog
    这将在当前目录创建一个名为 myblog 的新博客。

  2. **进入博客目录，输入代码：**
    cd myblog

**Tips代码指令解释：**
  
  1.查看当前目录：
    在 Git Bash 终端中，可以输入以下命令来查看当前所在的目录：
    pwd
    这会显示当前工作目录的完整路径。

  2.进入博客目录：
    使用 cd 命令来进入博客目录。假设你的博客目录名为 myblog，你可以执行以下命令：
    cd myblog

    如果博客目录不在当前工作目录，你需要替换成完整路径，例如：
    cd /d/blog/myblog
    这个就是根目录路径↑

  3.验证是否成功进入博客目录：
    输入 pwd 命令确认当前工作目录是否为你的博客目录。
    使用 ls 命令查看博客目录中的文件和子目录：
    ls
    通过这些步骤，你就能够在 Git Bash 中成功进入 Hugo 博客的目录。

  *注：在 Bash 里，

      $： 一般用户的默认提示符。
      #： 超级用户（root）的默认提示符。
      对于默认用户，通常显示 $。
      当你在 Bash 中输入 cd 命令时，你不需要管前面的 $。
      你只需在 cd 后面加上目标目录的路径即可。


# 三.配置Hugo主题模板

1. **选择主题：**
  
    在 Hugo 中，主题通常以 Git 存储库的形式存在。你可以从[Hugo Themes](https://themes.gohugo.io/)网站上选择一个主题。
        
    在该主题的详情页面找到download跳转到 GitHub 界面，点击绿色的按键code便可复制git链接。
        
2. **在博客目录中添加主题作为子模块：**

  
    方法1：直接连接github（坑：有时候因为防火墙问题会配置失败，不推荐！！）

    方法2：SSH密钥法链接（坑： .gitmodules 文件中的行尾符 (line endings) 与你的系统默认设置不一致，可能导致在 Windows 系统上的一些问题，所以也不推荐！！）

    （推荐）方法3：直接下载github仓库zip压缩包到themes文件夹解压（**这个方法最保险**）

      将下载的 ZIP 文件解压缩到你的 Hugo 项目的 themes 文件夹中。

      复制 themes 文件夹里的 exampleSite 中的文件：

      进入主题的文件夹，找到 exampleSite 文件夹。

      选择性复制文件：

      根据你的需要选择性地复制 exampleSite 文件夹中的文件到你的博客根目录。可能包括配置文件（如 config.toml、config.yaml 或 config.json）、内容文件、静态文件等。

      *注意文件路径：确保将文件复制到正确的位置。配置文件通常应该放在博客根目录，而内容文件可能需要根据主题的要求放在特定的文件夹中。

      *保留原有内容：在复制之前，建议备份你当前博客根目录中的重要文件，以免不小心覆盖。你可以将当前博客根目录的文件夹重命名或者备份到其他位置。

3. **编辑主题配置文件：**
    
    打开博客根目录中的 config.toml 文件，这是 Hugo 的配置文件。
    
    在文件中找到或添加一个与主题相关的配置段。你可能需要根据主题的文档查看如何配置。
    
    查找示例配置文件：
    
      在主题目录中，通常会有一个示例配置文件，例如 exampleSite/config.toml 或 exampleSite/config.yaml，具体文件名可能会有所不同。
    
    复制示例配置文件到博客根目录：
    
      使用以下命令将示例配置文件复制到博客根目录。
    
      如果示例配置文件是 config.yaml，则相应地更改文件名。
    
    返回到博客根目录：
    
      使用以下命令返回到博客根目录： 
    
      cd /d/blog/myblog
    
4. **配置其他设置：**
    
    仍然在 config.toml 文件中，你可能需要配置其他与博客相关的设置，如标题、作者、语言等。根据主题文档和你自己的需求进行配置。
    
    *注：编辑config文件时，baseURL应该填什么？
    
      baseURL 是 Hugo 网站的基本 URL 地址，它用于生成网站中的链接。正确配置 baseURL 对于确保生成的网站链接的正确性非常重要。
    
      以下是设置 baseURL 的一些建议：
    
      
      本地开发：
    
      当你在本地开发时，可以将 baseURL 设置为本地服务器的地址，通常是 http://localhost:1313/，这样可确保本地预览。

    
      code baseURL= "[http://localhost:1313/](http://localhost:1313/)"
    
      
      线上发布：
    
      当你准备发布网站时，将 baseURL 设置为你实际的域名或者托管服务的地址。如果你使用自定义域名，确保包括协议（https 或 http）。  
    
      code baseURL= "[https://www.yourdomain.com/](https://www.yourdomain.com/)"
    
      
      子路径或子目录：
    
      如果你计划将网站发布到子路径或子目录下，确保在 baseURL 中包含子路径。
      例如，如果你将网站放在 [https://www.yourdomain.com/blog/](https://www.yourdomain.com/blog/) 下：  
    
      code baseURL= "[https://www.yourdomain.com/blog/](https://www.yourdomain.com/blog/)"
    
      
    总之，根据你的实际情况和计划，选择适当的 baseURL 设置。在网站发布之前，确保在本地测试环境中检查生成的链接是否正确。
    
5. **保存配置文件：**
    
    Ctrl+S保存对 config.toml 文件的修改。
    
# 四.运行 Hugo
    
    在博客根目录运行 Hugo，查看是否成功应用了主题的配置和样式。
    
    hugo server -D

