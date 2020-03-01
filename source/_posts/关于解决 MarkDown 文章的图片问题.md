---
title: 关于解决 Markdown 文章图片问题
date: 2019-03-07 01:47:46
categories: 
- 工具
---

![图片取自 Zoommy](http://upload-images.jianshu.io/upload_images/1214187-f8468c0badb575ce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Alfred 是 Mac 上的利器，敲击键盘之间就可以帮你打开应用、浏览文件夹、文件内搜索、执行终端命令，还可帮你做一些繁复但有规律的事情。

用 MarkDown 写文章时，就会碰到『插入图片』这件繁复但有规律的事。在文章中插入一张图片的流程是：

1. 找到图片
2. 上传图片
3. 获取图片链接

为了写文章时方便插入图片，或者在其他用途中使用图片链接，最近写了一个 Alfred workflow，名叫 ```SmartPic```，可以帮你一键上传图片并获取图片链接。Alfred workflow 文件和相关代码已放在 GitHub ，[点击查看 SmartPic](https://github.com/QinGeneral/SmartPic)。

以下是该工具的简介和使用方式。

# SmartPic 简介和使用

SmartPic 是一款 Alfred workflow，可以方便大家上传图片到云上，并获取图片链接，可用于 Markdown 写文章时添加图片或其他用途。

> 注：SmartPic 基于 Python 2.7，请确保已安装 Python。

## 安装

下载 SmartPic.alfredworkflow 文件后，双击即可。当然，前提是已安装 Alfred（请自行安装）。

## 配置

SmartPic 其实是将图片上传至腾讯云存储桶，所以你需要自行申请免费的存储桶，并将存储桶相关参数配置到本地即可。

1. 登录腾讯云创建存储桶 [点击创建](https://console.cloud.tencent.com/cos5/bucket)。点击会打开腾讯云，界面如下图，点击其中的```创建存储桶```进行创建。
![创建存储桶](http://upload-images.jianshu.io/upload_images/1214187-ae19576086ef8e42.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. 创建完成后的界面如下图：
![创建后界面](http://upload-images.jianshu.io/upload_images/1214187-4c5536e8e6c760bd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. 点击左侧的密钥管理，可以找到配置参数中的 secret_id、secret_key 两项
![查看密钥](http://upload-images.jianshu.io/upload_images/1214187-ff75d03c44abb162.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4. 点击要使用的存储桶，进入下图界面。各个参数的对应值已在图中标出，包含 bucket、region、blog_prefix 三项。
![存储桶参数](http://upload-images.jianshu.io/upload_images/1214187-733bfe1eb29e2629.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5. 呼出 Alfred，输入 SmartPic 命令，按下 Enter 进入菜单界面，并选择 ```config``` 菜单（如下图），在打开的文件中以 json 方式配置上述步骤中找到的 secret_id、secret_key、bucket、region、blog_prefix 五项参数，替换 ```******``` 部分即可，以下述代码为例。
![配置 SmartPic](http://upload-images.jianshu.io/upload_images/1214187-1f8bb2a15c358cff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
    ```config.txt```文件的配置格式

    ```json
    {
        "secret_id": "******",
        "secret_key": "******",
        "region": "ap-guangzhou(只取英文)",
        "bucket": "******",
        "blog_prefix": "******"
    }
    ```

## 使用

### SmartPic 命令

此命令包含以下四个命令：

- ```config```：配置存储桶参数
- ```list```：查看已上传图片列表，移动到指定项：Cmd + Y 可查看图片；Enter 可复制图片链接
- ```uploadPic```：上传图片：搜索出图片，Enter 后即可上传，上传完成会自动复制链接到剪切板
- ```help```：查看帮助文档

### SmartPicUploadPic 命令

上传图片：搜索出图片，Enter 后即可上传，上传完成会自动复制链接到剪切板。

> 注：本文的图片均用 SmartPic 上传获取链接。

>版权声明  
本文首发自简书，搜索作者 QinGeneral
同步发于CSDN博客，搜索作者 QinGeneral  
同步发于微信公众号：AndroidRain  
无需授权即可转载，甚至无需保留以上版权声明；  
转载时请务必注明作者。