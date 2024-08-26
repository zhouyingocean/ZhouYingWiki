UMG调色板提供了很多内置的Widget控件，但是常用控件也就四种：面板（Panel）控件、输入（Input）控件、通用（Common）控件、用户创建（User Created）控件。
![Pasted image 20240823144021](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823144021.png)
# 面板控件
Panel一般用作一个父级容器，实现子元素间的对齐或分布操作。
![Pasted image 20240823144242](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823144242.png)
-  **Canvas Panel -- 画布面板**
画布面板允许在任意位置布局、固定控件，并将这些控件与画布的其它子项按Z轴顺序排序。画布面板是非常适用于手动布局的控件。一般作为根UI控件。
![Pasted image 20240823151701](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823151701.png)
-  **Grid Panel -- 网格面板**
这是一种在所有子控件之间平均分割可用空间的面板。
![Pasted image 20240823165848](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823165848.png)
上图为一个3x3的网格，类似一个Excel表格，通过设置行列的填充Fill比例来划分网格区域。

![Pasted image 20240823170410](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823170410.png)

上图为Grid Panel的一个子控件在网格中的占比（位于第2行第1列，占用3列）。

-  Horizontal Box -- 水平框
用于将子控件水平排布成一行，子控件的高度最高为Horizontal Box的尺寸Y。
![Pasted image 20240823171240](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823171240.png)

子控件有两种均匀分布模式，自动模式可以自动设置宽度，填充模式下，由设置的Size占用剩余宽度。（如下图中，HorizontalBox宽度为300，红色控件自动布局使用自身宽度100，剩余200宽度由白色【占用1/3】和紫色控件【占用2/3】按Size填充）
![Pasted image 20240823171837](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823171837.png)
![Pasted image 20240823171859](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823171859.png)
![Pasted image 20240823171913](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823171913.png)
-  **Overlay**-- 覆盖容器
允许控件互相堆叠，并针对每一层的内容使用简单的流布局。
不同于Unity 的UGUI（几乎每个UI组件都可以嵌套子组件），UE里面只有部分控件支持嵌套子控件，而且还是只能嵌套一个（像Button），如果需要嵌套组件，就需要使用Overlay。
![Pasted image 20240823181139](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823181139.png)
-  Safe Zone -- 安全区
拉取平台安全区信息并添加填充。
在非PC平台上经常会用到的一个容器，使用Safe Zone能保证其子控件不会被硬件遮挡。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240826171346.png)

-  Scale Box -- 缩放框
用于以所需的大小放置内容，并对其进行缩放以满足该框所分配到的区域的大小限制。如果您需要对背景图像进行缩放以填充某个区域，但又不希望因为高宽比的不同而产生失真，或者如果您需要将某些文本自动调整放入某个区域，那么该控件可满足您的需求。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240826175413.png)
主要是使其子控件在拉伸时保持宽高比，或者在不同宽高比下不会弯曲
-  Scroll Box -- 滚动框
一组可任意滚动的控件。当需要在一张列表中显示 10-100 个控件时非常有用。该控件不支持虚拟化。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240826183503.png)

跟Unity的Scroll View 差不多，就是做表格组件有点麻烦。
-  Size Box -- 尺寸容器
可以限制子控件的大小，有两种情况：1,SizeBox在CanvasPanel下时，需勾选Size To Content才能控制子布局，这时自身的尺寸会失效；2，将SizeBox包裹在Overlay下，自身尺寸不会失效，同时也可以控制子布局，跟Unity的Layout  Element有点类似
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240826185508.png)

-  Stack Box -- 堆栈框

-  Uniform Grid Panel -- 均匀网格面板
一种在所有子对象之间平均分割可用空间的面板。
-  Vertical Box -- 垂直框
垂直框控件是一种布局面板，用于自动垂直排布子控件。当需要将控件从上到下依次叠放并使控件保持垂直对齐时，这很有用。
-  Widget Switcher -- 控件切换容器
控件切换器类似于选项卡控件，但没有选项卡，您可以自行创建并组合以获得类似于选项卡的效果。一次最多只显示一个控件。
-  Wrap Box -- 自动换行容器
该控件会将子控件从左到右排列，超出其宽度时会将其余子控件放到下一行。

# 输入控件

# 通用控件

# 用户创建控件