# Java

## Fundamental

### 1.基本数据类型和大小

**整形：**int（4字节）,byte（1字节）,short（2字节）,long（8字节）

**浮点型：**float（4字节）,double（8字节）

**字符：**char（2字节）

**布尔值：**boolean

### 2.String可以被继承吗

不能，是被final修饰的（内部的数组也是由final修饰的）

### 3.String，Stringbuffer，StringBuilder的区别

**String：**String当中的字符串是final修饰的，每次处理字符串的时候都会生成新的字符串

**Stringbuffer，StringBuilder：**StringBuffer和StringBuilder的字符串对象是可以修改的，StringBuffer是线程安全的，StringBuilder不是线程安全的

### 4.ArrayList和LinkedList有什么区别

ArrayList底层是数组实现的，LinkedList底层是双向链表实现的

### 5.讲讲类的实例化顺序，比如父类静态数据，构造函数，字段，子类静态数据，构造函数，字段，当new的时候，他们的执行顺序

父类静态变量、 
父类静态代码块、 
子类静态变量、 
子类静态代码块、 
父类非静态变量（父类实例成员变量）、 
父类构造函数、 
子类非静态变量（子类实例成员变量）、 
子类构造函数。 

### 6.用过哪些Map类，都有什么区别，HashMap是线程安全的吗,并发下使用的Map是什么，他们内部原理分别是什么，比如存储方式，hashcode，扩容，默认容量等。

HashMap、HashTable、LinkedHashMap和TreeMap。

#### **HashMap**

根据HashCode值存储数据，访问速度快，最多允许一条记录的键值为Null，线程不安全

jdk1.7 底层实现：数组+链表

jdk1.8的改进：利用红黑树优化，防止Hash冲突时链表长度越来越长使得检索效率降低

![640?wx_fmt=png](https://ss.csdn.net/p?https://mmbiz.qpic.cn/mmbiz_png/QCu849YTaIPf1sDCN5zcDdGsibZwyzy9rc81tfAsDb0FdjzHkBRu4jXRgLco0aDPXQXOqTiamFL9eOtC0g5RuwYw/640?wx_fmt=png)



#### **线程安全的HashMap-ConcurrentHashMap**

jdk1.7 数组+链表：Segment数组，HashEntry

value和链表都是volatile关键字修饰的



#### HashTable

不允许记录的键或者值为空。

支持线程的**同步**，即任一时刻只有一个线程能写Hashtable，因此也导致了 Hashtable在写入时会比较慢。



#### LinkedHashMap

LinkedHashMap **保存了记录的插入顺序**，在用Iterator遍历LinkedHashMap时，先得到的记录肯定是先插入的。在遍历的时候会比HashMap慢，不过有种情况例外，当HashMap容量很大，实际数据较少时，遍历起来可能会比LinkedHashMap慢，因为LinkedHashMap的遍历速度只和实际数据有关，和容量无关，而HashMap的遍历速度和容量有关。

**底层实现：**HashMap+双向链表

**应用：**实现LRU算法



#### TreeMap

TreeMap实现SortMap接口，能够把它保存的记录根据键排序，默认是按键值的升序排序，也可以指定排序的比较器，当用Iterator 遍历TreeMap时，得到的记录是排过序的。

**底层实现：**红黑树



### 7.JAVA8的ConcurrentHashMap为什么放弃了分段锁，有什么问题吗，如果你来设计，你如何设计。

jdk8 放弃了分段锁而是用了Node锁，减低<u>锁的粒度，提高性能</u>，并使用CAS操作来确保Node的一些操作的原子性，取代了锁。

> **CAS：**Compare And Swap
>
> Swap函数已经成为System Call（CPU执行级别）

但是ConcurrentHashMap的一些操作使用了synchronized锁，而不是ReentrantLock,虽然说jdk8的synchronized的性能进行了优化，但是我觉得还是使用ReentrantLock锁能更多的提高性能



### 8.顺序的Map实现类

TreeMap和LinkedHashMap都是有序的

TreeMap底层实现是红黑树，LinkedHashMap底层实现是双向链表



### 9.抽象类和接口类的区别

抽象类继承的时候利用的extends关键字，但是接口的实现使用的是implements实现；

一个类可以实现多个接口，但是只能继承一个类，抽象类也可以实现多个接口，继承实体类；

抽象类可以有构造方法但是接口类不能；

抽象类当中可以有静态方法，但是接口类当中不能；

抽象类当中可以有不抽象的方法，但是接口类当中的方法一定是抽象的；

抽象类可以有普通成员变量但是接口类不能。

### 10.继承和聚合的区别是什么

OO里面继承是描述子类和父类之间的关系，聚合是描述组件与整体部件之间具有不同生命周期的特点

组合描述的生命周期一体的特点。



### 11.IO模型有哪些（NIO,BIO,AIO）

#### Synchronous IO-同步IO

#### 	NIO（Non-Blocking IO）非阻塞式IO

​		访问文件的时候假如内核没有准备好就返回error，不会把进程阻塞

#### 	BIO（Blocking IO）阻塞式IO

​		访问文件的时候假如内核没有准备好就把进程阻塞



#### AIO（Asynchronous IO）异步IO

Synchronous IO的特点：IO的时候进程被阻塞



### 12.反射的原理和创建实例的三种方式

JAVA反射机制是在**运行状态**中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性。这种动态获取的信息以及动态调用对象的方法的功能称为java语言的反射机制。



**Java在计算机当中运行的几个阶段：**

1. **Source阶段**

   javac把java代码编译成.class文件，保存在硬盘中

2. **Class阶段**

   .class文件中的信息转化为class类对象，成员变量Field[]，构造方法Constructor[]，成员方法Method[]

3. **Runtime阶段**

   new方法创建出第二阶段形成的类的实际对象

   

**Class创建实例的三个方法：**

```java
Class.forName("package.class_name");
ClassName.class;
Object.getclass();
```











