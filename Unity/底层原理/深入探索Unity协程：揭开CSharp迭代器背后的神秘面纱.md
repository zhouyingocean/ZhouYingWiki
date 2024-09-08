
协程是一种特殊类型的迭代器方法，允许你在多个帧之间分段执行代码。可以用来处理时间延迟、异步操作和顺序执行的任务，而不阻塞主线程。Unity协程的实现依赖于C#语言提供的迭代器相关的语言特性，所以想要弄清楚Unity协程的底层原理，必须先了解C#的迭代器的基本功能。

# C#迭代器

## 迭代器的基本概念

1. **迭代器是什么？** 迭代器是一种简化遍历集合或序列的工具。你可以用它来逐个访问集合中的每个元素，而不需要自己编写复杂的循环逻辑。迭代器通过生成一个可枚举的序列，让你逐个取出元素。
    
2. **`yield` 关键字** 。在 C# 中，`yield` 关键字是迭代器的核心。它帮助你创建一个可以暂停和恢复的迭代过程。使用 `yield` 关键字，你可以逐步生成序列中的每个元素，而不是一次性生成所有元素。
    
    - **`yield return`**：用于返回序列中的一个元素，并暂停迭代器的执行，直到下一次请求。
    - **`yield break`**：用于结束序列的生成，不再返回更多的元素。

## C#迭代器的作用

C#迭代器Enumerator提供了一种可以通过foreach遍历任何一个自定义类型的手段。对于任何一个实现了IEnumerable接口和IEnumerator接口的类型来说，都可以通过foreach语句来像遍历一个集合一样遍历一个对象。

定义一个班级类，由若干学生组成：
~~~csharp
public class Student
{
    public string Name { get; set; }
    
	public override string ToString()
    {
        return Name;
    }
}

public class ClassRoom : IEnumerable
{
    private List<Student> students;

    public ClassRoom()
    {
        students = new List<Student>();
    }

    public void Add(Student student)
    {
        if (!students.Contains(student))
        {
            students.Add(student);
        }
    }

    public void Remvoe(Student student)
    {
        if (students.Contains(student))
        {
            students.Remove(student);
        }
    }

    public IEnumerator GetEnumerator()
    {
        return new StudentEnumerator(students);
    }
}

 public class StudentEnumerator : IEnumerator
 {
     public StudentEnumerator(List<Student> students)
     {
         this.students = students;
     }
 
     private List<Student> students;
     private int currentIndex = -1;
 
     public object Current
     {
         get
         {
             if(0 <= currentIndex && currentIndex<students.Count)
             {
                 return students[currentIndex];
             }
             return null;
         }
     }
 
     public bool MoveNext()
     {
         currentIndex++;
         return currentIndex<students.Count;
     }
 
     public void Reset()
     {
         currentIndex = -1;
     }
 }
~~~
当需要能够编写代码遍历ClassRoom类中的Student对象，如果不借助迭代器，就只能将ClassRoom内部的students集合暴露出来供调用方使用，这样就暴露了ClassRoom内部有关Student对象的存储细节，以后如果Student对象的存储结构变了（比如由List结构变成了数组或者字典等等），对应的调用方的所有代码也得跟着变更。除了直接将students成员暴露出来以外，还有一种方法就是可以让ClassRoom实现IEnumerable接口，这样就可以通过foreach语句来遍历其中的Student对象。

验证代码：
~~~csharp
    ClassRoom c = new ClassRoom();
    c.Add(new Student() { Name = "zzz"});
    c.Add(new Student() { Name = "yyy"});

    foreach (Student s in c)
    {
        Debug.Log(s.ToString());
    }
    Debug.Log("......等价输出........");
	//foreach的等价写法
    IEnumerator enumerator = c.GetEnumerator();
    while (enumerator.MoveNext())
    {
        Debug.Log(((Student)(enumerator.Current)).ToString());
    }

~~~

控制台输出：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240908171018.png)

# Unity协程

通常情况下，我们写的每一段代码，都会在Unity的更新逻辑中在同一帧全部执行完毕。如果我们需要将某一段代码包含的逻辑拆分到不同的帧来分段执行，除了自己手写状态机来实现该流程外，更简单方便的方法就是使用Unity协程。总的来说，Unity协程允许我们在保证整个应用在单线程模式不变的情况下通过编写协程函数并调用开启协程的方法（_StartCoroutine_）将一个任务分到不同的时间段异步执行。

Unity针对开关协程均提供了三个重载方法，以下表格中的方法均是一一对应的开关协程的用法，不能混用。

