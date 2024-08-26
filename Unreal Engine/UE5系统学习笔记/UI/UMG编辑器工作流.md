
# 创建UI控件

1.在内容菜单（Content Browser）面板，点击添加（Add）或者右键空白处，依次选择用户界面（User Interface）/ 控件蓝图（Widget Blueprint）。
![Pasted image 20240822112655](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240822112655.png)

2.在弹出来的窗口中，点击User Widget即可创建一个UI控件，可以自定义命名（规范一点可以命名为WBP_XXX）。
![Pasted image 20240822113459](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240822113459.png)

# 初识UMG UI 编辑器

双击UI控件蓝图打开UMG 设计器：
![Pasted image 20240822114021](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240822114021.png)
UMG主要由七个部分组成：
![Pasted image 20240822115221](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240822115221.png)

| 选项卡                  | 用途                                   |
| -------------------- | ------------------------------------ |
| 1.设计器（Designer）      | 设计UI布局的画布，用于搭建并显示UI，可以摆放UI在屏幕中的位置    |
| 2.调色板（Palette）       | 可供使用的控件列表，引擎自带的或用户自定义的控件模版           |
| 3.细节面板（Details）      | 控件的属性，包括旋转变换属性等                      |
| 4.层级面板（Hierarchy）    | 当前创建的所有控件列表都显示在这里，UI之间的层级关系          |
| 5.动画面板（Animations）   | 为UI创建的动画都在这里显示                       |
| 6.时间轴（Timeline）      | 控件动画的属性和关键帧，可以制作帧动画                  |
| 7.编辑器模式（Editor Mode） | 有设计器和图表两种编辑模式切换，图表模式与蓝图编辑器具有几乎相同的功能。 |
	tip: 画布上的操作，通过按住右键并移动鼠标即可上下左右平移画布，通过鼠标滚轮滑动可进行缩放画布。

# 搭建UI界面

在进行UI 设计之前，你应该先往画布中放置一个Canvas Panel作为根物体。
可以在调色板里面搜索Canvas Panel或者在展开面板下找到：鼠标左键按住并拖拽到画布区域或层级面板中松开即可。
![Pasted image 20240822141729](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240822141729.png)

之后你就可以在画布中放置你所需的其他控件了，比如文本、按钮等等。
![Pasted image 20240822143147](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240822143147.png)
你还可以重命名控件、拖动控件、调整大小，也可以通过细节面板修改相关信息。

在设计好UI 界面之后，记得点击编辑器左上角的编译并保存。
# 显示UI界面

当你很高兴的运行游戏时却发现看不见你刚才设计的UI，这是因为要将UI显示到Game视口中，还要做一点额外的蓝图操作。

1.在关卡编辑器主工具栏处依次点击**蓝图/打开关卡蓝图**。
![Pasted image 20240822151538](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240822151538.png)

2.右键空白处搜索并添加**Event BeginPlay**节点
![Pasted image 20240822151910](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240822151910.png)
3.将鼠标放置到Event BeginPlay节点的执行引脚上，按住左键并拖拽到其余空白处松开并搜索**Create Widget**节点，点击Class参数下拉列表，搜索我们要创建的UI实例“WBP_HUD”。
![Pasted image 20240822152638](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240822152638.png)

4.同样的操作将Create Widget节点的执行引脚连接到**Add to Viewport**节点，并将其返回值Return Value连接到Target。
![Pasted image 20240822153013](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240822153013.png)
5.点击左上角编译并保存，关闭该窗口，点击主编辑界面的运行按钮，这时就能在游戏视口上看到制作的UI界面了。
![Pasted image 20240822153431](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240822153431.png)
# 更新UI界面

