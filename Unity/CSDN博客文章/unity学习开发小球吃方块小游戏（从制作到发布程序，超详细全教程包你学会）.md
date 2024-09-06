@[toc](unity小球吃方块开发过程)

### 你将学会用unity开发小游戏的基础知识
 通过创建对象、添加脚本、控制相机跟随、旋转对象、碰撞检测、显示文本和发布程序七个实验来对Unity 3D游戏开发过程中的场景、Plane、Sphere、Cube对象、脚本、碰撞检测、UI以及程序发布等问题进行学习和练习。在博客文末最后列出了Unity 3D的各个菜单栏以及它们所包含的下拉菜单及其译名。
### 吃方块游戏超详细全教程，保姆式教学包你学会
###  一、创建对象
知识点：
1.掌握在Unity 3D中创建项目、场景、Plane和Sphere等。
2.掌握在Unity 3D中材质的应用。
 
学会在Unity 3D中创建项目、场景、Plane和Sphere，学会材质的应用。
实验内容
#### 创建PlayBall小球吃金币游戏项目，创建地面和小球。
操作步骤：
1)新建项目，依次输入项目名称，选择项目存储路径，如图2-1所示。
![图2-1新建Unity 3D项目](https://i-blog.csdnimg.cn/blog_migrate/24908a6d7335deaf249a36136b10b460.png)


2)点击“Create project”创建项目进入Unity 3D界面，右上角“Layout”可修改布局，Unity 3D有多种布局，读者可以根据自己的习惯选择，下图为“Layout”|“Tall”布局，本实验截图均为Tall布局，如图2-2所示。
![图2-2 Unity 3D中Tall布局](https://i-blog.csdnimg.cn/blog_migrate/3589a148f77f657464038afe648628bd.png)


3)在“Project”窗口中新建文件夹Scenes，存储游戏场景，按“Ctrl+S”存储当前游戏场景main，如图2-3所示。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/e93b3ac7b3c5497f7c6e8c8e4811b4ac.png)

4)在“Hierarchy”窗口中创建游戏地面，右键选择“3DObject”|“Plane”，因为其为游戏地面，将其命名为Ground，如图2-4所示。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/9b29d1d99210aa2a71be28c6b7c6cd65.png)

5)选中Ground对象，在“Inspector”窗口的“Transform”右侧的齿轮选择“Reset”，将地面对象放置在坐标系原点，
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/b5cadef13f59dc3974a14f09e548b488.png)

6)若想修改该地面对象表面颜色，需要为其添加材质。在“Project”窗口中新建文件夹名为Materials，存储材质，在Materials文件夹中新建“Material”材质文件，
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/2b1fee29adfd67401732da68ca923b08.png)


7)将“Material”命名为Ground，选中Ground材质，在“Inspector”窗口中修改“Albedo”颜色为淡蓝色，
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/ae5b3890024b13345c3b4a615d9a1087.png)


8)将该材质与Plane进行关联，将Ground材质用鼠标左键拖动到“Hierarchy”窗口中的Ground对象上
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/bf6748cf6b23b01e65939fa3aed7a2d7.png)

9)在“Hierarchy”窗口创建游戏主角小球对象，右键选择“3D Object”|“Sphere”，并将其命名为Player，
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/ccd3e03af035f295f60bcddd114dfdc4.png)

10)将小球对象放置在坐标系原点，选中小球Player对象，在“Inspector”窗口的“Transform”右侧的齿轮选择“Reset”
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/0a9fb750cb007bdf60039b56df18e3af.png)


11)选择移动按钮，，向上拖动“y”轴绿色箭头，将小球拖到地面上方
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/d600855065417cecaa52f9083f63ba3b.png)

12)点击播放按钮查看游戏运行效果，
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/acf5d08ba7d72d0988d4a918862109f7.png)

13)为小球添加重力。在“Hierarchy”窗口选择小球Player对象，在“Inspector”窗口点击最小面的“Add component”添加组件按钮，添加“Rigidbody”刚体组件，
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a3fa013b22ce3351cc0cdadecc52a254.png)

