@[TOC](slider进度条实现)
## 带进度条的异步加载场景切换
   
   **作业ing，我想实现带进度条的场景切换功能：这里使用UI组件Slider完成**
   
   ### 具体实现：
 
 1. 需要三个场景：【Menu】——【Loading】——【VRsubway】
 2. 用SceneManager.LoadSceneAsync方法可以实现异步加载，即加载的时候，当前场景不变。
 3. 用AsyncOperation类来获取加载进度。
 4. Slider组件来显示进度。
 
 ### 简单搭建一下【Loading】场景
 ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/052b84ba07fafcc8444ab29cbd48c10f.png)
【bg】image组件，挂载背景图
【slider】进度条组件
【tips】提示信息文本Text

### 代码实现：
创建Loading脚本：

引用：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a35a5c917b604a5c6a296ee3fb72ab71.png)
定义，初始开启协程：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/da576d99db644a461d6d93e30bdb8110.png)
异步加载：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/b665216903122c7e46fd3e1615862b97.png)
### 运行效果：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/b73c32b2e347a7e91528f0b3d33f4cdf.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/6f2e5b5fec5456d1f62321e0db78f1c1.png)
### 总结
对此理解得还不够透彻；功能看上去是实现了，但是效果看上去可能不太满意，前面加载的时候会卡顿，暂时弄不清楚是什么原因，后面学习到优化的方法再说明一下，欢迎各位指教！！！
