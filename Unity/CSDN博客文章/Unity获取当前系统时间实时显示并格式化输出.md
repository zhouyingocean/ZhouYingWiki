@[TOC](unity获取当前系统时间实时显示并格式化输出)

# 前言
我们希望在Unity开发的软件里面如果当前系统时间戳并显示在UI上，那么如何实现呢？其实很简单，C#为我们提供了一个关于时间的类--DateTime，调用该类下的方法即可获取当前系统时间。

# C# DateTime类学习
C#中的DateTime类是一个非常重要的类，用于处理日期和时间相关的操作。以下是对C# DateTime类的一个详细学习总结：

## DateTime类的定义与用途
DateTime是.NET框架类库中的一个预定义类，用于表示日期和时间。它可以存储从公元0001年1月1日午夜12:00:00.000开始至今的时间，以100纳秒为单位（即Ticks）。DateTime类包含了许多用于执行与日期和时间相关的操作的方法，如加减时间间隔、比较日期和时间、格式化日期和时间的字符串表示等。

## 二、DateTime类的构造函数
C#提供了多种方式来初始化DateTime对象，包括使用默认的构造函数、使用指定的年、月、日、时、分、秒和毫秒等。以下是一些示例：

```csharp
DateTime date0 = new DateTime(); // 默认构造函数，表示当前本地时间  
DateTime date1 = new DateTime(2022, 7, 11); // 仅指定年、月、日  
DateTime date2 = new DateTime(2022, 7, 11, 11, 23, 10); // 指定年、月、日、时、分、秒
```

## DateTime类的属性
DateTime类提供了许多属性来访问日期和时间的各个部分，如年份（Year）、月份（Month）、日期（Day）、小时（Hour）、分钟（Minute）、秒钟（Second）等。以下是一个示例：

```csharp
DateTime now = DateTime.Now;  
int year = now.Year;  
int month = now.Month;  
int day = now.Day;  
int hour = now.Hour;  
int minute = now.Minute;  
int second = now.Second;
```

## 注意事项
时区问题：DateTime.Now返回的是当前本地时间，而DateTime.UtcNow返回的是UTC时间。如果需要进行时区转换，可以使用TimeZoneInfo类。

# 场景搭建
新建一个Unity工程，新建一个场景Scene，在Hierarchy面板右键新建一个Text文本组件。将其移动至场景中间位置并调整大小和居中对齐。
如下图所示：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/ca205d4594fb55f4451725c50b547a8e.png)

# 核心代码
新建脚本ShowTime.cs ，编写核心代码如下：
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class ShowTime : MonoBehaviour
{
    // Start is called before the first frame update
    /// <summary>
    /// 显示时间的文本
    /// </summary>
    public Text TxtCurrentTime;
    /// <summary>
    /// 是否允许显示时间
    /// </summary>
    public bool isShowTime = true;

    // Update is called once per frame
    void Update()
    {
        if (!isShowTime) return;
        //获取系统当前时间
        DateTime NowTime = DateTime.Now.ToLocalTime();
        //将时间格式化输出
        TxtCurrentTime.text = NowTime.ToString("yyyy-MM-dd HH:mm:ss");
    }
}

```
将脚本挂载到任意场景中激活的游戏对象上，并将Text组件拖拽赋值到该脚本TxtCurrentTime的引用。
# 效果显示
运行查看成功显示当前电脑系统时间戳。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/e7afb6fa7ce17a2d4c529e5152e321cf.png)


