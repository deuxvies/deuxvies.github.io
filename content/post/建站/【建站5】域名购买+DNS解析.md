---
title: "【建站5】域名购买+DNS解析"
date: 2020-01-01T17:34:26+08:00
tags: 
    - 建站
categories: 建站记录
toc: true
hidden: false
comments: true
license: false
slug: hugo5

---

# 域名购买与配置

<br>

**域名对比，我选的是namesilo：**

[https://shannote.com/archives/buy-foreign-domains.html](https://shannote.com/archives/buy-foreign-domains.html)

<br>

**namesilo购买教程：**

[https://shannote.com/archives/how-to-register-namesilo-domain.html](https://shannote.com/archives/how-to-register-namesilo-domain.html)

<br>

**Namesilo配置教程：**

[https://blog.mailjob.net/posts/4108183257.html](https://blog.mailjob.net/posts/4108183257.html)

[https://shannote.com/archives/how-to-register-namesilo-domain.html](https://shannote.com/archives/how-to-register-namesilo-domain.html)

<br>

**所有的操作是跟着这个教程走的:**

[https://www.zhudc.com/website/2413](https://www.zhudc.com/website/2413)


<br>

# 填写注意

## A 记录（IPv4 地址）

主机名（Host）： 通常是 @
 或者你的域名（比如 example.com）。

IP 地址： 这是你的服务器的公共 IPv4地址。


<br>

**如何获取服务器的公共 IPv4 地址：**

如果使用云服务提供商（如AWS、DigitalOcean、Azure），可在控制台或面板中找到你的服务器实例，并找到其公共 IP 地址。

如果有自己的物理服务器，你可以通过访问网站WhatIsMyIP 或使用命令行工具（例如，在终端中运行 curl ifconfig.me）获取公共 IP 地址。


<br>

## CNAME 记录

填上面两个A就不用填这个，这个是填你的www 子域名，和上面那个二选一。

主机名（Host）： 通常是 www。

目标（Value）： 这是你的域名（比如example.com）。

CNAME 记录是选填的，通常用于将 www子域名指向主域名，以确保两者都能正确访问博客。

TTL（Time to Live）是DNS记录在缓存中保存的时间，通常以秒为单位。

当你在NameSilo或其他域名注册商添加A记录或CNAME记录时，你可以选择设置TTL。TTL的设置影响了DNS变更生效的时间以及对DNS查询的缓存持续时间。

一般来说，TTL一般填3600秒就好（1小时），因为较短的TTL可以使DNS更迅速地生效，但同时也增加了DNS服务器的负担。如果频繁地进行DNS更改，可以选择将TTL设置得更短，以便更快地应用变更。

具体的TTL设置取决于你的需求和实际情况。如果不经常更改DNS记录，使用较长的TTL可能更有效，因为它会减轻DNS服务器的负担并提高性能。

总之，将TTL设置为3600秒是为了在进行DNS更改时能够更迅速地生效。可根据自己的需求来选择TTL的值。

<br>


# 使用Cloudflare解析DNS

<br>

参考教程：

[利用Cloudflare修改DNS服务器](https://lucumt.info/post/hugo/migrate-github-blog-from-http-to-https/)


[利用Cloudflare为基于GitHub Pages的Hugo博客添加HTTPS支持](https://zhaouncle.com/hugo_03/#%E4%BA%8C%E5%88%A9%E7%94%A8cloudflare%E4%B8%BA%E5%9F%BA%E4%BA%8Egithub-pages%E7%9A%84hugo%E5%8D%9A%E5%AE%A2%E6%B7%BB%E5%8A%A0https%E6%94%AF%E6%8C%81)

[hugo+github page搭建自定义域名的https博客](https://h11ba1.com/2021/06/05/hugo+github%20page%E6%90%AD%E5%BB%BA%E8%87%AA%E5%AE%9A%E4%B9%89%E5%9F%9F%E5%90%8D%E7%9A%84https%E5%8D%9A%E5%AE%A2/)

<br>

# dns解析之我的修正

因为网站的IP是会变化的，所以直接添加这四个github page网站给的IP地址为A记录。

185.199.108.153

185.199.109.153

185.199.110.153

185.199.111.153

<br>

# GitHub pages部署

<br>

**如果 Hugo 博客托管在 GitHub Pages，需要指向 GitHub 提供的域名。**

通常，GitHub Pages 的域名是 <username>.github.io（其中 <username> 是你的 GitHub 用户名）。

如果你在仓库的设置中配置了自定义域名，那么使用自定义域名。

步骤如下：

1. 打开你的 Hugo 项目的 GitHub 仓库。
   
2. 进入仓库的 "Settings"（设置）选项
   
3. 在 "GitHub Pages" 部分查看你的 GitHub Pages 网站的域名。如果设置了自定义域名，那么使用这个自定义域名。



例如，如果你的 GitHub Pages 网站是通过 [https://<username>.github.io/](https://username.github.io/) 访问的，那么你的 CNAME 记录可能如下所示：

- 主机名（Host）：www（或者其他子域名，根据你的需求）
- 目标（Value）：<username>.github.io

记住，在设置 CNAME 记录之后，DNS 记录需要一些时间来生效，通常在几小时内，因此你可能需要等待一段时间，然后在浏览器中输入子域名来测试。


<br>

**如果 Hugo 博客托管在 GitHub Pages，你想使用自定义域名，将github.io的子域名替换为你已经买好的域名：**

<br>

1. 打开 Hugo 项目的 GitHub 仓库。

<br>

2. 进入仓库的 "Settings"（设置）选项。
   
<br>

3. 自定义域名设置：

  在 "GitHub Pages" 部分：

  如果博客已启用 GitHub Pages，确保选择了 main 分支（或源分支）作为 source。

  在 Custom domain 字段中输入自己的域名，例如xxxx.blog，这将在 GitHub Pages 的仓库生成网站，并在自定义域名上链接该网站。

<br>

4. DNS 配置：

在 Namesilo 或其他域名注册商处，确保域名的 DNS 设置包括正确的 A 记录，将子域名（例如 www.xxxxxx.xxxx）指向服务器的公共IPv4 地址

<br>

1. 等待 DNS

记录生效，可能需要一些时间（通常在几小时内），以确保域名正确地映射到 GitHub Pages。

<br>

6. 测试和验证：

在浏览器中输入域名和子域名，确保Hugo博客能够正确加载。

如果一切设置正确，博客应该能够通过自定义域名访问。

<br>

<br>


## 其他参考教程

**[冰布子的简易 Wordpress 建站指南](https://blog.cysi.me/2022/05/guide-for-building-a-wordpress-site.html)（虽然是wordpress但是域名这块写得很详细）**  

[配置GitHub Page域名](https://zhuanlan.zhihu.com/p/582629584)


[使用自定义域名来访问GitHub上部署的hugo博客——GitHub Pages](https://cloud.tencent.com/developer/article/1834163)


[GitHub博客绑定自定义域名](https://ftzzloo.com/github-pages-and-domain-name-setting/#%E6%B7%BB%E5%8A%A0A%E8%AE%B0%E5%BD%95)

<br>

**问题排除参考：**  

[How to Fix Cloudflare Error 522](https://www.hostinger.com/tutorials/error-522)

[Troubleshooting custom domains and GitHub Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/troubleshooting-custom-domains-and-github-pages)

<br>