| 开启协程方法                                                                            | 停止协程方法                                                              |
| --------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| StartCoroutine(string methodName)/StartCoroutine(string methodName, object value) | StopCoroutine(string methodName)和StopCoroutine(Coroutine)           |
| StartCoroutine(IEnumerator routine)/StartCoroutine(IEnumerator routine)           | StopCoroutine(Coroutine routine)和StopCoroutine(IEnumerator routine) |

## Yield Return延迟函数

Uniyt协程中的协程函数通过yield return后面的WaitForSeconds、WaitForEndOfFrame等可以控制延迟多少秒、多少帧之后再执行，诸如此类效果是如何实现的呢？关键点在于yield return语句后面的对象类型。我们知道，Unity协程中常见的yield return有这么几种：
~~~csharp
  yield return new WaitForSeconds(1);

  yield return new WaitForEndOfFrame();

  yield return new WaitForFixedUpdate();
~~~
转到上诉三个函数定义源码处，不难看出它们均继承于**YieldInstruction**。Unity就是根据**yield return**返回的对象类型来判断到底应该延迟多长时间来执行下一段代码的。

## 总结

Unity的协程的实现原理是基于C#语言的迭代器特性，通过定义一个协程函数（通过**yield return**返回），将协程函数缓存为一个**IEnumerator**的对象，然后根据该对象的**Current（是一个YieldInstruction对象或者null）** 来判断下一次执行需要间隔的时间，等到间隔时间结束后执行**MoveNext**执行下一阶段的任务，并继续根据新的**Current**确定下一次等待的时间间隔，直到**MoveNext**返回**false**标志着协程终止。

大致可以用以下流程图来表示Unity协程的执行过程：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240908180324.png)

# 自定义实现一个有趣的协程方法

理解了Unity协程的实现原理之后，我们完全可以自己写代码来实现类似Unity中的**StartCoroutine**的效果。比如，我们编写一个自己的开启携程的方法：此方法规定能够接受一个返回IEnumerator的协程函数，并且可以根据yield return后面返回的字符串的长度来等待相应的秒数，比如**yield return "1234"**，那么就等待4秒之后再执行后面的代码，如果**yield return "100"**, 那么就等待3秒之后再执行后面的代码，如果**yield return**后面的对象不是**string**，则默认等待一帧之后再执行。有了前文的基础，我们很容易写出如下代码：
~~~csharp
	/// <summary>
    /// 用来存储创建的迭代器对象
    /// </summary>
    private IEnumerator taskEnumerator = null;
    /// <summary>
    /// 用来记录任务是否完成的标记
    /// </summary>
    private bool isDone = false;
    private float currentDelayTime = 0f;
    private float currentPassedTime = 0f;
    private int delayFrameCount = 1;
    private bool delayFrame = false;
    private bool isCoroutineStarted = false;

    private void MyStartCoroutine(IEnumerator enumerator)
    {
        if (enumerator == null) return;
        isCoroutineStarted = true;
        taskEnumerator = enumerator;
        PushTaskToNextStep();
    }

    private void Start()
    {
        MyStartCoroutine(YieldFunction());
    }

    private IEnumerator YieldFunction()
    {
        //第一段代码
        Debug.Log("first step......");
        yield return 1;

        //第二段代码
        Debug.Log("second tep......");
        yield return 2;

        //第三段代码
        Debug.Log("third step......");
        yield return 3;

        //第四段代码
        Debug.Log("forth step......");
        yield return 4;
    }

    private void PushTaskToNextStep()
    {
        isDone = !taskEnumerator.MoveNext();
        if (!isDone)
        {
            if (taskEnumerator.Current is string)
            {
                currentDelayTime = (taskEnumerator.Current as string).Length;
                currentPassedTime = 0f;
                delayFrame = false;
            }
            else
            {
                delayFrame = true;
                delayFrameCount = 1;
            }
        }
        else
        {
            isCoroutineStarted = false;
        }
    }

    private void Update()
    {
        if (isCoroutineStarted)
        {
            if (delayFrame)
            {
                delayFrameCount--;
                if (delayFrameCount == 0)
                {
                    Debug.Log(string.Format("第{0}帧（运行数:{1}）结果：阶段任务已完成!", Time.frameCount, Time.time));
                    PushTaskToNextStep();
                }
            }
            else
            {
                currentPassedTime += Time.deltaTime;
                if (currentPassedTime >= currentDelayTime)
                {
                    Debug.Log(string.Format("第{0}帧（运行数:{1}）结果：阶段任务已完成!", Time.frameCount, Time.time));
                    PushTaskToNextStep();
                }
            }

        }
    }
~~~
控制台输出与预期一致：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240908181352.png)

挺有趣哈！