14)点击播放按钮查看与没加刚体组件时的区别
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/101982ee7c4cdcc2b17c6c2e26e0c115.png)


### 二、添加脚本
实验目的
1.掌握在Unity 3D中创建脚本的方法。
2.掌握在Unity 3D中修改对象的属性。
实验要求
学会在Unity 3D中创建脚本以及修改对象的属性。
实验内容
#### 创建脚本使小球动起来，并用键盘控制小球的运动。
操作步骤：
1)为使小球运动起来，要为小球对象添加脚本文件。在“Project”窗口中新建文件夹Scripts，存储脚本文件，在“Hierarchy”窗口选择小球Player对象，在“Inspector”窗口点击最下面的“Add component”添加组件按钮，输入Player，选择“New Script”，Language选择默认的“C Shape”，点击“Creat and Add”创建脚本文件
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/e2398f0b3802f47c71d50aabc5b800ed.png)

2)将Player脚本文件拖入到Scripts文件夹中，
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/b9c636f46c53554c77a5c8011aa5f143.png)


3)双击player脚本文件，进入编辑器，本例进入的是Microsoft Visual Studio编辑器，
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/7384b24a1dfe783f98eb7ffbb1ebb72c.png)

4)为使小球运动起来，需要先得到小球刚体，并对刚体施加一个方向的力，具体代码如下：

```csharp
using UnityEngine;
using System.Collections;
public class player : MonoBehaviour {
    private Rigidbody rd;    //定义刚体对象
	// Use this for initialization
	void Start () {
        rd = GetComponent<Rigidbody>();   //取得小球的刚体
	}
		// Update is called once per frame
	void Update () {
        rd.AddForce(new Vector3(1, 0, 0));  //对小球刚体施加一个单位X轴正向的力
	}}
```
5)点击播放，查看小球运动状态，如图所示。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/d159667bfb19404b89168e0f33472ff0.png)


6)将上例中的Vector3(1, 0, 0)修改为Vector3(-1, 0, 0)播放查看运动效果，或者修改为Vector3(0, 0, 1)和Vector3(0, 0, -1)分别查看效果。

7)用键盘控制小球的移动，需要先取得输入，再通过输入控制小球的移动，修改Update代码：
	

```csharp
Void Update () {
float h = Input.GetAxis("Horizontal");//取得键盘的水平输入
         rd.AddForce(new Vector3(h, 0, 0));
	}
```

8)点击播放，试着按键盘的左右方向或者“A”“D”键控制小球的水平方向移动，修改Update代码，实现控制小球四个方向的移动

```csharp
void Update () {
float h = Input.GetAxis("Horizontal");  //取得键盘的水平输入
float v = Input.GetAxis("Vertical");    //取得键盘的垂直输入
rd.AddForce(new Vector3(h, 0, v) * 5);
}
```

9)至此可以用键盘实现对小球的方向控制，若果想使小球运动的更快，可以对施加的力乘上系数，代码如下：
         rd.AddForce(new Vector3(h, 0, v) * 10);  //对施加的力乘以系数
10)也可将力的系数设为公共变量，这样随时可以在Unity 3D页面修改系数的值，代码如下：
```csharp
using UnityEngine;
using System.Collections;
public class Player : MonoBehaviour {
private Rigidbody rd;
public int force = 5;    //定义公共变量force，为施加力的系数
	// Use this for initialization
	void Start () {
        rd = GetComponent<Rigidbody>();
	}
	// Update is called once per frame
	void Update () {
float h = Input.GetAxis("Horizontal");
float v = Input.GetAxis("Vertical");
        	rd.AddForce(new Vector3(h, 0, v) * force);   //对施加的力乘以系数
	}
}
```
11)设置公共变量之后，在Player对象的“Inspector”窗口可以看到，player脚本中多了Force值，这样随时可以在Unity 3D页面修改力的系数值，
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/1d1490ab57512f2cbe085a984271e7f8.png)


12)增大游戏地面面积。在“Hierarchy”窗口选择Ground对象，在“Inspector”窗口的“Transform”中修改“Scale”值，将X、Z都修改为2，
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/cae19c1ce8ffb6dffd27e3c0ef158d2a.png)

