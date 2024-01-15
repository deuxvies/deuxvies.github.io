---
title: "发布文章测试帖"
description: 建站测试
date: 2024-01-02T17:19:10+08:00
image: 
categories: 技能
tags: 
    - 建站记录
hidden: true
comments: true
toc: true
encryption: true 
slug: "发布文章测试帖"

---

这是受密码保护的文章内容。

# 文本效果语法 (✔)

## 文本折叠
{{< toggle "折叠↓" >}}
实际使用时别忘了换成双括号！
{{< /toggle >}}


## 文本模糊
<span class="blur">手动打码效果
</span>


## 文本黑幕
<span class="shady">数据删除！数据删除！
</span>

## 文本位置
{{< align left "文字居左" >}}
{{< align center "文字居中" >}}
{{< align right "文字居右" >}}

## 摘录引用

{{< blockquote author="George Orwell" title="《1984》" >}}
There is no possibility that any perceptible change will happen within our own lifetime. We are the dead. Our only true life is in the future. We shall take part in it ashandfuls of dust and splinters of bone. But how far away that future may be, there is no knowing.
{{< /blockquote >}}

# 插入图片

![图1](images/1.png)

调整大小：

<img src="/images/1.png" alt="Alt Text" style="width: 100px; height: auto;">


## 轮播图test(失败)


{{< imgloop "images/0.png,images/1.png,images/23.png" >}}

## 瀑布流(失败)

markdown内嵌

<gallery>
    <img src="images/v13.png" alt="" width="200" height="auto">
    <img src="images/v1.png" alt="Alt Text" style="width: 100px; height: auto;">
    <img src="images/v3.png" alt="Alt Text" style="width: 100px; height: auto;">
</gallery>


外链图片

<gallery>
    <img src="https://cn.bing.com/images/search?view=detailV2&ccid=GUiUnh3Z&id=ED5CB77EB75446D1888C1B04F591657EB641E110&thid=OIP.GUiUnh3ZAVW0KO4i2N7H_AHaE6&mediaurl=https%3a%2f%2fpic3.zhimg.com%2fv2-d1f733345b0d11ea4d1bde0e2511dbc8_720w.jpg%3fsource%3d172ae18b&exph=384&expw=578&q=%e4%b8%96%e7%95%8c%e6%97%85%e6%b8%b8%e8%83%9c%e5%9c%b0&simid=608042712618981344&FORM=IRPRST&ck=013AE326E8DBEBEEAED85C0F4D6F9EF2&selectedIndex=0&itb=0&ajaxhist=0&ajaxserp=0">
    <img src="https://cn.bing.com/images/search?view=detailV2&ccid=gLoEb4u2&id=FEFF4AE8F54B008A371FB95E8FCE970DDF6C8FB2&thid=OIP.gLoEb4u25t9BqIuzlWRBxQHaFL&mediaurl=https%3A%2F%2Fts1.cn.mm.bing.net%2Fth%2Fid%2FR-C.80ba046f8bb6e6df41a88bb3956441c5%3Frik%3Dso9s3w2Xzo9euQ%26riu%3Dhttp%253a%252f%252fpic.kuaizhan.com%252fg3%252f7e%252f2b%252f820b-ec18-45b3-a176-e12c1cdd5cb966%252fimageView%252fv1%252fthumbnail%252f640x0%26ehk%3DUXt3yu%252f1VP5lEJ5jWGl91oNfNCNvoiHxUjwCAhxotYw%253d%26risl%3D%26pid%3DImgRaw%26r%3D0%26sres%3D1%26sresct%3D1&exph=447&expw=640&q=%e4%b8%96%e7%95%8c%e6%97%85%e6%b8%b8%e8%83%9c%e5%9c%b0&simid=608045564469972034&form=IRPRST&ck=8763DB41672F0BBACEA92FA07C73671A&selectedindex=0&itb=0&ajaxhist=0&ajaxserp=0&vt=0&sim=11">
</gallery>

## 多图排版(失败)

![1](images/0.png)
![3](images/w.jpg)
![1](images/a2.jpeg)

# 时间轴test(失败)

{{< timeline date="2024-01-01" title="建站" description="test" tags="技能" date="2023" title="写文" description="test" tags="同人"  >}}

# neodb引用（✔）

{{< neodb "https://neodb.social/tv/season/1UMEf2NuQxnWLWDyso8Pwm" >}}
{{< neodb "https://neodb.social/book/3yPdW2Dl0Mv3sVCUX2Pllj" >}}


# pdf插入（失败）

{< pdf src="这里放pdf链接，本地文件当然也可以！跟md文件放在一个文件夹里就行。使用的时候请换成双括号。" >}

网页

{{< pdf src="https://www.ocha-festival.jp/archive/english/conference/ICOS2001/files/PROC/I-004.pdf" >}}

本地

{{< pdf src="【琴裕】水平线上的情人.pdf" >}}

# 插入网易云音乐 (✔)

{< netease XXXXXXXXX 0 >} //歌曲的id;是否自动播放(1为自动播放，0为手动播放)

{{< netease 1396731073 0 >}}

# 插入B站视频（✔）
{< bilibili XXXXXXXXXXX 0 >} //BV号，分p数，0/1为是否自动播放；使用记得双括号

{{< bilibili BV13J411d74C 0 >}} 

# 加密功能test

## 网页前端加密（✔）

参考[天堂错误文件-Loading：《hugo 装修日志 03》](https://naturaleki.one/post/loadinghugo%E8%A3%85%E4%BF%AE%E6%97%A5%E5%BF%9703/#%E6%96%87%E7%AB%A0%E8%AE%BE%E7%BD%AE%E5%AF%86%E7%A0%81%E8%AE%BF%E9%97%AE)操作后，在文章头部添加

password: "xxxx"  

password_hint: "xxxxx"

即可对显示的网页加密。

## 文章内部分内容加密（失败）

密码：花的日语罗马音（四个字母）

<!--more-->

{{< secret "hana" >}}


<!-- 这里放置需要加密的内容 -->

xxx

{{< /secret >}}

