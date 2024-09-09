![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240908182923.png)

# 问题背景

首先提一下之前项目开发时遇到的一个将自定义类型作为Dictionary键的坑。

项目中，我们有两个业务类BusinessA和BusinessB，因为某个需求，我们需要将这两个类建立一个映射关系，故引入字典Dictionary数据结构将它们关联起来：
~~~ Csharp
private Dictionary<BusinessA, BusinessB> businessDic = new Dictionary<BusinessA, BusinessB>();

//对外提供查找方法，通过A从字典中找到B
 public BusinessB FindB(BusinessA a)
{
    if (businessDic.ContainsKey(a))
    {
        return businessDic[a];
    }
    return null;
}
~~~

因为项目是协同开发的，随着业务逻辑不断增加，在某些其他业务逻辑中对字典中的某些Key对象做了修改（BusinessA对象的数据不变），之后当我们再次想要通过该对象查找对应的BusniessB对象时，却发现返回null。当时我们整个开发组排查了好久才发现这个bug的原因。

# 问题分析

这个bug的根本原因在于没有深入的理解C#中的Dictionary的底层存储原理：

>当你将一个键添加到字典中，Dictionary会使用哈希函数计算该键的哈希码，这是一个整数值，用于确定键在内部数组中的位置。

我们一开始以为如果将一个引用类型的对象作为Dictionary的key，只要key对象的数据没有变，那么就可以通过key获取对应的value。

## 使用Dictionary时，Key的必要条件

在C#中，字典(Dcitionary<Tkey,TValue>)使用将Key来快速查找值Value时，字典的键必须满足两个重要的条件：

-  **可比较性**
> 键必须可以被正确地比较以确定其唯一性。字典内部使用Equals方法来比较键，确保相同的键映射到相同的值

- **不可变性**

> 一旦键被添加到字典中，==其值不能被改变==。如果键的状态在被添加到字典后发生变化，字典的查找机制可能会失效，从而引发bug.
## 使用引用类型作为Key的注意事项

### 使用不稳定的键

为了确保字典的正确性，键应该在字典操作期间保持不变。一般来说，应该避免在字典中修改键对象的状态。推荐的做法是使用不可变对象作为键。你可以使用 `readonly` 字段或只读属性来保证键对象的不可变性

### 键的相等性比较

确保同时并正确的实现你的 `Equals` 和 `GetHashCode` 方法。相等性比较应该考虑所有影响对象身份的字段，并且 `GetHashCode` 方法应该始终返回相同的值（如果对象的状态没有改变）。

可以看以下示例代码的输出：
~~~Csharp
public class BusinessA
{
    public int id;
    public string name;

    public BusinessA(int _id,string _name)
    {
        id = _id;
        name = _name;
    }

    public override bool Equals(object obj)
    {
        if (obj == null) return false;
        BusinessA another = obj as BusinessA;
        if (another != null)
        {
            return id == another.id && name == another.name;
        }
        return false;
    }
}

public class BusinessB
{
    private string describe;
    private string score;

    public BusinessB(string _des,string _score)
    {
        describe = _des;
        score = _score;
    }
}

public class DictionaryDemo : MonoBehaviour
{

    private Dictionary<BusinessA, BusinessB> businessDic = new Dictionary<BusinessA, BusinessB>();

    private BusinessA bA;
    private BusinessB bB;

    private BusinessA bAA;

    void Start()
    {
        int id = 100;
        string name = "zzz";
        //声明两个内部数据一样的对象bA和bAA分别作为存储的key,和查找的key
        bA = new BusinessA(id, name);
        bAA = new BusinessA(id, name);

        //声明value
        bB = new BusinessB("yyy", "100");
        //bA和bB将添加到字典中
        businessDic.Add(bA, bB);

        //使用bAA在字典中查找bB
        BusinessB findB = FindB(bAA);
        BusinessB findB1 = FindB(bA);
        //比较findB 是否等于bB
        Debug.Log(bB == findB);
    }

    public BusinessB FindB(BusinessA a)
    {
        if (businessDic.ContainsKey(a))
        {
            return businessDic[a];
        }
        return null;
    }
    
}
~~~

控制台输出：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240908153057.png)
由此可以，虽然两个对象bA和bAA的内部成员数据相同，但是并没有重写GetHashCode方法，所以这相当于是两个不同哈希值的对象，使用bAA无法找到Value返回null，所以bB不等于findB。
# 解决方案

由此得出解决方案：在使用字典存储键值对时，如果需要将自定义类型作为字典的键，那么该自定义类型应该重写并正确实现GetHashCode方法。

验证：
我们在BusinessA中重写GetHashCode方法：
~~~Csharp
	public override int GetHashCode()
    {
        return string.Format("{0}-{1}", id, name).GetHashCode();
    }
~~~
控制台输出：
![image.png](https://zhouyingwiki-1329003762.cos.ap-guangzhou.myqcloud.com/wiki-pictures/20240908154311.png)

由此可知，虽然bA和bAA是不同的对象引用，但是重写了GetHashCode方法之后，在字典查找时，就能正确匹配对应的key，所以能找出Value，findB和bB相等。

==Equals和 GetHashCode 方法缺一不可。==
# 总结

代码层面出现bug的时候，很多时候还是一些底层的逻辑没有搞懂，平时还是要多测试多验证多了解原理。所以说在使用字典作为存储查询数据结构时还是建议使用**不可变类型作为键**，如何值类型（int、float等）或者常用的引用类型string。如果一定要使用自定义类型作为字典的键，那么应该注意两点：**1.避免在字典操作期间修改键；2.作为键Key的对象需要重写并正确实现Equals和GetHashCode方法**。通过，遵循这些原则，可以避免由于自定义类型对象作为字典键而引起的bug.