###  三、控制相机跟随
实验目的
1.掌握在Unity 3D中移动和选择对象等操作。
2.了解在Unity 3D中控制相机跟随的方法。
实验要求
学会在Unity 3D中移动和选择对象等操作及了解控制相机跟随的方法。
实验内容
#### 控制相机跟随小球移动。
操作步骤：
1)点击移动按钮，选择相机对象，向上拖动“Y”轴，将其拖动到稍高一点的位置，每次调整相机时，在右下角会出现相机预览图，以便观察其视野，![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/4ebc271d27ba8443e2d7e1e53bb25c14.png)

2)点击旋转按钮，旋转相机角度，使其面向小球
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a8b1958e0baa8378f1ec0fb2cfcaad85.png)

3)若想相机跟随小球运动，需要为相机添加脚本。在“Hierarchy”窗口选择“Main Camera”对象，在“Inspector”窗口点击最小面的“Add component”添加组件按钮，输入follow，选择“New Script”，选择默认的“C Shape”语言，点击“Creat and Add”创建脚本文件，
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/6136dddc280fb6de83fd11529ef3d983.png)


4)将follow脚本拖入到Scripts文件夹中。若想相机跟随小球运动，需要相机与小球的距离保持不变。首先，在follow脚本中要取得小球的位置信息。代码如下：

```csharp
using UnityEngine;
using System.Collections;
public class follow : MonoBehaviour {
public Transform playerTransform;   //定义公共变量记录小球的位置信息
	// Use this for initialization
	void Start () {
	}
	// Update is called once per frame
	void Update () {
	}
}
```

5)公共变量定义好后，在“Main Camera”对象的“Inspector”窗口可以看到，follow脚本中多了playerTransform，将“Hierarchy”窗口中的小球Player对象拖到playerTransform上，使playerTransform绑定小球的位置信息
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/87a409655050943a0a2b24bffdebdd94.png)

6)取得小球的位置信息后，添加代码实现相机跟随小球移动，代码如下：

```csharp
using UnityEngine;
using System.Collections;
public class follow : MonoBehaviour {
public Transform playerTransform;   //定义公共变量记录小球的位置信息
private Vector3 offset;    //定义相机和小球之前的距离
	// Use this for initialization
	void Start () {
    		offset = transform.position - playerTransform.position;    //计算相机和小球之间距离
	}
	// Update is called once per frame
	void Update () {
      	transform.position = playerTransform.position + offset;  //保持距离
	}
}
```

###   四、旋转对象
实验目的
1.掌握在Unity 3D中创建cube对象。
2.了解在Unity 3D中旋转对象的方法。
实验要求
学会在Unity 3D中创建cube对象并了解旋转对象的方法。
实验内容
#### 控制小球移动范围并加入可旋转的金币。
操作步骤：
1)创建地面边界墙，在“Hierarchy”窗口创建cube对象，右键选择“3D Object”|“Cube”，选中cube对象，在“Inspector”窗口的“Transform”中修改“Position”的X、Y、Z为0,0,10，“Scale”的X、Y、Z为20,2,1，如图2-25所示。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/32295aebd28a33ce4d603ae3d3405521.png)

2)在“Hierarchy”窗口选中cube对象，按“Ctrl+D”复制cube对象，分别创建其他三面墙体，三面墙体的“Transform”参数分别为（PositionX、Y、Z为0,0,-10，ScaleX、Y、Z为20,2,1）、（PositionX、Y、Z为10,0,0，ScaleX、Y、Z为1,2,20）、（PositionX、Y、Z为-10,0,0，ScaleX、Y、Z为1,2,20），
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/296dca898ae8c98a197878ec4ce2834d.png)

3)在“Hierarchy”窗口中，将创建好的四个cube墙体对象拖动到Ground对象上，形成父子关系
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/bc71d26323822acce4a4dd03db91e521.png)


4)创建可收集的金币。在“Hierarchy”窗口新建cube对象，命名为Pickup，选中cube对象，在“Inspector”窗口的“Transform”中修改“Rotation”的X、Y、Z为45,45,45，“Scale”的X、Y、Z为0.5,0.5,0.5，
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/f097e4ab0a7245037f2801f189036b03.png)

