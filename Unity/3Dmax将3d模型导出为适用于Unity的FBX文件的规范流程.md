*unity毕设开发之将3d模型导出为适用于unity的FBX文件*
@[TOC](3dmax导出FBX格式)

# 准备工作
工具：3dmax2014 + unity2018.3.6
# 导出步骤
1.在3dmax中按键盘组合键“Ctrl+A”选中需要导出的模型，依次点击 菜单——导出——导出。

2.选择保存路径、命名和格式（FBX）
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/84df6aad1361eecea1eb78dd8ccf5d94.png)
3.点击保存，设置文件参数，在弹出的窗口中展开【摄像机】【灯光】【嵌入的媒体】【高级选项——轴转化】栏目，取消【摄像机】和【灯光】选项的勾选状态，注意：将【嵌入的媒体】勾选，并将【向上轴】设置为【Y向上】，确定导出。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/97f85a19e269da699ae20a5174eda325.png)
4.找到导出文件，拖入unity视图中即可使用。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a93ed5c60ef28318bc3e29b031bfaf21.png)

