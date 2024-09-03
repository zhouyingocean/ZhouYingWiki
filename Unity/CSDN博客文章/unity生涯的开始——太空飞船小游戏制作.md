***初识unity做的一个小 demo***

1、飞船等场景的设置
场景布局：把灯光放到合适的位置，摄像机拉到灯光上方，在scene里面新建一个quad作为背景，给它贴上材质图，把飞船player拖到场景中，调整位置，在飞船尾巴添加一个喷火特效。

2、给飞船写一个飞行脚本	
Player.cs：

```csharp
 public float speed = 5.0f;

 float moveH = Input.GetAxis("Horizontal");
        float moveV = Input.GetAxis("Vertical");
        Vector3 move = new Vector3(moveH, 0, moveV);
        transform.Translate(speed * move * Time.deltaTime);
```

在unity里把player.cs拖拽到飞船那里，作为飞船的子对象，这样用键盘上上下左右键就可以控制飞船运动了。

3、做子弹的飞行和prefab
在hierarchy新建一个game empty命名为bolt，新建一个quad，作为bolt子对象，给它贴上一个materials，子弹的模型，调整子弹在飞船下方的位置，也给子弹做一个飞行脚本bolt_move.cs：
 

```csharp
 public float speed = 5.0f;
    //沿着z轴正方向飞行
	// Update is called once per frame
	void Update () {
        //  transform.Translate(0,0,speed*Time .deltaTime);
        transform.Translate(Vector3.forward * speed * Time.deltaTime);
```

同样把脚本拖到子弹那里
给子弹添加刚体组件和胶囊体碰撞器：

给子弹做一个预制包，放到_prefab里：
直接把hierarchy里的bolt拖拽到assets里的_prefab就行。

4、子弹的发射
做一个子弹发射的脚本，放到player里：

```csharp
//时间间隔
    public float fireRate = 0.5f;
    //每隔0.5f发射子弹
    public float nextFire = 0.0f;

    public GameObject shot;
    public Transform shotSpawn;

   //点击鼠标发射子弹
        if (Input.GetButton("Fire1") && Time.time > nextFire)
        {
            //存在问题的一系列的子弹出来了，需要用时间控制子弹的发射
            nextFire = Time.time + fireRate;

            //Instantiate(实例化物体‘位置’角度）
            Instantiate(shot, shotSpawn.position, shotSpawn.rotation);
```

点击player，在inspector完成设置：

运行一下，子弹就会从飞机下方发射出来.

5、子弹的销毁和碰撞检测
新建一个cube命名为boundary，调整大小，位置，使它把飞船包围住
做一个子弹销毁的脚本destbyboundary.cs：

```csharp
 void OnTriggerExit(Collider other)
    {
        Destroy(other.gameObject);
    }
```

拖拽到boundary里：
相关设置如下

运行一下，子弹飞行出boundary边界的时候就是销毁.

6、添加陨石运动和销毁
新建一个gameobject命名为Asterial，拖拽一个陨石模型作为子对象，调整其在场景中的位置，给它做一个运动脚本as_move.cs：
 

```csharp
 public float speed = 5.0f;
    
	void Update () {
        transform.Translate(Vector3.back * speed * Time.deltaTime);

    }
```

并为其添加刚体组件和胶囊体碰撞器

同时给它做一个预制包，一会要自动出现.

7、添加tag
在as_move.cs脚本中添加下面代码：
 //小行星rigidbody和collider trigger，boundary有collider trigger，当trigger enter的时候自然会响应了。
   

```csharp
 void OnTriggerEnter(Collider other)
    {
        //print(other.name);//相应的名称就是boundary，销毁就是boundary，所以需要修改一下
        //实例化粒子物体
        if (other.tag == "Boundary")
            return;
       
            gameController.GameOver();
      
        Destroy(other.gameObject);
}
```

在此做属性响应修改.

8、陨石和飞船的爆炸
在as_move.cs添加如下代码：
 

