
# Actor通信介绍

Actor类似于Unity中的空物体GameObject，一种可以随意放置到场景中的游戏对象。UE提供了多种供不同Actor之间通信的方法，本文将通过搭建Demo来演示以下表格中四种通信方法的要求和常见用法。

Actor通信方法表：

| 通信方法  | 使用场景                      | 前提条件                          | 示例                    |
| ----- | ------------------------- | ----------------------------- | --------------------- |
| 直接通信  | 需要调用关卡中某一Actor的方法         | 需要引用关卡中的Actor                 | 在关卡中的特定Actor上触发事件。    |
| 类型转换  | 希望验证Actor是否属于特定类，以便访问其属性。 | 需要引用关卡中的Actor以类型转换到所需的Actor类。 | 访问属于同一父类的子Actor的特定功能。 |
| 事件分发器 | 通过一个Actor来触发到多个Actor的事件。  | 其他Actor需要订阅事件，以便对事件作出响应。      | 通知不同类型的Actor：某事件已经触发。 |
| 接口    | 当你需要为不同Actor添加相同功能时。      | 需要引用关卡中的Actor，并且该Actor需要实现接口。 | 为不同类型的Actor添加交互行为。    |

# 通信方法演示

## 准备工作

打开虚幻引擎--创建新项目--选择游戏--第三人称游戏--勾选初学者内容包。

![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240909134728.png)
本Demo使用最新虚幻引擎版本5.4构建。
## 直接通信

本示例将实现由第三人称角色Actor蓝图控制Cube的显隐来演示直接通信方法的使用。

1. **制作BP_Cube蓝图**
打开内容侧滑菜单--在内容菜单下新建MyBlueprints目录--右键菜单选择蓝图类--选择通用下的Actor类--命令为BP_Cube。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240909161029.png)
2. 添加静态材质
双击打开BP_Cube--在左边组件窗口点击添加--搜索并选择立方体（Cube）。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240909162525.png)

3. 编写BP_Cube蓝图
在左边我们蓝图下找到函数列表--点击+号添加一个函数--命名为OnCubeVisible--按住键盘Ctrl键+鼠标拖拽变量Cube到蓝图中--从Cube引脚拖出一根线松开--搜索并选择**Set Visibility**函数。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240909163520.png)

4. 给函数添加形参
选中函数OnCubeVisible--在右边细节面板输入栏点击+号--添加布尔变量IsVisible--将函数参数Is Visible引脚连接到Set Visibility的new Visibility处--点击编译保存蓝图。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240909165416.png)
5. 给第三人称蓝图BP_ThirdPersonCharacter添加按键事件
在内容菜单搜索BP_ThirdPersonCharacter并双击打开--在蓝图空白处右键搜索数字按键0事件（**Keyboard Events**节点）。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240909171627.png)
从**Pressed**引脚拖出一根线松开搜索**Get Actor Of Class**节点--在引脚**Actor Class**点击下拉框搜索并选择BP_Cube--连接**Flip Flop**节点--从return value引脚处拖出显连接On Cube Visible函数。具体连接图如下：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240909172243.png)
6. 将Actor物体BP_Cube从内容菜单拖放至场景中，并运行测试。不断按下数字键盘0键即可
![cube.gif](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/cube.gif)

## 类型转换通信

本示例将实现由第三人称角色Actor蓝图控制Cube的旋转来演示类型转换通信方法的使用。
继续使用PracticeProject项目完成这部分工作。
1. 在BP_Cube蓝图编写旋转逻辑
双击打开BP_Cube蓝图--在变量栏添加IsRotate变量--在事件图标找到**Event Tick**节点--将其执行引脚拖出连接至**Branch**分支节点--将True引脚连接到**Add Actor Local Rotation**节点--将Delta Rotation引脚的Z随意输入一个值--将变量IsRotate拖出连接至Branch的Condition节点。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240909175522.png)
最后将IsRotate设置为公开变量（提供其他蓝图设置）。
2. 编写BP_ThirdPersonCharacter蓝图添加碰撞函数
在组件Capsule Component处右键选择添加事件--将**On Component Begin Overlay和On Component End Overlap**函数添加到事件图表中。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240909180105.png)
3. 编写类型转换调用逻辑
在Begin节点中，从**Other Actor**引脚拖出连接到**Cast To BP_Cube**节点--从As BP Cube节点连接到**Set Is Rotate**节点--将引脚Is Rotate勾选。
同理操作设置End节点，只不过需要将最后的Is Rotate引擎取消勾选。如下图
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240909180827.png)
4.  设置角色Pawn的碰撞预设
要使角色发生重叠碰撞，还需要将组件的碰撞预设设置栏勾选WorldDynamic。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240909181721.png)

