---
title: Java基础
date: 2017-10-30 22:01:29
tags: Java
---
# java 基础
--------------------------------
### java 排序

  *  用法
      * Arrays.sort(a)
  * 自定义排序
    * Arrays.sort(a, new MyComparator)

``` java
  import java.util.Arrays;
  import java.util.Comparator;
  class MyComparator implements Comparator{
          public int compare(Object arg0, Object arg1){
                return 1 ,-1, 0
          }
    }

```

--------------
### java中初始化执行顺序
* 在java语言中，静态块在类的加载是就会被调用，因此可以在main()方法执行之前
* 在java语言中，当实例化对象时，对象所在类的所有成员变量首先要进行初始化，只有当
所有的成员变量完成初始化后，才会调用对象所在类的构造函数创建对象。
  * java程序初始化的一般遵循3个原则（优先级递减）：
    * 静态对象（变量）优于非静态对象（变量），
    * 父类优于子类进行初始化
    * 按照定义顺序进行初始化

* java中没有任何方法的接口 也叫标识接口，仅仅是充当标识的作用，java
中已经存在的标识接口有 Cloneable 和 Serializable ，经常用instanceof判断

### java中clone方法的作用
* java处理基本数据类型（例如 int、char、double等）时，都是采用按值传递，除此之外
都是引用，对象除了在函数调用时是引用传递，在使用“=”赋值也是引用传递。
* 浅层复制和深层复制

### java中的反射机制
* 反射机制允许在运行是进行自我检查，也允许对内部的成员进行操作
* 反射机制提供的主要功能有：
  * 得到一个对象所属的的类
  * 获取一个类的所有成员变量和方法
  * 在运行时创建队象
  * 在运行时调用对象的方法
* 在反射机制中，class是一个非常重要的类，有3中方法可以获取class类
  * class.forName("class path")
  * className.class
  * 实例.getClass()
* 实现函数指针功能
  * 可以利用接口和类来实现该功能
  * 具体而言，应先定义一个接口，然后在接口中声明要调用的方法，接着实现这个接口，
  最后把实现的类的一个对象作为参数传递给调用程序，从而实现回调函数的功能。

### 面向对象
* 在java语言中，多态主要有一下两种表现方式：
  * 方法重载（overload）（编译时多态） 。重载是指类中同名方法，但是参数个数不同或者参数类型不同。，
  * 方法覆盖（override）（运行时多态） 。
  * 覆盖的注意一下几点：
      * 派生类中覆盖的方法必须与基类的方法有相同的函数名和参数
      * 返回值必须相同
      * 所抛出的异常必须和基类抛出的异常一致。
      * 基类中被覆盖的方法不能是private，否在子类并没有对其进行覆盖

* 抽象类（abstract class）与接口（interface）的异同
  * 接口中的方法都是抽象的，接口中的成员变量都是 static final
  * 相同点：
    * 都不能实例化
  * 不同点：
    * 接口只有定义，抽象类可以有定义和实现。
    * 接口需要实现（implements），抽像类只能被 extends
    * 接口强调 “has-a”，abstract class ”is-a”
    * 接口中定义的成员变量默认是 public static final，必须赋初值，

### 获取父类的类名
  * getClass().getName()
  * getClass().getSuperClass().getName()

### this 和 super
  * 当子类构造函数需要显示的调用父类的构造函数时，super()必须为构造函数的第一条语句。

### final finally finalize
  * final用于声明属性、方法和类。分别表示属性不可变、方法不可覆盖和类不可被继承。
    * fianl属性，被final修饰的变量不可变。final指的是引用的不可变。
    * final参数 表示参数在函数内部不允许修改。
    * final类 此类不能被继承
  * finally 作为异常处理一部分，表示这段语句最终一定被执行。
  * finalize 是object类的一个方法。在拉及回收器执行时会调用被回收对象的finalize()方法，
  可以以覆盖此方法来实现对其他资源的回收，例如关闭文件等，需要注意，一旦垃圾回收器准
  备好释放对象占用的空间，将首先调用finalize方法，并且在下一次垃圾回收动作才会真正回收占用内存。

### assert 作用
  * assert 作为软件调试的方法。
  * 包括两种表达方式： assert expression1 与 assert expression1：expression2
  其中expression1表示一个boolean表达式，expression2表示一个基本的类型或者对象。

### volatile 作用
  * volatile是一个类型修饰符，被设计用来修饰不同线程访问和修改的变量。

### 实现无符号数的右移
  * java提供了两种右移运算符，“>>”,">>>"。”>>” 有符号右移，“>>>”无符号右移。
  特别注意，在对char、byte、short等类型进行移位前，编译器都会自动将数值转化为int类型。


## 字符串与数组
### 字符串创建与存储的机制
  * 字符串的声明和初始化主要有如下两种情况。
    * String s1 = new String("abc"),String s2 = new String("abc"),
    存在两个对象引用s1,s2.两个内容相同的字符串对象”abc”，它们在内存中的地址是不同的，
    只要使用new总是会生成新的对象。
    * 对于String s1 = “abc”和String s2 = ”abc”，**在jvm中存在一个字符串池**
    其中保存了很多String对象，并且可以被**共享使用**。因此s1和s2引用的是同一个常量池中的对象。
    * new String("abc") 创建几个对象。
    一个或者两个。如果常量池中有abc，则一个。否则创建两个

