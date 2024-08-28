UMG调色板提供了很多内置的Widget控件，但是常用控件也就四种：面板（Panel）控件、输入（Input）控件、通用（Common）控件、用户创建（User Created）控件。
![Pasted image 20240823144021](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823144021.png)
# 面板控件
Panel一般用作一个父级容器，实现子元素间的对齐或分布操作。
![Pasted image 20240823144242](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823144242.png)
1.  **Canvas Panel -- 画布面板**
提供了最大的灵活性，允许你通过绝对坐标或相对于父控件的坐标来放置子控件。这使得你可以自由地设计复杂的布局。可以随意放置子控件，类似于在画布上随意绘画。
![Pasted image 20240823151701](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823151701.png)

Canvas Panel下的组件可以调整Anchors、Offsets、Alignment这些常用属性

| 常用属性           | 说明               |
| -------------- | ---------------- |
| Anchors（锚点）    | 定义组件在画布上的固定位置    |
| Offsets （偏移量）  | 控制组件与锚点之间的距离     |
| Alignment （对齐） | 允许根据控件的内容设置其对齐方式 |

2.  **Grid Panel -- 网格面板**
将子组件按行和列排列，像Excel表格一样。
![Pasted image 20240823165848](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823165848.png)
上图为一个3x3的网格，类似一个Excel表格，通过设置行列的填充Fill比例来划分网格区域。

![Pasted image 20240823170410](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823170410.png)

上图为Grid Panel的一个子控件在网格中的占比（位于第2行第1列，占用3列）。

| 常用属性                 | 说明              |
| -------------------- | --------------- |
| Column Fill/Row Fill | 定义网格的列数/行数      |
| Row/Column           | 指定子组件在网格中的行和列位置 |
| Row/Column Span      | 允许子组件跨越多个行或列    |

3.  Horizontal Box -- 水平框
将子组件水平按从左到右的顺序排列，适用于需要横向布局的场景
![Pasted image 20240823171240](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823171240.png)

子控件有两种均匀分布模式，自动模式可以自动设置宽度，填充模式下，由设置的Size占用剩余宽度。（如下图中，HorizontalBox宽度为300，红色控件自动布局使用自身宽度100，剩余200宽度由白色【占用1/3】和紫色控件【占用2/3】按Size填充）
![Pasted image 20240823171837](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823171837.png)
![Pasted image 20240823171859](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823171859.png)
![Pasted image 20240823171913](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823171913.png)

| 常用属性      | 说明              |
| --------- | --------------- |
| Padding   | 控制子控件直接的间隔      |
| Alignment | 控制子控件在父容器下的对齐方式 |

4.  **Overlay**-- 覆盖容器
允许多个组件重叠放置。
于Unity 的UGUI（几乎每个UI组件都可以嵌套子组件），UE里面只有部分控件支持嵌套子控件，而且还是只能嵌套一个（像Button），如果需要嵌套组件，就需要使用Overlay。
![Pasted image 20240823181139](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/Pasted%20image%2020240823181139.png)

| 常用属性    | 说明                     |
| ------- | ---------------------- |
| Z-Order | 控制组件的层级顺序，数字越大越优先显示在上面 |

5.  Safe Zone -- 安全区域面板
在非PC平台上经常会用到的一个容器，确保UI元素在不同屏幕上都能正确显示，避免被屏幕边缘遮挡。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240826171346.png)

| 常用属性    | 说明        |
| ------- | --------- |
| Padding | 设置安全区域的大小 |

6.  Scale Box -- 缩放框
它允许你指定如何将其子控件进行缩放。你可以设置缩放因子，这样无论子控件的原始大小是多少，它都可以根据Scale Box的设置进行放大或缩小。这对于需要适应不同屏幕尺寸或分辨率的UI元素非常有用。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240826175413.png)

| 常用属性                 | 说明            |
| -------------------- | ------------- |
| Stretch              | 控制子组件的拉伸方式    |
| User Specified Scale | 手动设置缩放比例      |
| Min/Max Desired Size | 设置子组件的最小和最大尺寸 |


7.  Scroll Box -- 滚动框
允许用户滚动查看超出可见范围的内容，适合长列表或内容。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240826183503.png)

跟Unity的Scroll View 差不多，就是做表格组件有点麻烦。

