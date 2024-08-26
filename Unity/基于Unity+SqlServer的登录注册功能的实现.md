***基于unity2018.3.6+sqlserver2014实现的登录注册功能。***

我给我的VR系统做了一个简易的登录注册功能。
1.在unity里搭建了一个登录面板如下图：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/b1e00fb213c167f2bebf1cad612b3422.png)
往视图里添加3个Text（登录信息的提示、账号密码输入提示），3个button（用来挂载登录注册事件、退出系统）和两个inputText（用于输入账号密码）。
2.搭建注册面板：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/7fd3363e2edb520a5e59a18ed046fa97.png)
跟登录面板一样创建游戏对象就行了，不同的是，这里加了一个确认密码的输入框，不过这里的确认密码我没有加任何代码逻辑，只是个装饰，可用可不用，后面完善功能时再添加也行。
3.unity连接数据库前的准备——引用数据库DLL文件：
创建文件夹Plugins，添加4个dll文件：![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/982d15bcde99fd948a97862286a7e1f4.png)
注意：连接不同数据库添加的dll文件不同，这里我们连接sqlserver，用这四个就够了，这些dll可以在网上找，也可以在自己unity的安装目录下找到：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/705b4df9ee3505c008629b70e82d1d57.png)
这里我遇到一个问题，就是我unity 2018.3.6f1导入dll文件报错：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/b32e5373c99406b60b8f05cfca2500fb.png)
网上查了解决方法，主要是说DLL的.NET版本需与脚本运行版本不对应，这里我们就要做一下更改了——找到File/Build Settings/Player Settings/Other Settings/Configuration，![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/b1147b3257d5b119cf526d6bdc9f5c2d.png)
选择对应版本，重启unity即可解决。好了，现在我们可以开始写脚本实现功能了。
4.登录功能的实现：
（1）首先设计一下数据库的内容：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/ef40b58eff54111e24c2c16164e19828.png)
（2）代码+可视化实现：
创建一个脚本userLogin：``
首先我们添加一些引用：

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/7689c0307835e67f18387071f5186e84.png)
（如果前面没有添加dll文件，这里就无法引用，下面自然也不能连接数据库了）
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/badbbb79ba338657b36a161092b8abb8.png)
定义两个公共inpuField组件，一个静态文本
![](https://i-blog.csdnimg.cn/blog_migrate/994ccfe6af5e38ca0095f1aff04689ad.png)
在这里，我们要在刚开始的时候获取一下登录提示信息文本组件，在视图中，给这个Text组件添加一个标签LoginMessage。
（3）下面写一个登录的方法，连接数据库访问数据，与输入的数据对比：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/30b0f65e8e1362cd7c19f1a52de1e580.png)
![在的这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/83064469c2890a20fc978e427bd29bd9.png)
server=“计算机ip地址/电脑用户名，默认127.0.0.1为本地地址，也可以用localhost”、database=“自己创建的数据库名称”、uid=数据库用户sa、pwd=数据库密码，可自定义。其他sql语句，自行学习。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/dca9cc19804cba0ad318bbe904e46928.png)

（4）测试登录功能：
无输入：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/0a3f6d8c677d73cfba06df26fbde0da4.png)
数据库不存在的账号：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/63a47c1ed60ef0bbb9ecdf844ca7d2f2.png)
密码错误：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/1985a10a460559dbed22f39123c03b6f.png)
账号密码匹配成功登录

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/fe8f90cf96961da3f264df574b711486.png)
5.登录功能的实现：
（1）直接在注册按钮添加鼠标点击事件，设置bool setactive的属性：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/c7000fd67e55c0ba1e731cd14f6cbfab.png)
（2）注册的实现就是往数据库添加数据：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a3314391800d036f52b41cbe2140fe5c.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/5d5731a7b3bf6b62094e56d67ac2782d.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/d1f8243d25b668a6e6a76d1351df984a.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/df423569e14057d9c41586ad64984915.png)
（3）测试注册功能：
注册相同账号时：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a434e64929baacf779dcaaffd89964e3.png)
注册新账号成功登录：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/f9f4825cbcaa69cc1ed0442ffd2792e1.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/e97b0061f1be62aeea63e0b7951a9fcb.png)
好了，到这里，我的登录注册小功能总算是完成了。