### "==" equals hashCode 区别
  * “==” 运算符用来比较两个变量的值是否相等。也就是说，该运算符用于比较变量对应的
  的内存中所存储的数值是否相同。要比较两个基本类型的数据或者两个引用变量是否相等，只能使用==运算符
  。对于引用变量，比较的是是否是同一个对象。
  * equals 是 object类提供的方法之一。object中使用的是”==”运算符比较两个对象
  所以没有覆盖equals的情况下，和“==”是一样的。
  String类的equals方法比较的是内容是否相等。
  * hasCode 方法是从object中继承过来的，也用来鉴定两个对象是否相等。object对象
  hashCode方法返回对象在内存中地址转换成int值。所以没有重写hashCode的话，任何对象的
  hashCode都是不等的。

### String StringBuilder StringBuffer StringTokenizer 区别
  * String 字符串修改原理如下：当用String 类型来对字符串修改时，其实现的方法是
  首先创建一个StringBuffer，其次调用StringBuffer的append()方法，最后调用toString方法。
  * StringBuilder与StringBuffer类似。但是StringBuilder不是线程安全的。单线程中StrngBuilder效率会高一些。
  * StringTokenizer是用来分割字符串的工具。

### java 序列化
  * java 提供了两种对象持久化的方式，分别为序列化和外部序列化。

### java平台与内存管理
  * GC垃圾回收，回收程序中不再使用的内存。
  * 垃圾回收器要负责完成3项任务：分配内存、确保被引用对象的内存不被错误的回收以及回收不再被引用的内存空间。
  * 垃圾回收常用算法。
    * 引用计数法
    * 追踪回收法
      * 追踪回收法利用jvm维护的对象引用图，从根节点开始遍历对象的应用图，同时标记遍历到的对象。
    当遍历结束后，未标记的对象就是目前已经不被引用的对象，可以被回收。
    * 压缩回收算法
    * 复制回收算法。
    * 按代价回收算法
  * 可否主动通知jvm进行垃圾回收。
    * 由于垃圾回收器的存在，java语言本身并没有提供显示的释放已分配内存的方法。但是可以通过
    System.gc()方法通知垃圾回收器运行。当然jvm不会保证垃圾回收器马上就会运行。
    System.gc()会停止所有的响应，去检查内存中是否有可回收的对象。不推荐频繁使用。

### java容器
  * set接口 两个实现类 HashSet TreeSet，其中TreeSet实现SortedSet接口，因此TreeSet是有序的。
  * List接口 实现类：LinkedList ArrayList Vector
  * Map接口 实现类 HashMap TreeMap LinkedHashMap WeakHashMap IdentityHashMap
  * 迭代器（Iterator）是一个对象，它的工作是遍历选择序列中的对象。
    * 使用容器的iterator()方法返回一个Iterator，然后通过Iterator的nexxt()方法返回一个元素。
    * 使用Iterator的hasNext()判断容器中是否还有元素。
    * 通过remove()方法删除元素。
  * ArrayList Vector LinkedList区别
    * Vector是线程安全的，ArrayList不是线程安全的，因此vector性能差点。
    * LinkedList是采用双向列表来实现的，随机访问效率低，插入效率高，是非线程安全的。
  * HashMap HashTable TreeMap WeakHashMap区别。
    * HashMap 是 HashTable 的轻量级实现（非线程安全的实现），HashMap空（null）键值（key）
    HashTable不允许。
    * HashMap把HashTable的contains方法去掉，改成containsvalue和containsKey。
    HashTable继承Dictionary类。HashMap是Map的实现。
    * HashTable使用 Enumeration，HashMap使用Iterator。
    * WeakHashMap的key是弱引用方式，只要key不再被外部引用，它就可以被垃圾回收器回收。
  * 自定义类型作为HashMap和HashTable的key
```
HashMap<String,String> hm = new HashMap<String,String>();
Iterator it = hm.entrySet().iterator();
while(it.hasNext()){
    Map.Entry entry = (Map.Entry)it.next();
    String key = (String)entry.getKey();
    String val = (String)entry.getValue();
}
```
### 多线程
  * java使用synchronized关键字来实现同步。实现同步的两种方式：
    * 利用同步代码块来实现同步
    * 利用同步方法来实现同步。
  * java 多线程，一般有以下三种方式。
    * 继承Tread类，重写run()方法
    * 实现Runnable接口，并实现该接口的run()方法。
      * 自定义类并实现Runnable接口，实现run
      * 创建Thread对象，用实现Runnable接口的对象作为参数实例化Thread对象
      * 调用Thread的start()方法。
    * 实现Callable接口，重写call()方法
  * 多线程同步的实现方法有哪些
    * synchronized synchronized关键字有两种用法（synchronize方法和synchronized块），此外该关键字可以
    作用与静态方法，类，某个实例，但是对程序的效率有很大的影响。
    * wait()方法与 notify()方法
    * Lock
  * 终止线程：stop suspend

## 设计模式
  * 单例设计模式
``` java
  public class Test{
      private Test(){}
      private static Test uniqueInstance = new Test();
      public static Test getInstance(){
          return uniqueInstance;
      }
  }
```
  * 工厂设计模式
    * 工厂模式专门负责实例化大量公共接口类。








**************************