| 常用属性                  | 说明        |
| --------------------- | --------- |
| Scroll Bar Visibility | 控制滚动条是否显示 |
| Orientation           | 可设置滚动的方向  |

8.  Size Box -- 尺寸容器
可以限制子控件的大小，确保它们不会超出指定尺寸。有两种情况：1,SizeBox在CanvasPanel下时，需勾选Size To Content才能控制子布局，这时自身的尺寸会失效；2，将SizeBox包裹在Overlay下，自身尺寸不会失效，同时也可以控制子布局，跟Unity的Layout  Element有点类似
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240826185508.png)

| 常用属性                       | 说明                                |
| -------------------------- | --------------------------------- |
| Width Override（宽度覆盖）       | 允许你指定子部件的固定宽度。如果设置为0，则宽度根据内容自动调整。 |
| Height Override （高度覆盖）     | 允许你指定子部件的固定高度。如果设置为0，则高度根据内容自动调整。 |
| Min Desired Width （最小期望宽度） | 设置子部件的最小宽度                        |
| Min Desired Height（最小期望高度） | 设置子部件的最小高度                        |
| Max Desired Width（最大期望宽度）  | 设置子部件的最大宽度                        |
| Max Desired Height（最大期望高度） | 设置子部件的最大高度                        |

9.  Stack Box -- 堆栈框
一个堆叠布局面板，子控件按垂直或水平方向堆叠。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240827095954.png)
其实就是水平框和垂直框的结合，只不过说这个堆栈框可以在运行时动态修改布局的朝向。

| 常用属性            | 说明                       |
| --------------- | ------------------------ |
| Orientation（方向） | 选择堆叠的方向                  |
| Padding（填充）     | 设置 Stack Box 边缘到子部件的内边距。 |

10.  Uniform Grid Panel -- 均匀网格面板
这个控件允许你以网格形式排列子控件，其中所有单元格的大小都是统一的。你可以通过调整网格的行数和列数来控制布局。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240827133949.png)

| 常用属性         | 说明                 |
| ------------ | ------------------ |
| Slot Padding | 设置子组件与网格容器边缘之间的内边距 |
| Row/Column   | 子组件所在的行/列号         |

11.  Vertical Box -- 垂直框
用于将子组件按从上到下的顺序垂直排列，适用于需要竖向布局的场景。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240827135530.png)

| 常用属性      | 说明                            |
| --------- | ----------------------------- |
| Padding   | 设置子组件与 Vertical Box 边缘之间的内边距。 |
| Alignment | 设置子组件在 Vertical Box 中的对齐方式。   |

12.  Widget Switcher -- 控件切换容器
用于在多个子部件之间切换显示。它常用于实现选项卡式布局或多种视图之间的切换，比如设置面板或多页面表单。

![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240827140444.png)

| 常用属性                         | 说明                                      |
| ---------------------------- | --------------------------------------- |
| Active Widget Index（活动小部件索引） | 指定当前显示的子组件索引。通过设置这个属性，你可以控制哪个子部件是当前可见的。 |

13.  Wrap Box -- 自动换行容器
该控件会将子控件从左到右排列，当一行放不下时自动换行，它特别适用于需要动态调整排列的 UI 元素，如标签、按钮或图标集合。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240827141526.png)

| 常用属性        | 说明                                                    |
| ----------- | ----------------------------------------------------- |
| Orientation | 选择换行的方向                                               |
| Wrap Size   | 设置 Wrap Box 的最大宽度，当子部件的总宽度超过此值时会自动换行。对于垂直方向，可以设置最大高度。 |

# 输入控件

常用的输入控件用于收集用户输入或显示文本，让玩家与游戏进行交互。UE5 UMG提供了ComboBox(Key)、ComboBox(string)、Editable Text、Editable Text(Multi-Line)、Spin Box、Text Box、Text Box(Multi-Line)共7种基础控件。

1. ComboBox(Key) --（下拉框 - 键）
下拉菜单，用于让用户从预定义的键列表中选择一个键
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240827170025.png)
菜单项需要自定义。可以根据需求搭建组合控件作为下拉菜单的Item。

| 常用属性            | 说明                             |
| --------------- | ------------------------------ |
| Options         | 提供可供选择的按键列表，例如“W”，“A”，“S”，“D”。 |
| Selected Option | 当前用户选择的选项按键                    |

