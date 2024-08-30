## ***unity之使用VRTK实现手柄发射射线和漫游功能***
@[TOC](目录导航)

通过学习VRTK自带新案例【002-Pointers StraightPointer】、【003-Pointers BezierPointers】、【004-Locomotio Teleporting】,实现了我前期需要的功能。
### ***【002-Pointers StraightPointer】案例说明***
在该场景中，你触摸触摸板后出现一条直线，按下触摸板放开后会对射线触碰到的物体进行选择，可以看到物体的边框颜色有所变化，同时在unity控制台会打印出所选择的物体的名字、手柄与物体之间的距离及射线顶端在物体上的位置。
### ***【003-Pointers BezierPointers】案例说明***
在该场景，你触摸触摸板后，手柄发射一条曲线，按下并释放触摸板进行选择。可以看到场景中有三个选项图块，选择左边的图块可以将射线变为线性的，选择右边的可以将射线样式变为自定义的样式，在该场景中自定义的样式为将射线顶端与物体接触后的样式变为光环，选择中间的图块可以将样式设置成贝塞尔曲线的默认样式
### ***【004-Locomotio Teleporting】案例说明***
在该场景，按下触摸板发射射线，松开可以传送到指针光标的位置，可以传送方块到被网格碰撞器包围的石头上，高度不受限制，同时通过脚本对灰色方块进行限制，使其不能成为传送地点。

可以自行体验学习。

为了方便后期交互，个人开发习惯：左手柄发射曲线瞬移，右手柄发射直线交互。之前我已经搭建好了VR开发的基本环境，不懂的可以看我之前的文章，下面开发实现发射射线和瞬移。
1、在【VRTK_Scripts】下添加空物体命名为【PlayArea】，为其添加VRTK组件【VRTK_DashTeleport】(个人比较喜欢用这个，实现传送的脚本很多，自行学习使用)：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/7d238090663f4cb2539349192fb22664.png)
2、为有手柄添加组件【VRTK_ControllerEvents】(监听手柄事件的脚本)【VRTK_StraightPointerRenderer】(发射直线的的脚本，可以更改射线样式和颜色)【VRTK_Pointer】(渲染射线指针的)将本物体的拖入，如下图：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/c95fc26db10a660f4e3d5815b7e37bf2.png)
3、同理，为左手柄添加【VRTK_ControllerEvents】【VRTK_BezierPointerRenderer】(这个是发射曲线的脚本)【VRTK_Pointer】
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/26ad360523729794dfb8b133f017d147.png)
这里，为了指针光标点更好看一点可以如下图所示设置：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/889515befdc7db097775cdd5e8fcc261.png)
也可以自己学习制作自己喜欢的样式。至此完成基本配置。
### ***功能测试***
有手柄发射射线漫游，这里使用的是模拟器，按住键盘上【Q】发射射线，松开瞬移：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/fe7c66fb9f0e54391a80ab048a83dfa8.png)
左手柄发射射线漫游：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/49fa5f9058ee52f416a82501221d1ccc.png)
基本功能已经实现了，后面再完善吧。
