---
title: "【技巧】Pandoc批量转md的方法"
date: 2024-01-01T17:34:26+08:00
tags: 
    - 建站记录
categories: 技能
toc: true
hidden: false
comments: true
draft: false

---


需要：Git、pandoc

批量管理Markdown文件的笔记软件为Obsidian  

前提：已安装Git软件、word文档格式为.docx而不是.doc（如果是.doc格式要先自行转换为.docx） 、文件命名不含特殊字符     

——————————————————————                    

如果你有大量文档需要搬运到博客，可以尝试.docx格式批量转.md    

**.docx ：** Microsoft Word 文档的文件扩展名 ，以 XML（可扩展标记语言）为基础。这种格式取代了早期的二进制 .doc 格式，提供了更高的兼容性和可扩展性。（所以office软件保存现在保存.docx、.pptx等格式更好哦）。

**.md：** Markdown 文件的文件扩展名，通常包含纯文本，并使用一些特定的语法规则来标记文本的结构和格式，方便转换为有效的HTML。

做法参考这位大佬的教程：
[https://www.cnblogs.com/misaka10212/p/16751506.html](https://www.cnblogs.com/misaka10212/p/16751506.html)

# 安装Pandoc

Pandoc是一个开源的文档转换工具，可以从[官网](https://pandoc.org/)下载并安装。

Windows用户下载 pandoc-3.1.9-windows-x86_64.msi 或 pandoc-3.1.9-windows-x86_64.zip。
如果喜欢使用MSI安装程序（Microsoft Installer），选择 .msi 文件。
如果喜欢使用ZIP文件，选择 .zip 文件。
这两个文件格式都是Windows用户常见的安装文件类型，选一个下就好，下载完成后，按照提示说明进行安装

# 使用Git将文档转换为markdown语法

找到包含你要批量转换的 Word 文档的文件夹，右键打开Open Git bash here。

或者用cd命令在Git里导航到你的文件夹所在路径：    

```jsx
cd /X/XXXX/XXXX/XXXX
```

注：在 Git Bash 中，路径分隔符使用正斜杠 /，而不是反斜杠 \。

转换 Word 文档为 Markdown，输入以下代码： 

```jsx
pandoc your_document.docx -o output_file.md
```

如果遇到问题，请确保 Git Bash 和 Pandoc 都已正确安装，并且 Pandoc 已经被添加到系统的 PATH 中。

```jsx
for file in $(find . -name "*.docx"); do
  pandoc "$file" -o "${file%.docx}.md"
done
```

这个脚本意思是使用 find 命令来查找当前目录及其子目录中的所有 .docx 文件，并通过循环逐个转换它们为 Markdown 文件。

**注：这种方法假设文件名中没有空格或特殊字符。**

如果您的文件名包含空格或特殊字符，可能会影响命令的解释和执行。

常见的特殊字符有：

**空格（Space）：**  常用作参数或文件名之间的分隔符。

**双引号（"）和单引号（'）：**  用于定义字符串。

**反斜杠（\\）：** 用于转义字符。

**通配符（*、?）：** 用于匹配文件名中的字符。

**美元符号（$）：** 在一些上下文中，美元符号有特殊含义，如变量引用。

**反引号（`）：** 在某些上下文中，反引号可能用于命令替换。

**注意在转换前让docx文件名避免包含上述特殊字符。**

Pandoc 找不到文件时会尝试使用默认的输出格式。如果 Pandoc 无法从文件扩展名中推断出格式，将默认为 Markdown 格式。


# 将Markdown文件批量导入Obsidian

将之前转换生成的Markdown文件直接批量复制/移动到 Obsidian 笔记文件夹中，或使用Obsidian的导入功能将文件导入。

Obsidian就会识别Markdown格式，并将文档添加到您的笔记库中。

补充（针对不懂Obsidian者）：

如何 Obsidian 中创建笔记文件夹：

1. 打开 Obsidian 应用。
2. 在左侧文件导航面板中，选择想创建笔记文件夹的位置。
3. 在右键菜单中，选择 "New folder"（新建文件夹）。
4. 输入文件夹的名称并按 Enter 键确认。这样就在选定的位置成功创建了一个新的笔记文件夹。在该文件夹中，你可以创建或存放、修改你的 Markdown 笔记文件，Obsidian 会根据笔记文件的路径和文件名来模拟文件夹结构。

# 其他批量转md文件的方法

方法1：参考→[怎么用calibre将电子书简单粗暴转换为md格式导入obsidian](https://forum-zh.obsidian.md/t/topic/971/3)

方法2：使用notion的导出为markdown功能（前提是文档已存在notion）    

其他方法：[https://publish.obsidian.md/chinesehelp/03+教程/从其他软件导入obsidian（MOC）](https://publish.obsidian.md/chinesehelp/03+%E6%95%99%E7%A8%8B/%E4%BB%8E%E5%85%B6%E4%BB%96%E8%BD%AF%E4%BB%B6%E5%AF%BC%E5%85%A5obsidian%EF%BC%88MOC%EF%BC%89)

# 其他参考

ppt转word（含怎么把大纲不显示文字的PPT转换Word和如何保留原格式将PPT转换成Word）

[http://www.liangshunet.com/ca/201904/765362983.htm](http://www.liangshunet.com/ca/201904/765362983.htm)