```csharp
 public GameObject explosion;
    public GameObject playerExplosion;

//实例化小行星的爆炸粒子效果，在小行星的位置处生成粒子效果
        Instantiate(explosion, transform.position, transform.rotation);
        //实例化player，也就是飞船的爆炸例子效果，在飞船的位置处生成粒子效果
        if (other.tag == "Player")
        {
            Instantiate(playerExplosion, other.transform.position, other.transform.rotation);

        }
        Destroy(other.gameObject);

        //小行星被击中后玩家分值增加，需要把增加的这个过程通知到Text控件显示
        gameController.AddScore(scoreValue);

        Destroy(gameObject);
    }
```

如图设置
运行之后就会出现射击陨石和碰撞之后的爆炸效果了.
9、陨石批量生成：
这里要用到一个协程的方法：

```csharp
IEnumerator WaitAndPrint()
{
yield return new WaitForSecond(5)；
print(“WaitAndPrint”+Time.time);
}
```

新建一个gameobject命名为gamecontroller，新建脚本gamecontroller.cs：
 

```csharp
//实例化小行星的物体，位置
    public GameObject hazard;//代表小行星物体
    public Vector3 spawnValues;//代表生成的x轴和z轴的变化值
    private Vector3 spawnPosition = Vector3.zero;//代表生成位置
    private Quaternion spawnRotation;

    public int hazardCount = 6;

    //延迟生成的时间
    public float spawnWait;

    //不希望游戏一开始就立刻产生小行星，而是等待一段时间，加人变量来控制等待时间
public float startWait = 1.0f;


    //生成小行星的代码
    IEnumerator SpawnWaves()
    {
        yield return new WaitForSeconds(startWait);
        while (true)
        {
            for (int i = 0; i < hazardCount; i++)
            {
                spawnPosition.x = Random.Range(-spawnValues.x, spawnValues.x);
                spawnPosition.z = spawnValues.z;
                spawnRotation = Quaternion.identity;
                Instantiate(hazard, spawnPosition, spawnRotation);
                yield return new WaitForSeconds(spawnWait);
            }
            yield return new WaitForSeconds(2.0f);

void Start () {

        StartCoroutine(SpawnWaves());
		}
```

根据场景设置所需参数
运行一下陨石就可以随机生成了.

10、做一个不同脚本之间的一种数据传递，做一个游戏的生命周期：记录得分，游戏结束，和重新开始

在as_move.cs添加如下代码：
 

```csharp
private GameController gameController;
    public int scoreValue;//增加的分值

 gameController.GameOver();

  void Start()
    {
        //将这里定义的gamecontroller和之前的gamecontroller绑定，一般来说
        //所以我们先通过findwithtag找到物体，得通过getcomponent找到gamecontroller脚本
        GameObject go = GameObject.FindWithTag("GameController");//注意，必须在属性响应那里做修改

        if (go != null)
            gameController = go.GetComponent<GameController>();
        else
            Debug.Log("找不到tag为GameController的对象");
        if (gameController == null)
            Debug.Log("找不到脚本GameController.cs");

    }
```

在gamecontroller.cs添加如下代码：

```csharp
public Text ScoreText;
    private int score;

    public Text gameOverText;
    private bool gameOver;

    public Text restartText;
    private bool restart;

  if (gameOver)
            {
                restartText.text = "按【R】重新开始";
                restart = true;
                break;
            }
        }
    }
	// Use this for initialization
	void Start () {
        score = 0;
        ScoreText.text = "得分：   " + score;
        gameOverText.text = "";
        gameOver = false;

        restartText.text = "";
        restart = false;
        StartCoroutine(SpawnWaves());
	}
	//修改分值
    public void AddScore(int newScoreValue)
    {
        score += newScoreValue;
        ScoreText.text = "得分：   " + score;
    }
    //修改结束的属性
    public void GameOver()
    {
        gameOver = true;
        gameOverText.text = "游戏结束";
    }
    void Update()
    {
        if (restart)
        {
            if (Input.GetKeyDown(KeyCode.R))
                Application.LoadLevel(Application.loadedLevel);
        }
```

  在场景里做如下设置：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/6aa999bdb2fb827c4aa0de28765d9d53.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/ee439f8232c8d853c7eecb4464c058c6.png)

至此，一个太空飞船小游戏基本完成了

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/8031b937dfacb42e5e5027b6d6e07b21.png)

运行游戏：

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/50f00045cef5157d88f648081aa267cd.png)

