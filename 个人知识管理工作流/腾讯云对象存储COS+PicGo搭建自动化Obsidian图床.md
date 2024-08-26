![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240826160004.png)

# 前言

考虑到需要将Obsidian的笔记分发多平台，其中最繁琐的工作就是需要将文章中的图片一次次的复制粘贴，为了减少这个重复的工作量，这里使用的一种解决方案就是利用**腾讯云对象存储**作为图床工具，借助图片上传工具**PicGo**和Obsidian的插件**image auto upload plugin**搭建自动化上传图片流程。

# 准备工作

## 注册腾讯云并开通对象存储服务

1、访问[腾讯云官网](https://cloud.tencent.com/document/product/436/6240)注册一个账号并实名验证，建议使用微信注册。
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826143312.png)
2、进入控制台之后，选择对象存储，首次开通有6个月的免费额度资源包哦
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826143349.png)

3、选择创建存储桶
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826143838.png)

4、填写基本信息，必须勾选具有**公有读**权限的选项，确保你之后上传的图片外网能访问。
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826144324.png)

5、高级配置默认即可，当然也可根据需求选。
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826144806.png)
6、成功创建之后就可以创建一个文件夹来管理之后上传的图片了
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826145510.png)

## 获取密钥信息

1、在控制台常用工具--秘钥管理--点击访问密钥。
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826150902.png)

2、点击新建密钥，可以复制粘贴另存保管好。（后面会在PicGo用到）
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826151023.png)

## 安装PicGo

1、前往[PicGo官网](https://picgo.github.io/PicGo-Doc/zh/guide/#%E4%B8%8B%E8%BD%BD%E5%AE%89%E8%A3%85)选择任意下载源下载安装即可。
2、安装好打开软件
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826151714.png)

# PicGo配置腾讯云COS

详细官网文档可访问：[PicGo配置手册](https://picgo.github.io/PicGo-Doc/zh/guide/config.html#%E8%85%BE%E8%AE%AF%E4%BA%91cos)

我这里选择v5版本配置：
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826152700.png)

1、APPID、SecretId和SecretKey从密钥管理那里查看。
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826153035.png)
2、bucket名以及存储区域代号在你得控制台存储桶列表获取。
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826153152.png)

3、测试一下是否可以上传成功
回到PicGo上传去，选择腾讯云COS，随便上传一张图片
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826153619.png)
成功上传云，下一步设置Obsidian自动粘贴上传。
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826154047.png)

# Obsidian安装插件image auto upload

1、在Obsidian里打开设置--第三方插件--社区插件市场--搜索image auto upload安装并启用。
![](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240826154907.png)

2、注意：使用默认设置即可，==并且保持PicGo软件在运行状态，才能实现自动上传==
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240826155305.png)
之后在Obsidian写笔记时每次粘贴图片都会自动上传到腾讯云对象存储，而不会保存到本地了，会自动返回一个图片链接。

# 批量上传以前文章的所有图片

1、在需要上传的文章使用快捷键==Ctrl + P==打开命令面板，输入==upload all images==并回车，开启自动上传。而且还能替换原始图片链接。perfect!
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240826161246.png)