2. ComboBox(String) -- （下拉框 - 字符串）
下拉菜单，用于让用户从字符串列表中选择一个选项。例如，选择一个角色的职业或一个菜单项。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240827170209.png)
继承于ComboBox(Key) ，实现了字符串列表的下拉框，相当于Unity默认的Dropdown组件。

| 常用属性            | 说明                        |
| --------------- | ------------------------- |
| Default Options | 字符串的列表，例如“战士”，“法师”，“弓箭手”。 |
| Selected Option | 当前选中的字符串                  |

3. Editable Text -- 可编辑文本

单行文本输入框，用户可以在其中输入或编辑单行文本，例如用户名或密码。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240827170634.png)
提供高度自定义

| 常用属性             | 说明                      |
| ---------------- | ----------------------- |
| Text（文本）         | 默认显示的文本                 |
| Hint Text（提示文本）  | 输入框为空时显示的提示信息，如“输入用户名”。 |
| Is Read Only（只读） | 设置是否允许编辑                |

4. Editable Text(Multi-Line) -- 可编辑多行文本
多行文本输入框，允许用户输入多行文本，适合较长的描述或评论。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240827171240.png)
提供高度自定义

| 常用属性           | 说明         |
| -------------- | ---------- |
| Text           | 默认显示的多行文本。 |
| Auto Wrap Text | 决定是否允许自动换行 |

5. Spin Box -- 旋转框
一个数字输入框，可直接输入数字或者点击滑动数字，例如设置音量或选择数量。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240827173503.png)

| 常用属性                 | 说明         |
| -------------------- | ---------- |
| Minimum Value（最小值）   | 设置可输入的最小数字 |
| Maximum Value（最大值）   | 设置可输入的最大数字 |
| Minimum Slider Value | 允许滑动的最小值   |
| Maximun Slider Value | 允许滑动的最大值   |

6. Text Box -- 文本框
单行文本显示框，用于显示信息或提供玩家输入文本。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240827171630.png)
继承于Editable Text，实现了背景框显示、

| 常用属性             | 说明         |
| ---------------- | ---------- |
| Text（文本）         | 要显示的默认文本内容 |
| Font Size（字体大小）  | 文本的字体大小    |
| Text Color（文本颜色） | 文本的颜色      |

7. Text Box(Multi-Line) -- （多行文本框）
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240827171916.png)
继承于Editable Text(Multi-Line)，实现了背景框显示和滚动视图

| 常用属性                 | 说明         |
| -------------------- | ---------- |
| Text（文本）             | 要显示的多行文本内容 |
| Wrap Text At（文本换行位置） | 设定文本换行的宽度  |

# 通用控件
UE5提供了（Border、Button、Check Box、Image、Named Slot、Progress Bar、Radial Slider、Rich Text Block、Slider、Text）10种基本的通用控件，用于构建用户界面的基本元素。

1. Border（边框）
用于创建一个有边框的区域，可以包裹其他控件，通常用于视觉分隔
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240828100954.png)
如图包裹一个Editable Text就相当于一个Text Box。

| 常用属性         | 说明                    |
| ------------ | --------------------- |
| Brush（画刷）    | 用于定义边框的外观，包括颜色、材质和样式。 |
| Padding（内边距） | 控制边框和其内容之间的间距         |

2. Botton （按钮）
用户可以点击的控件，用于触发事件或动作，如提交表单、启动功能或导航至其他页面。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240828101506.png)
不同于Unity的Button，这里的按钮需要添加一个文本框作为文本显示，如果需要的时候。

| 常用属性      | 说明         |
| --------- | ---------- |
| Style     | 按钮的外观样式    |
| OnClicked | 点击按钮时触发的事件 |

3. Check Box （复选框）
一种允许用户选择或取消选择的控件，通常用于设置选项。

| 常用属性             | 说明                                |
| ---------------- | --------------------------------- |
| Is Checked（是否选中） | 复选框的当前状态，表示是否被选中                  |
| Check Box Type   | 复选框的显示类型（Check Box和Toggle Botton） |
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240828102633.png)
跟Unity的UGUI差不多，只不过这里没有自带Text，需要再挂载。

4. Image （图像）
用于显示静态图片或纹理的控件，如展示图标、背景图案、游戏角色等各种图像元素。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240828102958.png)
跟Unity的Image一样，只不过UE的iamge可以实现一下更复杂的效果。

