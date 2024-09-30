
在虚拟仿真与可视化系统中，摄像机视野的控制至关重要。用户通常通过键盘的W、A、S、D键进行前后左右移动，使用Q和E键实现上下移动；同时，通过鼠标右键进行视角的旋转，并利用鼠标滚轮来调整视野的缩放。这篇文章将详细介绍如何在UE5.3中利用蓝图实现这些摄像机控制功能，帮助开发者创建更加沉浸式的虚拟环境体验。
# 准备工作

## 绑定轴映射

在菜单栏找到编辑--项目设置--引擎--输入--找到轴映射，进行下图设置：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240929152028.png)
其中，MoveForward表示鼠标WS控制相机前后移动，MoveRight控制左右移动；MoveUp控制上下移动；Turn和LookUp分别控制相机视野的左右和上下旋转；Zoom控制相机视野缩放。

## 创建相机控制蓝图

创建一个继承于Pawn的蓝图类，命名为BP_CamController
打开蓝图添加组件：分别添加SpringArm、FloatingPawnMovement、Camera(作为SpringArm子组件)这三个组件，如下图：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240929153136.png)

# 蓝图节点连连看

## 实现相机前后左右移动

在事件图表中，右键输入MoveFroward和MoveRight添加WASD输入事件，并根据下图连接相关节点即可。

![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240929154323.png)


## 实现相机上下左右旋转

在事件图表中，右键输入Turn和LookUp添加鼠标X和Y事件，并根据下图连接相关节点即可。

![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240929154832.png)

## 实现相机上下移动

在事件图表中，右键输入MoveUp添加QE输入事件，并根据下图连接相关节点即可。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240929154935.png)

## 实现相机视野缩放

在事件图表中，右键输入Zoom添加鼠标滚轮输入事件，并根据下图连接相关节点即可。

![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240929155028.png)
（SpringArm为弹簧臂组件的引用）

# 将相机蓝图放置于场景中

在内容菜单里找到BP_CamController拖放置场景中合适的位置，并在细节面板中找到Pawn栏将Use **Controller Rotation Pitch和Use Controller Rotation Yaw**勾选，将**Auto Possess Player**设置为Player 0。

![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240929160020.png)

如果需要相机更加平滑移动，可以选中SpringArm组件设置其滞后栏中的Enable Camera Lag和Enable Camera Rotation Lag为勾选状态，也可以设置相应的平滑速度
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240929160354.png)

运行即可使用鼠标键盘控制相机的视野了，其他可以根据需求进行微调。