5)点击Local按钮，切换成全局坐标系，调整该cube对象的高度，使其立在地面上

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/8402cb2c377c2169c42bbff250bcfd6d.png)

6)在Materials文件夹中新建Material，将Material命名为Pickup，选中Pickup材质，在“Inspector”窗口中修改“Albedo”颜色为金色，并将该材质与Pickup对象关联
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/7cc2306085618c02f4c7b270aaeda4ca.png)

7)因为还要创建很多个Pickup对象，所以把Pickup对象做成预制体，在“Project”窗口中新建文件夹Prefabs，存储预制体，将“Hierarchy”窗口中的Pickup对象用鼠标左键拖动到该文件夹内
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/dff864155fb2010e78822d03a0d50e0e.png)

8)将Prefabs文件夹中的Pickup对象拖入到左侧的舞台上，调整高度，使其立于地面上，选中Pickup对象，并按“Ctrl+D”复制多个，调整位置，如图2-32所示。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a888f8e6a68ba6c6a2b417ebf6eae388.png)

9)在“Hierarchy”窗口中，创建空的游戏物体“Create Empty”，并将该游戏物体放到原点，将所有的Pickup放到该物体上
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/5eeb40d6da493cdf0b1641eb4eab74f4.png)

10)为了使所有的Pickup都旋转，选择“Project”窗口下Prefabs文件夹中的Pickup，在“Inspector”窗口点击最小面的“Add component”添加组件按钮，输入pickup，选择“New Script”，选择默认的“C Shape”语言，点击“Creat and Add”创建脚本文件，并将该脚本放在Scripts文件夹下
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/57941d746ee53bd5e4086c0a86611658.png)

11)双击进入该脚本，添加如下代码，使金币旋转起来。

```csharp
using UnityEngine;
using System.Collections;
public class pickup : MonoBehaviour {
	// Use this for initialization
	void Start () {
	}
	// Update is called once per frame
	void Update () {
        transform.Rotate(new Vector3(0, 1, 0));  //使对象绕y轴旋转
	}
}
```

12)点击播放，游戏运行如图下图所示。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/26ec1d834adbfc01c4978fcacf6d5456.png)

### 五、碰撞检测
实验目的
1.掌握在Unity 3D中为对象设置标签。
2.了解在Unity 3D中碰撞检测的方法。
实验要求
学会在Unity 3D中为对象设置标签以及了解碰撞检测的方法。
实验内容
#### 实现小球吃掉金币效果。
操作步骤：
1)为了检测小球碰撞到金币还是墙体，为金币Pickup对象设置标签，选择“Project”窗口下Prefabs文件夹中的Pickup，在“Inspector”窗口“tag”下拉菜单中选择“Add Tag”
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/89d4be8f1da5d2ced1dc75213ff45f06.png)

2)进入如图界面。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/2eb4a979920c8f244da64dece74ea6d1.png)

图2-37  Add Tag界面
3)点击“+”，添加标签Pickup
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/41b5a7a49036caee7d56a91699bb1d01.png)

4)再次选择“Project”窗口下Prefabs文件夹中的Pickup，在“Inspector”窗口“tag”下拉菜单中选择Pickup
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/ffa3de7f591dc8d8e7d3089047f2a722.png)

5)为了实现小球碰撞金币使金币消失，打开Player脚本，修改代码如下：

```csharp
using UnityEngine;
using System.Collections;
public class player : MonoBehaviour {
private Rigidbody rd;
public int force = 5;
	// Use this for initialization
	void Start () {
        rd = GetComponent<Rigidbody>();
	}
	// Update is called once per frame
	void Update () {
float h = Input.GetAxis("Horizontal");
float v = Input.GetAxis("Vertical");
        	rd.AddForce(new Vector3(h, 0, v) * force);
	}
void OnCollisionEnter(Collision collision) {//碰撞检测函数
if(collision.collider.tag == "Pickup") {//判断小球是否碰到金币
            Destroy(collision.collider.gameObject);   //使金币消失
        }
}
```

}
6)运行游戏效果如图下图所示。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/15dfe0ee81c55a47273d55cf589ac528.png)