| 常用属性    | 说明       |
| ------- | -------- |
| Size    | 设置图像的宽高  |
| Opacity | 控制图像的透明度 |

5. Named Slot（命名插槽）
用于在用户界面布局中定义一个可插入其他控件的区域。这种控件通常用作容器的一部分，允许你动态地将不同的 UI 元素插入到指定的位置。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240828104249.png)
适用于组合UI，定义一个插槽，可以进行动态插入、删除、添加其他控件的一块区域，一般需要配合布局容器类的控件使用，这对于需要重复使用的控件来说十分方便。

| 常用属性            | 说明                      |
| --------------- | ----------------------- |
| Slot Name（插槽名称） | 用于标识和引用这个插槽的名称          |
| Visibility（可见性） | 控制插槽的可见性，可以设置为可见、隐藏或不可见 |

6. Progress Bar（进度条）
用于显示任务完成进度的 UI 控件。它通常用于展示长期操作的进度，比如下载、加载或任务完成情况。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240828110936.png)

| 常用属性             | 说明                            |
| ---------------- | ----------------------------- |
| Percent（百分比）     | 当前进度条的完成百分比，范围从0.0到1.0        |
| Is Marquee（动态效果） | 进度条是否显示动态的“滚动”效果，通常用于表示未知的进度。 |

7. Radial Slider（圆形滑块）
用于通过旋转滑块来调整一个值。它通常呈现为一个圆形的滑块，用户可以通过旋转控制器来改变值，这种控件在需要旋转输入或调整范围值时非常有用。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240828111201.png)
类似于汽车的仪表盘。

| 常用属性       | 说明                                  |
| ---------- | ----------------------------------- |
| Value（值）   | 当前滑块的值，通常是一个范围内的数字（如 `0.0` 到 `1.0`） |
| Value Tags | 定义文本标签所在值的位置                        |

8. Rich Text Block（富文本块）
是一种用于显示格式化文本的 UI 控件。它允许你在同一文本框中使用不同的字体、颜色、样式等，以实现复杂的文本格式化效果。
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240828112712.png)
这里需要设置文本样式集并正确书写格式才能正常显示内容，这里先不做演示，后面实战再操作。

| 常用属性             | 说明                |
| ---------------- | ----------------- |
| Text（文本）         | 富文本块中显示的文本内容。     |
| Text Style（文本样式） | 控制文本的字体、大小、颜色等样式。 |

9. Slider（滑块）
用于允许用户通过拖动滑块来调整一个值。滑块通常用于调整范围内的参数，例如音量、亮度或其他可调节设置
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240828112947.png)

| 常用属性                | 说明              |
| ------------------- | --------------- |
| Orientation（方向）     | 滑块的方向，可以是水平或垂直。 |
| Bar Thickness（滑块厚度） | 滑块条的厚度          |

10. Text（文本）
用于在用户界面中显示静态文本。它是最基本的 UI 控件之一，适用于展示各种信息，如标签、说明、提示等
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240828113432.png)

| 常用属性              | 说明               |
| ----------------- | ---------------- |
| Text Shadow（文本阴影） | 为文本添加阴影效果，以增强可读性 |
| Font（字体）          | 控制文本的字体类型、大小和样式。 |

# 用户创建控件

就是开发者自己创建的UI控件都会在这里显示，类似于Unity里面的UI预制体，可重复使用。用户可以创建自定义控件来扩展和定制 UI 元素。这些控件可以是简单的 UI 组件，或者是复杂的自定义控件，用于满足特定的需求。

![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240828114144.png)

比如UE的Button不提供文本的显示，那不可能每次做一个Button都要去拖一个文本框显示，这时候就需要提前做好一个可复用的Button按钮，这样子无论是在制作其他控件时还是在运行时动态创建时，只要一需要就能获取并使用。

# 总结

目前来说，只是初步使用了一下UMG的常用控件，可能是习惯了Unity开发UI的流程，感觉UE搭建UI的流程不太好用，有点麻烦的样子。特别是摆放操作上比较不习惯，限制的东西有点多。应该是没有Unity的UGUI易于上手。不过UE的UMG 控件与蓝图集成之后，在复用性和自定义程度上应该是优于UGUI的，可能是目前两大引擎的定位和市场需求不太一样的原因吧。下一步进入项目实战上看看使用UE制作UI的工作流如何，说不定深入使用就会有不一样的感觉了。Let' Go。