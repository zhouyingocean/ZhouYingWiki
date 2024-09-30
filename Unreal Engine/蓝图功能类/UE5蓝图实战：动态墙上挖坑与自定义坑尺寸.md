
在Unreal Engine 5.3中，我利用蓝图系统开发了一个创新的挖坑Demo，该Demo展示了如何在实时环境中动态地在墙体上挖坑，并允许用户自定义坑的大小。这一过程得益于UE5官方提供的Geometry Script插件，该插件通过蓝图接口实现了强大的网格布尔算法功能。文章中，我将详细介绍如何在运行时动态地进行挖坑操作。此外，我还将展示如何通过蓝图接口调整坑的尺寸，为游戏世界中的互动元素添加更多可能性。无论是对于建筑模拟、地形编辑还是其他需要动态网格修改的应用场景，本文提供的方法都将大有裨益。

# 准备工作

## 启用插件Geometry Script

在UE5.0之后的版本，如UE5.3中，在编辑栏--插件--搜索栏输入**Geometry Script** 打钩启用并重启UE。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240930113148.png)

## 导入RuntimeGizmo插件

这是一款可以在运行时控制对象移动旋转缩放的工具
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240930114051.png)
可以从UE商店里购买，或者在网上找一些免费资源。将插件解压后的父级目录复制到UE项目工程中的Content文件夹下。

## 制作挖坑蓝图类Actor

在此之前确保Geometry Script插件启用成功。在内容菜单里右键创建蓝图类，在弹出的选取父类窗口中间的搜索栏搜索并选择**DynamicMeshActor**，命名为BP_DigHole
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240930114740.png)

# 蓝图节点连连看

## 实现挖坑函数


1. 定义变量和函数

双击打开BP_DigHole蓝图，在我的蓝图--函数栏点击+号添加一个函数，命名为GenerateHole，在变量栏分别添加Dimension（Vector），Size（Vector），DynamicMesh（DynamicMesh），DragSphere（Actor）这个四个变量。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240930152012.png)

2.  完善函数

按照下图连接蓝图节点：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240930152425.png)
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240930152943.png)

## 接入Gizmo工具

1.  在Gizmo蓝图里添加事件分发器

在此之前确保RuntimeGizmo插件导入成功。
双击打开BP_Gizmo蓝图，添加一个事件分发器命名为OnGizmoChanged，并找到**Process Interaction**函数，在其执行修改坐标轴位置之后的逻辑下连接以下节点：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240930154826.png)

2.  在控制器中启用Gizmo
在任意一个在场景中激活的Pawn类（如BP_CamController）中，按下图蓝图连接节点：

![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240930155612.png)

在这个蓝图中，显示定义了一个BP_Gizmo的变量GizmoRef，使用Event BeginPlay节点绑定BP_Gizmo的事件分发器OnGizmoChanged用于触发挖坑函数GenerateHole，后面是将鼠标光标显示到Game视图中。

Left Mouse Button是一个鼠标左键点击事件，用于触发Attach Gizmo函数以激活场景中的Gizmo小组件，在鼠标左键点击Actor对象时显示。

# 场景Actor参数设置

放置一个球体到场景中，命名为DragSphere，在内容菜单中找到BP_DigHole和BP_Gizmo，将它们拖拽至场景中，其中需要给BP_DigHole的变量Dimension、Size、DragSphere赋值如下：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240930163154.png)

# 运行效果

![hole.gif](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/hole.gif)

需要修改墙体网格大小可以添加函数修改Dimension变量，修改坑的大小可以修改Size变量，置于坑的深度可以通过设置坑在父级网格体下的Z坐标实现。