7)游戏运行后发现，在碰撞金币使金币消失时，会有撞到物体的反弹效果，如果不想要这种效果，首先选择“Project”窗口下Prefabs文件夹中的Pickup，在“Inspector”窗口“Box Collider”中，勾选“Is Trigger”
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/589b07c01033b828a683fd853049ab0b.png)

8)修改Player脚本如下：

```csharp
using UnityEngine;
using System.Collections;
public class player : MonoBehaviour {
private Rigidbody rd;
public int force = 5;
	// Use this for initialization
	void Start () {
        	rd = GetComponent<Rigidbody>();
	}
	// Update is called once per frame
	void Update () {
float h = Input.GetAxis("Horizontal");
float v = Input.GetAxis("Vertical");
        rd.AddForce(new Vector3(h, 0, v) * force);
	}
void OnTriggerEnter(Collider collider)    //检测接触
    {
if(collider.tag == "Pickup")
        {
            Destroy(collider.gameObject);
        }
}
}
```
###   六、显示文本
实验目的
1.了解在Unity 3D中UI的使用方法。
实验要求
了解在Unity 3D中UI中Text控件的使用方法。
实验内容
#### 在小球吃掉金币时显示分数以及吃光所有金币后显示胜利。
操作步骤：
1)如果想在小球吃掉金币时加分，并实时显示分数，修改Player代码如下：

```csharp
using UnityEngine;
using System.Collections;
public classplayer : MonoBehaviour {
private Rigidbody rd;
public int force = 5;
private int score = 0;   //定义分数变量
	// Use this for initialization
	void Start () {
        rd = GetComponent<Rigidbody>();
	}
	// Update is called once per frame
	void Update () {
float h = Input.GetAxis("Horizontal");
float v = Input.GetAxis("Vertical");
        	rd.AddForce(new Vector3(h, 0, v) * force);
	}
void OnTriggerEnter(Collider collider)
    {
if(collider.tag == "Pickup")
        {
            score++;      //每次接触金币对分数加1
            Destroy(collider.gameObject);
        }
}
}
```
2)若想在游戏时显示分数，需要加入UI，在“Hierarchy”窗口中，右键“UI”|“Text”，切换到2D显示
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/1fdf89fbf26a6245226e25a5ed4e0ba7.png)


3)选择Text对象，在“Inspector”窗口“Rect Transform”中，点击左侧方框，按住“Alt”键，选择左上角的方框
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/ae379db5f512c29e0594d911239bbad0.png)

4)调整Text位置，将其向右下稍微调整，游戏运行，效果如图所示。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/3a6a286d145dcea7852a0185ac617d7f.png)

5)为了在Text对象中显示分数，需要将Text对象与Player脚本关联，修改Player脚本代码如下：

```csharp
using UnityEngine;
using System.Collections;
using UnityEngine.UI;
public class player : MonoBehaviour {
private Rigidbody rd;
public int force = 5;
public Text text;      //定义Text公共变量，准备关联Text对象
private int score = 0;
	// Use this for initialization
	void Start () {
        rd = GetComponent<Rigidbody>();
	}
	// Update is called once per frame
	void Update () {
float h = Input.GetAxis("Horizontal");
float v = Input.GetAxis("Vertical");
        	rd.AddForce(new Vector3(h, 0, v) * force);
	}
void OnTriggerEnter(Collider collider)
    {
if(collider.tag == "Pickup")
        {
            score++;
            Destroy(collider.gameObject);
        }
}
}
```

6)在Player对象的脚本中会出现Text，将Text对象拖入到Text后面的框中
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/3e63fe5919059eac435229e8ddee1cca.png)

7)通过拖动已经在Player中取得了Text对象，然后将分数传递给Text，修改Player代码如下：

