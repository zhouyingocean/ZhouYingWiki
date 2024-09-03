***
@[TOC](目录)

## unity之搭建VR开发环境

***
***选用unity2018.3.6f1+steamVR1.2.3+VRTK3.3 ，兼容性比较好。***

亲测：进行正式开发之前，最好安装一下虚拟现实 环境驱动和选好对应的插件版本，能避免不少坑和报错。
### ***HTC VIVE环境配置***
虚拟现实应用需要配置虚拟现实硬件的驱动，本作品的硬件设备为HTC VIVE，故需在此网址下载驱动程序并根据提示安装并配置硬件：https://www.vive.com/cn/setup/vive/。
###  ***Steam VR环境配置***
 Steam VR环境为大多数VR软件的通用环境，本作品也需Steam VR的支持。此网址可浏览Steam VR的相关介绍信息并下载Steam: https://store.steampowered.com/steamvr/。
 点击网页右上方的安装Steam绿色按钮，下载Steam安装程序并进行安装，安装完成Steam后需手动安装Steam VR。
###  ***创建功能导入插件检查环境***
 找到兼容性比较好的插件，我这里用的是steamVR1.2.3+VRTK3.3,文章后面我上传这两个插件，导入Assets，弹出的SteamVR窗口，点击Accept All按钮设置Steam VR环境即可，无其他报错证明可用：
 ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/3dbf846d816afbd347ebc75ad6a2f05f.png)

 ### ***创建VR交互环境***
 该作品使用VRTK配合SteamVR快速配置VR环境。在Plugins文件夹中打开VRTK->Prefabs文件夹，找到SDKSetupSwitcher预制体，拖入Hierarchy窗口中：
 ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/e5f3678b696270931fca9a46a040ec02.png)

在Hierarchy中新建一个空物体Create Empty，将其命名为VRTK_SDKManager，并置零其位置和旋转参数。将SDKSetupSwitcher拖曳至该空物体下，使SDKSetupSwitcher成为其子物体。用同样的方法，新建一个VRTK_Scripts空物体，并创建LeftController与RightController空物体作为其子物体，同样置零位置和旋转参数：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/d1ad6fd9285261b119c978de1299a251.png)
接下来需为两个空物体上添加VRTK_Controller Events组件实现VRTK监听手柄事件。这里的LeftController和RightController实际上代表着虚拟环境中的左、右手。因此相关的脚本和手柄上的物体（比如UI）则可放在这两个空物体上。
接下来我们将VRTK预制好的组件加在空物体上。选择VRTK_SDKManager，在右侧Inspector面板中点击Add Component按钮，在弹出的菜单中搜索VRTK_SDK Manager，点击添加此组件：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a3f0024051a66931e46153d6bb8c135f.png)
VRTK支持多种VR设备的SDK，在本作品中只安装SteamVR的SDK，故需根据SteamVR创建一个SDKSetup（SDK配置），按照VRTK的标准进行引用，VRTK就能统一获取对应配置的输入、输出。
在VRTK_SDKManager下新建一个空物体，命名为SteamVR，将其Position的Y轴改为0.5。为空物体添加组件VRTK_SDKSetup，在组件的Quick Select一栏选择SteamVR选项：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/5d0b76c96b2f09c23718a0805fd50ff5.png)
在Project窗口，进入Plugins/SteamVR/Prefabs目录，将Camera与SteamVR预制体拖曳至刚创建的SteamVR空物体下。此时查看SteamVR的属性面板，红色提示消失:
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/d69708d2be2b261f8ff0d53ef726c4b0.png)
至此，创建SDK配置完成。VRTK可提供一个VR环境的模拟器，可从Plugins/VRTK/Prefabs目录下查看。新建一个名称为Simulator的SDK配置，将目录下VRSimulatorCameraRig预制体拖曳至该空物体下作为其子物体，将SDK Setup设置为Simulator。
接下来，配置SDKManager，并将其启用。选择VRTK_SDKManager，在VRTK_SDK Manager组件的Setups选项中，点击Auto Populate按钮即可启用SDKManager配置并自动排序。同时，需将VRTK_Scripts下的左右手物体分别拖曳至Script Aliases项对应位置。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/8c303d910f1b08c1a0ef087ce3bdfc87.png)
最后，在Project窗口下新建一个名为Prefabs的文件夹，将SDKManager和左右手物体分别拖曳至该文件夹中，生成预制体，以便后续使用。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/5ddbdefb6ecd200e215957d0ecc828c1.png)
### ***测试VR环境***
对创建好的VR交互环境进行测试，如若开发环境未连接VR设备，会自动选择VRTK的模拟器进入测试。我们可根据左上角UI提示在模拟器中进行移动、旋转、更改手柄位置等操作，运行时可点击右上角Switch SDK Setup按钮进行更改VR环境。Console窗口若无其他报错，则运行成功。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/1257570fb941662f30b4a115d646f098.png)
图中报错可忽略，主要是没连接VR设备，连接上自然就没有了，运行时使用的是VRTK自带的模拟器Simulator，方便后期交互测试。

steamVR1.2.3+VRTK3.3下载:
https://download.csdn.net/download/qq_42437783/16608509[点此链接下载相关插件](https://download.csdn.net/download/qq_42437783/16608509)
