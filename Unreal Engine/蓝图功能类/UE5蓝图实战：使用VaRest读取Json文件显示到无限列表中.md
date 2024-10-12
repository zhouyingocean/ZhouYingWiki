
VaRest是一款开源的UE插件，它允许我们使用蓝图来进行Json文件的读写操作，本次蓝图实战将演示如何使用VaRestd读取Json数据显示到无限列表中。

# 安装并启用VaRest插件

首先需要在**虚幻商城** 搜索**VaRest**关键字，找到该插件点击“免费按钮”，然后切换到**库**，在保管库下降VaRest安装到所需要的项目引擎中即可。

最后需要再引擎中开启该插件的使用，依次在菜单栏点击**编辑--插件--搜索并勾选VaRest--重启引擎**。

![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20241011103017.png)


# 创建Json文件和搭建无限列表

1. 使用Json在线编辑器模拟Json数据

在项目Content目录下新建Data文件夹，新建文本文件命名为Info.json。将在线Json编辑器模拟的数据复制粘贴到Info.json中。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20241011111555.png)

2. 搭建无限列表UI
我们需要做一个UI来显示Json数据。

首先做一个无限列表显示显示Item：命名为WBP_StudentPanel，添加一个ListView控件，在其列表记录栏下点击+号新建一个EntryWidgetClass蓝图类，用于显示单个学生信息的预制体UI，命名为WBP_StudentItem。如下图：

![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20241011155344.png)
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20241011152705.png)

# 蓝图节点连连看

##  定义数据结构

这里还需要定义两个基本数据结构用于数据的解析和显示。新建一个结构体蓝图，命名为S_StudentInfo，定义与之前Json数据匹配的四个变量：name、number、height、weight用于解析Json数据后构造的数结构体；新建一个继承于Object类的蓝图类，命名为O_StudentInfo。定义一个变量，类型为刚才定义的结构体：S_StudentInfo用于将数结构体据显示的列表UI上。如下图两个基本蓝图类：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20241012094150.png)

## 完善测试蓝图逻辑

### 初始显示无限列表UI

在一个相机控制的蓝图类中，开始BeginPlay节点连接Create Widget节点，Class引脚选择WBP_StudentPanel，执行引脚连接到Add to Viewport。如下图：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20241012095721.png)

### 点击数字0键解析Json并显示到列表中

这里将用到VaRest插件提供的API，所以在此之前确保VaRest插件已启用。

1.  解析Json的蓝图逻辑

首先使用Load Json from File函数解析相对于Content目录下的json文件，所以Path引脚处填入Data/Info.json。然后在Get Array Field方法解析data节点下的数据，构造一个Student Data的Json数据，如下图：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20241012100826.png)

然后for循环遍历这个Json数组，没每个元素单独解析，这里使用Get String Field方法对name、number、height、weight单独解析然后再构造S_StudentInfo添加到StudentInfoList数组中，最后定义一个事件分发器ParseStudentInfoCompleted，在解析完成后调用将StudentInfoList传递出去。如下图：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20241012101410.png)

2. 绑定事件分发器ParseStudentInfoCompleted

在WBP_StudentPanel中，从Event Construct牵出引线获取相机控制器的引用，绑定事件分发器，再用Create Event节点创建一个事件触发函数ParseStudentInfoCompletedCallBack。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20241012102427.png)

完善函数ParseStudentInfoCompletedCallBack：

定义一个变量StudentInfos，类型为O_StudentInfo。对于传递过来的结构体数组进行遍历，单个元素构造O_StudentInfo。使用Add item节点添加到StudentListView（这里是一个无限列表ListView控件），完成之后设置ListView的item，用到SetListItems（这里很重要，会触发后续的更新接口事件）：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20241012103113.png)

3.  将数据显示到单个列表元素中

这里关键的一步是在WBP_StudentItem蓝图的**类设置**中实现一个接口：**User Object List Entry**

然后实现On List Item Object Set 事件就好了，对与传过来的Object对象转换为O_StudentInfo再获取结构体S_StudentInfo的引用，最后依次对Text组件赋值即可。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20241012103923.png)

# 运行测试结果

点击Play运行，按下键盘数字键0，无限列表成功显示Json数据：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20241012104310.png)

这个ListView对于海量数据来说真是挺有用的