```csharp
using UnityEngine;
using System.Collections;
using UnityEngine.UI;
public class player : MonoBehaviour {
private Rigidbody rd;
public int force = 5;
public Text text;
private int score = 0;
	// Use this for initialization
	void Start () {
        rd = GetComponent<Rigidbody>();
	}
	// Update is called once per frame
	void Update () {
float h = Input.GetAxis("Horizontal");
float v = Input.GetAxis("Vertical");
        	rd.AddForce(new Vector3(h, 0, v) * force);
	}
void OnTriggerEnter(Collider collider)
    {
if(collider.tag == "Pickup")
        {
            score++;
            text.text = score.ToString();   //将分数赋值给Text
            Destroy(collider.gameObject);
        }
}
}
```

8)运行游戏，效果如图2所示。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/fadc6dcc131866a82b1c78324c9e5055.png)


9)当把所有金币都吃掉后，显示游戏胜利。在“Hierarchy”窗口中，在“Canvas”上右键“UI”|“Text”，再创建一个Text用来显示胜利信息
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/3681fd6d4543d14d847bce615a5cee60.png)

10)选择调整按钮![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/c7adc4b6907ed24b9e0f8b6d83944855.png)
调整Text（1）对象的大小，在Text（Script）中修改Text（1）的一些属性
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/4513615a1a25dec10a747d6e3d1018bf.png)


11)在“Inspector”窗口中取消Text（1）前面的对号，使其在游戏刚开始运行时不显示，
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/4ea92dac8fc939297e1d1aebf1940847.png)

图2-49  在Inspector中取消Text（1）前面的对号
12)用同样的方法关联Player和Text（1）对象，并修改Player脚本的代码如下：

```csharp
using UnityEngine;
using System.Collections;
using UnityEngine.UI;
public class player : MonoBehaviour {
private Rigidbody rd;
public int force = 5;
public Text text;
private int score = 0;
public GameObject winText;   //定义存放胜利消息的Text
	// Use this for initialization
	void Start () {
        rd = GetComponent<Rigidbody>();
	}
	// Update is called once per frame
	void Update () {
float h = Input.GetAxis("Horizontal");
float v = Input.GetAxis("Vertical");
        	rd.AddForce(newVector3(h, 0, v) * force);
	}
void OnTriggerEnter(Collider collider)
    {
if(collider.tag == "Pickup")
        {
            score++;
            text.text = score.ToString();
if(score == 12)
            {
                winText.SetActive(true);  //如果全部金币（本例为12个）全部吃完，显示胜利消息
            }
            Destroy(collider.gameObject);
        	}}}
```

13)在Player对象的脚本窗口中会出现winText，将Text（1）对象拖入到winText后面的框中，![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/58859cba710e070ed01722960664084a.png)

图2-50  Player对象的脚本窗口
14)运行游戏，当吃光所有金币后效果如图所示。
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/affba6ce6a3bad8e90e89dd273df8ba3.png)

###  七、发布程序
实验目的
1.掌握在Unity 3D中发布程序的方法。
实验要求
掌握在Unity 3D中发布程序的方法以及运行发布后的程序。
实验内容
#### 发布PlayBall的Windows程序并运行该程序。
操作步骤：
1)发布windows平台的exe游戏，点击“File”|“Build Setting”
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/2d11e41d122dfa365b1553230cfba519.png)

2)选择“PC，Mac&Linux…”，选择“TargetPlatform”|“Windows”，“Architecture”中x86为32位操作系统应用程序，x64为64位应用程序，根据实际情况选择即可，点击“Build”即可发布程序。
3)运行exe文件运行游戏
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/ec73f53e1fdd7851e20df41d2343c937.png)

图2-53  游戏运行开始界面
4)勾选Windows，点击“Play”运行游戏
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/755e6a730e56cb7aaf9d6ae7f5e22afc.png)


### 八、Unity 3D的各个菜单栏以及它们所包含的下拉菜单及其译名
主菜单	包含的子菜单
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/730089b91eddd514e4071a3a01226252.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/c05599cfed54f5c816b8e002b40726b1.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/ecc232a0d7b4b8a215e2fdcaf043cc30.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/66099c760fc5c019de20f4d8fe82e819.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/e8fba26686e67797a3d3a0e06debc00e.png)

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/49778a4d2638bd559bc9530f12757d51.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/558000b7f1fab99d9f8857ecf52d714d.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/52ef2537a9b48d1cc5723826b2a622d6.png)


