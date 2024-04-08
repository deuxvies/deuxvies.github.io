---
title: "【建站3】使用SSH密钥法将Hugo上传至Github"
date: 2020-01-01T17:34:26+08:00
tags: 
    - 建站
categories: 建站记录
toc: true
hidden: false
comments: true
license: false

---

<br>

需要：能访问GitHub的条件


<br>

# 前期准备

<br>

## 注册github账号

GitHub是一个基于Git版本控制系统的代码托管平台。

注册步骤（要魔法工具，有github账号的可跳过）：    

1）访问[GitHub官网](https://github.com/)。  

2）在GitHub首页点击"Sign up"按钮。

3）填写注册信息，包括用户名、电子邮件地址（尽量用外国邮箱，推荐[proton mail](https://proton.me/mail)、[tutanota mail](https://tuta.com/zh_hans/)或gmail）和密码。用户名要好好取，因为它会用作你在GitHub上的标识。

4）选择免费计划然后点击"Continue"。

5）设置头像、添加个人简介等信息。完成设置后，点击"Submit"。

6）验证邮箱：按照指示操作就行了。


注册好GitHub账户后就可以使用你的用户名和密码登录GitHub。


<br>

# 将Hugo部署到GitHub前期准备

*注：在生成静态页面之前要把config.toml文件里的baseURL修改为自己博客的网址，譬如：

```jsx
baseURL = "[https://xxxxx.github.io/](https://xxxxx.github.io/)"
```

```jsx
hugo    ##生成静态页面文件
```

<br>

<br>

## 在 GitHub 上创建新仓库

登录到 GitHub

在右上角的头像旁边，点击加号（+），然后选择 "New repository"。

命名你的仓库，**注意：**仓库名要以 [你的github用户名.github.io](http://xn--github-on9im33ani7aou3bged.github.io/) 这种格式

例如，你的github用户名是abcd，仓库名就是：[abcd.github.io](http://xxxxx.github.io/)，确保github用户名和你的本地文件config.toml里的baseURL博客网址一致，

不要勾选 "Initialize this repository with a README" 选项（因为 Hugo 网站已经有了自己的 README）。

点击 "Create repository"。


<br>

接下来将本地 Hugo 仓库关联到 GitHub 仓库，有两种方法。

方法1：https法推送到github pages，适合没有墙的环境，pass

方法2：SSH密钥法连接，比较安全，减少了每次推送、拉取或克隆仓库时的繁琐过程，推荐


<br>

<br>

## 注：确认Github仓库的默认分支

GitHub 近期已经在新仓库中将默认分支的名称从 master 更改为 main，如果你的github默认分支是 master，请将master替换为 main。

<br>

替换步骤：

打开你的 GitHub 仓库。

点击右上角的 "Settings"（设置）。

进入新的界面后直接在Repository name下找到 "Default branch"（默认分支）

下拉菜单中选择你想要设置为默认的分支，例如 main

点击 "Update"（更新）按钮保存更改。


<br>

设置 GitHub Pages：

• 在 GitHub 仓库页面的顶部，点击 "Settings"。

• 在左侧导航栏中选择 "Pages"。

• 在 "Source" 下拉菜单中选择 main 分支（或者是你的默认分支）。

• 点击 "Save"。


<br>

<br>


# 使用SSH密钥与GitHub建立连接

<br>

## 生成 SSH 密钥

打开Git。
运行以下命令生成 SSH 密钥。如果已有一个 SSH 密钥可跳过此步骤。

```jsx
ssh-keygen -t rsa -b 4096 -C "[your_email@example.com](mailto:your_email@example.com)"
```

替换 "[your_email@example.com](mailto:your_email@example.com)" 为你在 GitHub 注册时使用的电子邮件地址。

按照提示，选择默认的文件路径和设置密码（可选）。

<br>

## 添加 SSH 密钥到 SSH 代理

运行以下命令启动 SSH 代理：

```jsx
eval "$(ssh-agent -s)"
```

将 SSH 私钥添加到 SSH 代理：

```jsx
ssh-add ~/.ssh/id_rsa
```

如果使用了不同的密钥文件名，替换 id_rsa 为实际的私钥文件名。

<br>

## 添加 SSH 公钥到 GitHub

使用以下命令查看并复制 SSH 公钥：

```jsx
cat ~/.ssh/id_rsa.pub
```

该命令将在终端中显示 SSH 公钥内容。

<br>

## 登录到 GitHub

点击右上角的头像，选择 "Settings"。

在左侧导航栏中，选择 "SSH and GPG keys"。

点击 "New SSH key"。

在 "Title" 字段中，为 SSH 密钥提供一个描述性的名称。

在 "Key" 字段中，粘贴复制的 SSH 公钥。

点击 "Add SSH key"。


<br>

## 测试 SSH 连接
运行以下命令测试 SSH 连接：

```jsx
ssh -T [git@github.com](mailto:git@github.com)
```

如果设置正确，会看到一条消息显示已成功地进行了身份验证。

如果出现警告或错误，请检查你的设置。

一旦成功设置了 SSH 密钥，就可以用它与 GitHub 进行安全的连接。


<br>

## 将仓库 URL 切换为 SSH

在你的 Hugo 项目目录中，使用以下命令将仓库的 URL 从 HTTPS 切换到 SSH。


## 找到仓库的 SSH 地址

进入你的 GitHub 仓库页面

点击 "Code" 按钮，然后选择 "SSH" 选项，会显示仓库的 SSH 地址，类似于 [git@github.com](mailto:git@github.com):your_username/your_repository.git

复制到git面板，把下列代码后半段的ssh地址替换成你的↓

```jsx
git remote set-url origin [git@github.com](mailto:git@github.com):xxxxxx/xxx.git
```

<br>

## 推送到 GitHub 仓库

在git里使用以下代码将本地分支推送到 GitHub 仓库：

```jsx
git push origin main
```

该命令会将本地的 main 分支的提交推送到 GitHub 上的 origin/main 分支。

<br>

## 验证推送
在推送后，可以在 GitHub 仓库页面上查看是否有新的提交。若一切正常，提交应该已经被推送到 GitHub 仓库。


<br>

<br>

<br>


# **注：可能遇到的问题**

<br>

**q1：**
Enter file in which to save the key
(/c/Users/xxxx/.ssh/id_rsa): /c/Users/.ssh/id_rsa already exists. Overwrite
(y/n)? y Enter passphrase (empty for no passphrase): 这一步该怎么办？

<br>

答：这个步骤是在生成 SSH 密钥时的一些设置选项，如  

<br>

***"Enter file in which to save the key"：***

这个意思是系统正在询问你要保存 SSH 密钥的文件路径和名称。默认情况下，它会提供一个默认的路径，例如 /c/Users/xxxx/.ssh/id_rsa。这是 SSH 密钥的默认路径和名称。

如果想将密钥保存在默认位置并使用默认名称，只需按 Enter 键。否则，你可以输入一个新的文件路径和名称，例如 /c/Users/xxxx/.ssh/custom_key。

<br>

***"already exists. Overwrite (y/n)?"：***

如果你选择的文件路径和名称已经存在一个文件，系统会询问你是否要覆盖现有文件。在你的情况下，系统发现 /c/Users/xxxx/.ssh/id_rsa 已经存在。

如果想覆盖现有文件并使用相同的路径和名称，你可以输入 y 并按 Enter 键。否则，输入 n 并按 Enter 键，然后选择另一个路径和名称。

<br>

***"Enter passphrase (empty for no passphrase)"：***

在这一步，系统询问你是否要为 SSH 密钥设置密码（也称为“passphrase”）。密码对于提高安全性很有用，但是你可以选择留空，按 Enter 键，以创建没有密码的密钥。

如果你选择设置密码，确保记住密码，因为在将来你使用密钥时需要输入密码。


<br>

***总结：***

如果希望使用默认设置，只需按 Enter 键即可。

如果希望更改保存密钥的路径和名称，输入新的路径和名称。

如果密钥文件已经存在，自己决定是否要覆盖。

选择是否设置密码，如不想设置密码，直接按 Enter 键。


<br>


**Q2：**
输入仓库的SSH地址时，显示：

The authenticity of host 'github.com (XX.XXX.XXX.XXX)' can't be established.
XXXXXX key fingerprint is XXXXXXXXXXXXXXXXXXXXXXXX
This key is not known by any other names. Are you sure you want to continue
connecting (yes/no/[fingerprint])? 该怎么办？

<br>

答：这是 SSH 连接的一部分，系统会询问你是否信任 GitHub 的主机密钥。通常只会发生一次，当你第一次连接 GitHub 时，GitHub 提供了一个密钥用于安全连接，在提示中会有一行显示 GitHub 的公钥指纹，需要确保指纹与 GitHub 上提供的一致。

如果指纹是正确的，输入 yes 表示你确认连接。

如果你有疑虑或担心，可以输入 no 中止连接。

如果输入 yes，计算机将记住 GitHub 的主机密钥，以后连接时不再提示。

<br>

**Q3：**

显示Cloning into 'D:/blog/myblog/themes/XXXXX'... Enter passphrase for key '/c/Users/XXXX/.ssh/id_rsa': remote: Enumerating objects: 2393, done. remote: Counting objects: 100% (98/98), done. remote: Compressing objects: 100% (65/65), done. remote: Total 2393 (delta 42), reused 73 (delta 29), pack-reused 2295 Receiving objects: 100% (2393/2393), 1.56 MiB | 1.08 MiB/s, done. Resolving deltas: 100% (1400/1400), done. warning: in the working copy of '.gitmodules', LF will be replaced by CRLF the next time Git touches it 该怎么办？

<br>

答：这个警告是由于 Git 发现 .gitmodules 文件中的行尾符 (line endings) 与你的电脑系统默认设置不一致，可能导致在 Windows 系统上的一些问题。

可按照以下步骤操作：
在 Git Bash 中运行以下命令，将 .gitmodules 文件的行尾符修改为 LF（换行符）：

```jsx
git config --global core.autocrlf input
```

接下来，重新拉取子模块：

```jsx
git submodule update --init --recursive 
```

这样，Git 将使用 LF 行尾符处理 .gitmodules 文件，与 GitHub 上的默认设置一致。

可通过运行以下命令检查设置是否正确：
```jsx
git config --global core.autocrlf 
```
如果设置正确，命令的输出应该是 input。如果输出是 true 或 false，则表示设置不正确，需要重新运行 git config 命令。


<br>

<br>

**其他参考：**

[塔塔的博客的Q&A](https://mantyke.icu/posts/2021/hugo-build-blog/)：这个是vercel+github托管，用GitHub Desktop推送，实在搞不懂上述教程的可以试试这个方法。

hugo+github+vercel部署流程如下：

<img src="/images/jianzhan2.png" >


[Hugo 的使用&配置中有那些技巧与坑？](https://blog.csdn.net/ccviolett/article/details/124815319)

[记录下使用hexo搭建博客踩过的坑](https://juejin.cn/post/7127828118143762469)


<br>

