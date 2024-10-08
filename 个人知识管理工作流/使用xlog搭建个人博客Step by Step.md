# 我为什么需要一个个人博客？

2024年8月这个时间刚好是工作了3年的时间点。三年间，见过不少人和事，有了些许社会的阅历，愈发的觉得内心空虚。于是，我觉得我需要学习更多的东西，学习后我希望能够分享出来，分享可以让思想产生多维的碰撞，在碰撞上可能产生新的火花，以此来用输出倒逼输入，所以我希望拥有一个可以分享的个人博客。
![mind-544404_640](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/mind-544404_640.webp)
很喜欢的两句话：
>总会有一些人，需要的是一个安静、内向与创作的互联网。

>书写是为了更好的思考！

我想把个人博客当做世外桃源，让我可以静下心来慢慢耕耘。

# xlog是什么？

xLog是一个现代化的开源博客系统，使用区块链技术存储博客数据，包括配置、文章、评论等。它具有丰富的交互功能，可以关注博客、评论、点赞文章，并将文章铸造为NFT。xLog基于proselog项目开发，使用Next.js + Tailwind CSS + TypeScript + TanStack Query构建，具有完善的开发体验。它使用Crossbell区块链进行社交活动，无需购买gas费用。每个博客都是一个属于用户的NFT，配置和文章存储在NFT中。----源自xlog创始人博客。
![Pasted image 20240803165030](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240803165030.png)
想了解更多关于xlog的信息，请前往以下链接：
1、[xlog官网介绍](https://xlog.app/about)
2、[第一个开源链上博客系统 xLog](https://diygod.cc/xlog?locale=zh)
3、[开源项目介绍xlog——区块链上的博客系统](https://www.isharkfly.com/t/xlog/14491)]
4、[ 谈谈我对xLog（基于Web3和加密钱包等技术的博客平台）的理解](https://linux.do/t/topic/104342)]
# 我使用xlog的理由

从毕业开始一直有写博客的习惯，大多是关于Unity的技术博客，发布在某SDN上。最近感觉某平台从上到下真的烂透了（就不一一吐槽了，懂的都懂），加上迫切的希望打造自己的个人知识库，于是就开始为自己物色一个可以分享个人知识库的的开源博客系统。

在网上搜寻了一大堆流行的个人博客框架：hexo（之前有用过，三分热情，没有坚持写作）、Hugo、Halo、VuePress、MkDocs、wordPress。
也罗列了一些我关于个人博客最基本的需求：
- 必须支持MarkDown文件
- 基础的博客功能（订阅、点赞、评论、自定义域名、导航栏等）
- 主题看得过去（可简约可酷炫可自定义）
- 搭建成本低、拒绝繁琐的配置和安装各种环境
- 多语言切换
- 对PC、移动设备友好
- 数据安全、性能也有一定要求

调研了一圈发现大部分主流框架都不太符合我的需求，而目前来说的还比较小众xlog却能映入眼帘。现在我也只是抱着尝试的心态使用xlog进行博客创作。希望未来xlog的生态会越来越好，我也能一直坚持写作分享。
# 开始折腾？No

拒绝繁琐的折腾，真的如xlog官网所说5分钟就拥有自己的个人博客！

以下搭建过程基于谷歌浏览器，这里也建议使用谷歌浏览器。
## 安装一个虚拟币钱包

1、进入[xlog官网](https://xlog.app/)，点击右上角“连接”，我这里选择第一个钱包MethMask
![Pasted image 20240804145542](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804145542.png)
2、点击Download here安装一个钱包的浏览器扩展插件。
![Pasted image 20240804145654](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804145654.png)
3、点击下载适用于谷歌（此处建议使用科学上网方式，当然如果没有，这个插件也适用于Firefox、Edge等）
![Pasted image 20240804145947](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804145947.png)
4、点击Add to Chrome，在弹出来的窗口选择添加扩展程序
![Pasted image 20240804150335](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804150335.png)

![Pasted image 20240804150539](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804150539.png)

5、同意条款，点击创建新钱包，根据提示勾选一些设置（特别提醒要记住自己的**私钥助记词**），最后将其固定在浏览器上。
![Pasted image 20240804150738](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804150738.png)
  
![Pasted image 20240804151226](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804151226.png)
至此，你就正式拥有了一个属于你的以太坊钱包。
## 使用钱包登录你的xlog

1、重新回到xlog官网，刷新一下网页，再次点击“连接”，点击MetaMask后会弹出钱包窗口让你授权登录xlog，按照提示允许即可。
![Pasted image 20240804155407](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804155407.png)

2、登录成功之后，就会看到这里显示你的账号信息了，紧接着你可以点击我的xLog，再进去之前会弹出创建xlog角色的窗口，填写你的名称等内容即可。首次登录会给新人赠送0.02$CSB（只需要跟随页面指引点击验证和Claim即可，不需要发推）。
![Pasted image 20240804161133](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804161133.png)
![Pasted image 20240804161306](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804161306.png)
![Pasted image 20240804162156](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804162156.png)

## 进入个人主页
嗯，还不错，下方还显示有独特的区块链标识。
![Pasted image 20240804171155](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804171155.png)
## 进入仪表盘（博客后台）

可以在线写文章（支持实时渲染md），也支持导入md文件，至此完成xlog个人博客的搭建，接下来就是进行文章创作了。（如果只是发布文章的话0.02$CSB够用挺久了，不够了也可以免费领，领取地址：[水龙头](https://faucet.crossbell.io/)
![Pasted image 20240804161952](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804161952.png)
# 发布第一篇xlog博客

依次点击仪表盘--文章--新建文章，使用Markdown语法创作第一篇xlog博客。
![Pasted image 20240804174226](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804174226.png)
点击发布，并确认消耗虚拟币即可。
![Pasted image 20240804174347](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804174347.png)
![Pasted image 20240804174427](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804174427.png)
好了，现在就可以去主页刷新查看刚才发布的文章了
![Pasted image 20240804174846](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240804174846.png)
# 总结

首次体验xlog还是不错的，就搭建流程来看，确定挺快的，虽没有深入使用，但现在来说xlog功能也基本满足我对个人博客的要求，后续稳定了，打算买个域名。再结合自己使用笔记软件Obsidian整理的个人知识库文章托管到github上，并借助其他工具自动同步到xlog中。

	希望通过个人博客去记录与分享，去与人类建立连接，去找寻志同道合之人，去往诗和远方。