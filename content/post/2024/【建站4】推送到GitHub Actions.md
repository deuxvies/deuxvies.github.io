---
title: "【建站4】推送到GitHub Actions"
date: 2024-01-01T17:34:26+08:00
tags: 
    - 建站记录
categories: 技能
toc: true
hidden: false
comments: true
draft: false
license: false

---

# 基本介绍

GitHub Actions是GitHub提供的一项自动化工作流服务。它允许你在代码仓库中配置和执行自动化任务，例如构建、测试、部署等。

使用 Git 推送到 GitHub 仓库通常需要手动运行 Hugo 构建命令，将生成的静态文件添加到 Git 仓库，并推送到 GitHub，

相比之下，GitHub Actions 提供了自动化的方式来构建和部署 Hugo 网站。在每次推送代码到 GitHub 仓库时，GitHub Actions 可以自动触发构建过程，并将生成的静态文件部署到指定的目标，如 GitHub Pages。


# 主要步骤

<br>

## 创建workflow文件

在 Hugo 项目的根目录下创建一个名为 .github/workflows/main.yml 的文件

打开Git，使用 cd 命令导航到你的 Hugo 项目的根目录。例如：

```jsx
cd path/to/your/hugo/project
```

<br>

替换 path/to/your/hugo/project 为自己的 Hugo 博客文件路径。

使用以下命令创建 .github/workflows 目录：

```jsx
mkdir -p .github/workflows
```

这会创建一个名为 .github/workflows 的目录。-p 选项用于确保如果上级目录不存在也能一并创建。

 
<br>


进入 .github/workflows 目录，用 VSCode创建 main.yml 文件：

<br>

```jsx
code main.yml
```

<br>

打开 main.yml 文件，将 GitHub Actions 的配置内容复制到该文件中：  

```jsx
name: Deploy Hugo

on:

push:

branches:

- main  # 可以根据实际情况修改分支

jobs:

build:

runs-on: ubuntu-latest

steps:

- name: Checkout repository

uses: actions/checkout@v4.1.1

- name: Setup Hugo

uses: peaceiris/actions-hugo@v2

with:

hugo-version: 'latest'

- name: Build

run: hugo --minify

- name: Deploy to GitHub Pages

uses: peaceiris/actions-gh-pages@v3

with:

deploy_key: ${{ secrets.ACTIONS_DEPLOY_KEY }}

publish_dir: ./public
```

<br>

此配置文件的主要作用是：

当代码推送到 main 分支时触发工作流程。

使用 actions/checkout 动作检出仓库。

使用 peaceiris/actions-hugo 动作设置 Hugo 环境并构建网站。

使用 peaceiris/actions-gh-pages 动作将生成的静态文件推送到 GitHub Pages。

<br>

<br>

**注：要更新uses: actions/checkout@ 后面的版本号!!!**

在 GitHub 上 actions/checkout 仓库的 releases 页面查看最新版本，步骤如下：

<br>

打开 actions/checkout 仓库的 releases 页面：

[https://github.com/actions/checkout/releases](https://github.com/actions/checkout/releases)。

在页面上可看到列出的所有发布版本的信息。GitHub Actions 通常会以 v2.x.x 的形式进行版本命名。

最新版本的标签在列表的最上面。

<br>

在 GitHub Actions 工作流程文件中，更新 uses: actions/checkout@v2 部分的版本号为最新版本。例如：

```jsx
name: Checkout repository
uses: actions/checkout@v2.5.1  # 替换为最新版本
```

通过使用最新版本，你可以确保 GitHub Actions 在最新的特性和改进的环境中运行。

<br>

<br>

## 生成 GitHub Personal Access Token（访问令牌）    

为使 GitHub Actions 推送到 GitHub Pages，需要一个具有推送权限的访问令牌，并将其添加到仓库的 Secrets 中。

<br>

**步骤如下：**

1） 生成个人访问令牌     


登录到你的 GitHub 帐户；


在右上角的头像旁边，点击你的头像，然后选择 "Settings"；


在左侧导航栏中，选择 "Developer settings"；


在 "Access tokens" 部分，点击 "Generate token"；


在 "Note" 字段中，输入一个描述性的名称，以便识别这个访问令牌是用于什么目的；


在 "Select scopes" 或 "Select scopes to grant access to your repositories" 部分，选择适当的权限范围。对于部署 Hugo 网站，你可能需要选择 repo 和 workflow；


滚动到页面底部，点击 "Generate token"。


<br>

2）复制生成的个人访问令牌


**重要： 请在生成后立即复制令牌，保存下来，因为它将不再可见，下次忘了得重新生成。**


<br>

3）将令牌添加到仓库的 Secrets 中


转到你的 Hugo 项目的 GitHub 仓库。

在仓库页面的右上角，点击 "Settings"。

在左侧导航栏中，选择 "Secrets and variables"。

点击 "Actions" New repository secret"。

在 "Name" 字段中，输入 ACTIONS_DEPLOY_KEY，这是在 GitHub Actions 配置中引用的 Secret 名称。

在 "Value" 字段中，粘贴刚刚生成的个人访问令牌。

点击 "Add secret"。就可将个人访问令牌添加到仓库的 Secrets 中，在 GitHub Actions 的配置中使用它进行部署。


<br>

<br>

## 将修改的文件添加到 Git

在你的 Hugo 项目路径，使用Git复制以下命令将修改的文件添加到 Git 缓存区：

```jsx
git add .
```

使用以下命令提交修改，其中 "Your commit message" 替换为你的提交信息：

```jsx
git commit -m "Your commit message"
```

将提交的修改推送到 GitHub 仓库：

```jsx
git push origin main
```

<br>

注：

如果默认分支不是 main，请将 main 替换为你的默认分支名称。


确保 main.yml 文件的缩进是正确的 YAML 格式。


确保 Hugo 项目的根目录中有 public 文件夹，并且该文件夹在 .gitignore 文件中没有被忽略。


如果 Hugo 网站使用子模块，确保在 actions/checkout 步骤中包括 submodules: 'recursive' 选项，以确保子模块也被正确检出。


以上步骤适用于 GitHub Actions 的配置，确保仓库的 GitHub Pages 设置是正确的（例如，设置为使用 gh-pages 分支或 docs 文件夹）。部署完成后， 网站应该可以通过 GitHub Pages 访问。


<br>

## 查看 GitHub Actions 运行

访问 GitHub 仓库页面，进入 "Actions" 标签页，能够看到 GitHub Actions 的运行。如果配置正确，工作流程应该会触发并开始运行。


在 GitHub Actions 页面，可查看运行的工作流程的状态、日志和任何可能的错误信息。

一旦工作流程成功运行， 网站应该会被构建并部署到指定的目标（例如 GitHub Pages），可访问网站来确认部署的状态。


<br>
