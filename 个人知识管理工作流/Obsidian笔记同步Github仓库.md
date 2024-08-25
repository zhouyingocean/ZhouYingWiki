
记录本知识库备份至Github仓库的工作流。

# 准备工作

## Git安装

1、前往[Git官网](https://git-scm.com/downloads)下载并安装
![[Pasted image 20240825103341.png]]
按照安装程序默认勾选的配置安装即可。
2、验证Git是否安装成功
按Win + R 打开Cmd命令行窗口输入：git help有输出即可。
![[Pasted image 20240825104636.png]]

## 准备Github账户和远程仓库

1、前往[Github官网](https://github.com/)注册并登录一个Github账户。
2、点击右上角+号创建一个仓库
![[Pasted image 20240825105940.png]]
填写仓库信息。
![[Pasted image 20240825111133.png]]

## SSH密钥配置

1、首先在本地配置Github账户。
打开Git Bash，输入以下命令：
>git config --global user.name “用户名”
>git config --global user.email "邮箱"

![[Pasted image 20240825112031.png]]
2、生成SSH密钥文件
继续输入命令：
> ssh-keygen -t rsa -C "邮箱"

根据提示点击回车键三次出现以下内容即为创建SSH文件成功。
![[Pasted image 20240825112610.png]]

3、将公钥id_rsa.pub配置到Github账户

根据上面步骤创建的信息找到.ssh\id_rsa.pub文件，使用记事本打开并复制里面的内容，打开github主页，进入**个人设置 -> SSH and GPG keys -> New SSH key**：
![[Pasted image 20240825113814.png]]

4、验证本地是否能通过SSH连接到Github

Git Bash输入命令：ssh -T git@github.com，按提示输入yes显示以下内容即证明ssh配置成功
![[Pasted image 20240825120417.png]]

## Obsidian安装插件Git

在Obsidian笔记软件里进入设置 -> 第三方插件 -> 社区插件市场，点击浏览并搜索 "**Git**" ,点击安装并启用。
![[Pasted image 20240825121804.png]]

如果Obsidian侧边栏没有出现Git Control View，可以按下 Ctrl + P，搜索并点击 `Obsidian Git: Open Source Control View` 即可出现。
![[Pasted image 20240825123134.png]]

插件的顶部按钮对应的一些Git常用操作：
1. Backup：备份，提交所有的更改，并且执行推送。
2. Commit：确认提交，但不推送。
3. Stage all：存储当前的变更。
4. Unstage all：取消存储变更。
5. Push：推送到远端，可以理解为推送到 Github。
6. Pull：从远端拉取到本地，可以理解为从 Github 拉取最新数据到本地。
7. Change Layout：改变下方文件的排布方式。
8. Refresh：刷新当前的文件变更情况。
### Git插件配置

1、打开Obsidian，进入设置 ->右侧边栏底部 第三方插件-> Git。
![[Pasted image 20240825144403.png]]
根据需要配置备份间隔、自动拉取等选项，每次你做了更改，Git会根据你设置的间隔自动备份，或者你可以点击工具栏上的Git图标手动备份。
# 将知识库笔记Push到远程仓库

1、先到github复制自己的ssh凭证
![[Pasted image 20240825135056.png]]

2、在知识库所在目录右键，选择**Open Git Bash here**
![[Pasted image 20240825135219.png]]

3、在终端输入以下命令：

>git init  //git初始化
>git add --all //添加当前目录下的所以文件
>git commit -m "first commit" //提交日志
>git remote add origin git@github.com:zhouyingocean/ZhouYingWiki.git     //这里替换成自己的库
>git push -u origin master  //推送到远程仓库分支master

显示以下信息即为推送成功
![[Pasted image 20240825142347.png]]

之后就可以直接在Obsidian 笔记软件内使用Git插件推送同步了。
# 如何删除误同步的文件或者忽略某些文件？

## 删除git仓库上的目录和文件

1、可以看到我这里将.obsidian和欢迎.md全部误推送到仓库了，现在我要将它们从远程仓库删除。

![[Pasted image 20240825150357.png]]

- 删除远程目录
使用命令：==git rm -r --cached .obsidian==
- 删除远程文件
使用命令：==git rm 欢迎.md --cached==
2、提交更改并推送
git commit:
![[Pasted image 20240825152231.png]]

git push:
![[Pasted image 20240825152349.png]]
可以看到仓库上已经删除了相关文件和目录：
![[Pasted image 20240825152706.png]]

## 忽略不需要推送的目录和文件

1、在笔记目录下新建文本文件，改名为==.gitignore==，在文件中添加需要忽略的文件目录如：.obsidian
其他文件需要加斜杠”/ “才能识别。
![[Pasted image 20240825154139.png]]
这样在你之后的提交推送中都不会上传这些忽略的文件。