5. 运行测试，靠近Cube时旋转 ，远离时停止旋转。
![rotate.gif](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/rotate.gif)

## 事件分发器通信

类似于Unity中的委托事件，全局或局部公开的一个事件分发器，由需要的脚步自由订阅，只要订阅了该事件分发器，当事件触发时，这些订阅者就能收到消息，处理各自的逻辑。

1. 编写一个持有事件分发器的Actor
在内容菜单新建一个Actor类型的蓝图类--命令为BP_EeventActor--添加一个Box组件--并在我的蓝图中事件分发器一栏添加+号--添加事件分发器并命名为OnBoxEvent--在事件图表中添加On Component Begin Overlay事件--将事件分发器拖拽到图表中选择**调用**，连接图如下：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240910141040.png)
编译保存，并将其放进场景中任意位置
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240910141150.png)
2. 创建第一个事件接收器Actor--BP_CircularReceive
编写蓝图逻辑，将四个QuarterCylinder隐藏。
添加一个变量命名为EventActor在细节面板设置变量类型为BP_EevntActor,并设置为公开变量--添加一个变量命名为CylinderList，在细节面板设置变量类型为Static Mesh Actor（数组类型），并设置为公开。--在EvenActor变量细节面板事件栏下添加On Box Event右边的+号，开始编写逻辑：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240910143943.png)
将BP_CircularReceive拖放到场景中，在细节面板分别赋值变量的引用：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240910144115.png)
3. 编写第二个事件接收器Actor--BP_ExplosionActor
在内容菜单里搜索**Blueprint_Effect_Explosion**，将其复制到自己定义的文件夹中并命名为BP_ExplosionActor--将其拖到场景中圆柱的位置，稍微调整一下位置让在圆柱中间。同上一步一样添加变量Eventor，将其事件完善，这里是启用爆炸效果。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240910145648.png)
还需要将两个子组件P_Explosion和ExplosionAudio的激活属性Auto Activate取消勾选。最后将其放置场景中并设置变量引用：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240910145855.png)
4. 测试事件分发器效果
![event.gif](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/event.gif)

## 接口通信

UE5中，Actor 接口通信是一种非常有效的设计模式，接口负责定义一系列共有的行为或功能，这些行为或功能在不同Actor中可以有不同的实现方法。当你为不同Actor实现了相同类型的功能时，适合使用此通信方法。

本例中，将实现一个简单的交互系统，通过在两个不同Actor间通信，学习接口的用法。

1. 创建接口
右键目录空白处创建蓝图接口类
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240910151858.png)
双击打开添加函数命名为Interaction
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240910151952.png)
2. 创建可交互开关的灯
在内容菜单搜索**Blueprint_CeilingLight**将其复制到自定义的目录，并重命名为BP_Light--将其放置到场景中。
双击打开蓝图点击类设置添加接口BPI_Interaction，编译保存后再我的蓝图接口栏下右击Interaction接口选择实现事件可以看到Event Interaction节点自动添加到蓝图中。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240910153245.png)
编写交替开关灯的逻辑：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240910153858.png)
3. 创建可交互的球体
新建一个Actor蓝图类命名为BP_Sphere，添加一个球体组件，同第2步一样添加接口Interaction并实现切换材质的逻辑：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240910160402.png)
4. 修改玩家蓝图并测试接口事件
找到蓝图BP_ThirdPersonCharacter，在其OnComponent Begin Overlap事件中添加执行节点Interaction(Message)。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240910160642.png)
编译保存并运行：
![interface.gif](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/interface.gif)
# 总结

1. **直接通信**：
    
    - 适用于简单的场景，当你需要直接与特定的 Actor 交互时非常有效。需要确保你有正确的引用。
2. **类型转换**：
    
    - 当你需要访问特定类的功能或属性时，类型转换是一个很好的选择。它允许你在运行时验证和访问 Actor 的特定功能。
3. **事件分发器**：
    
    - 适合需要广播事件的场景，能够让多个 Actor 响应同一事件，增强了系统的灵活性和扩展性。
4. **接口**：
    
    - 提供了一种灵活的方式为不同类型的 Actor 添加共同的功能。通过接口实现，可以减少代码重复，提高可维护性。

通过这四种通信方法，开发者可以在 Unreal Engine 中高效地管理 Actor 之间的交互，构建复杂的游戏逻辑。选择合适的通信方式能够提升代码的可读性和可维护性，使得项目更加模块化。