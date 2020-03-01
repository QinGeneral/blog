---
title: Cocos 中 JSC 文件解密和重新加密的脚本
date: 2019-03-09 02:55:31
categories: 
- Cocos
---

![图片源于zoommy](http://upload-images.jianshu.io/upload_images/1214187-c58b9c0f9e58c566.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

好久没更，正好最近毕业生找工作的季节，几篇面经的文章多了一些赞，也顺带涨了几个粉。

从文章统计数据来看，浏览量比较多的还是面经，而非平常的技术文章。以前在文章里也说过，一个人能挣的钱取决于他的社会价值，一个人能否找到好工作在于其本身实际素养。虽然面试时能够包装一下，但是过度包装也很容易被戳破。面经固然可以起到一些作用，但是读一些技术文章和实践编码才是成长的关键。希望找工作的同学读面经时，遇到不会的一定要逐个突破掌握，才能让面经起到应有的作用。否则纵然你读100篇面经，也涨不了知识。

另外，做一个项目不仅仅包含写代码这一部分。比如Android项目还要包含自动化构建等等内容，一些操作靠人来完成耗时耗力，如果能够实现一些能够解放人力、提高效率的脚本是十分有用的。

最近写了一个Cocos中 jsc 文件解密和重新加密的脚本，可以提升Cocos中比如热更新时的打包效率。项目地址：[点击跳转GitHub](https://github.com/SNGfamily/cocos-jsc-endecryptor)

## 简介

通过阅读Cocos2dx源码发现，其脚本加解密用的就是xxtea加密和解密。

CocosCreator构建过程为：

1. 工程用到的所有js脚本聚合为project.js等几个脚本
2. 如果勾选“Zip 压缩”选项，会进行压缩project.js，会减少很多体积，进而可以减少包大小
3. 使用xxtea进行加密上述文件，生成project.jsc
4. 将project.jsc打包到apk、ipa等安装包中

在程序运行时，正好做了相反操作：

1. 使用xxtea进行解密
2. 如果勾选“Zip 压缩”选项，进行解压缩
3. 调用js代码

此脚本就是用于CocosCreator加密编译后 jsc 文件解密为 js 文件和 js 文件加密为 jsc 文件。

CocosCreator构建时，是否勾选Zip压缩选项决定了使用脚本的参数不同。在CocosCreator的构建面板下图的位置中，查看加密密钥和是否开启Zip压缩。
![image](http://upload-images.jianshu.io/upload_images/1214187-1eb40ddfc23d4e50.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 此脚本在 macOS High Sierra 10.13.6 系统，Python 2.7 下运行正常，其他环境未测试

## 使用说明

命令行使用：

1. 如果使用加密功能，第二个参数设置为 **encrypt**；如果使用解密功能，第二个参数设置为 **decrypt**。此参数为必选参数

2. 如需设置加密密钥，添加 --key 或 -k 参数，并跟上加密密钥字符串。如不设置，会在命令行中提示输入

3. 如需设置为非压缩方案，添加 --nozip 或 -n 参数，并设置为 true。如不设置，默认为压缩方案
    > 非压缩方案是指Cocos编译时没有勾选“Zip 压缩”选项

4. 找到CocosCreator编译出来的 .jsc 文件，一般在工程目录下 **build/jsb-default/src** 文件夹下。你可以在脚本运行时，根据提示输入文件的路径来指定对应文件。也可以添加 --path 或 -p 参数，设置为文件路径。如不设置，会在命令行中提示输入

5. 运行脚本即可
    - encrypt：解密后文件路径为 **decryptOutput/decrypt.js**
    - decrypt: 加密后文件路径为 **encryptOutput/projectChanged.jsc**

6. 举例：
    - ./edc.py encrypt --key yourkey --nozip true
    - ./edc.py decrypt --nozip true
    - ./edc.py decrypt

其他Python脚本中引用：

1. 下载edc.py文件放到你的脚本目录下，通过 **import edc** 进行导入
2. 直接调用 edc.decrypt(is_zip, key, jsc_path) 或 edc.encrypt(is_zip, key, js_path) 即可，可参考 edcExample.py 文件

> 如果是非交互式脚本，请务必在调用方法时传入有效的参数，并保证其正确性

## 参数说明

| 参数名 | 缩写 | 是否必须 | 默认值 |
| ----- | ----- | ---- | ----- |
| encrypt/decrypt | 无 | 是 | - |
| --key | -k | 否 | - |
| --nozip | -n | 否 | false |
| --path | -p | 否 | - |

## 参考文章

- [形同虚设的cocos默认加密](http://blog.shuax.com/archives/decryptcocos.html)
- [cocos2dx lua 反编译](https://bbs.pediy.com/thread-216800.htm)

>版权声明  
本文首发自简书：搜索作者 QinGeneral
同步发于CSDN博客：搜索作者 迷失  
同步发于微信公众号：AndroidRain  
无需授权即可转载，甚至无需保留以上版权声明；  
转载时请务必注明作者。

![扫码关注微信公众号](http://upload-images.jianshu.io/upload_images/1214187-6a3f1c6079560129.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/150)