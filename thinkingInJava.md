---
title: thinking In Java Notes
date: 2020-05-15 15:32:03
tags:
	-java
keywords:
cover: https://cdn.jsdelivr.net/gh/Eastwood6/Eastwood6.github.io@master/img/https.jpg
abbrlink:
top_img: https://cdn.jsdelivr.net/gh/Eastwood6/Eastwood6.github.io@master/img/TB10Vh7SpXXXXbZaFXXXXXXXXXX-2880-1080.jpg
---

[TOC]
## Introduction to Objects 
## Everything Is an Object 
## Operators
## Controlling Execution 
## Initialization & Cleanup 
**constructor：没有写constructor有默认constructor，写了没有默认constructor**
- 访问static final constant(compile-time constant) ,that value can be read without causing the Initable class to be initialized.但是static field还是会的
>If a static field is not final, accessing it always requires linking (to allocate storage for the field) and initialization (to initialize that storage) before it can be read 



## Access Control 
## Reusing Classes 
## Polymorphism 

---
## Interfaces 
---
抽象类里的抽象方法可以逼迫子类重写抽象方法

## Inner Classes ***

- 外部类无法调用内部类资源,反过来可以

---
## Holding Your Objects ***

- Linklist
 linklist.getfirst(),element(),peek(),get the first element,
   while remove(),removeFirst(),poll() get and remove the first element
  addFirst() add to the first position,
  while offer() and add() add to the last position

- Arraylist
 B<Pet> b = A.subList(x,y); b所做的改变对A有影响

collection<T a>.toArray(T[] a)，返回的数组类型必须是T，没有泛型是object


- Utility(Collections and Arrays)
1. Collections
Collections.addAll( )比collection(Collections c) more quicker,and flexible

2. Arrays
Arrays.asList() notes :
1、Arrays.asList()不要乱用，底层其实还是数组。
2、如果使用了Arrays.asList()的话，最好不要使用其集合的操作方法。
3、List list = new ArrayList<>(Arrays.asList("a", "b", "c"))可以在外面这样包一层真正的ArrayList。

---


## Error Handling with Exceptions *
---
捕捉了异常会继续往后走，靠系统捕捉不往后走

## Strings ***
- Immutable Strings ............355
`toUpperCase()`
通过jdk可以看到,String的**类方法**对original String object做的修改(original的引用)会保存到新的String object，original String object不变

- Overloading ‘+’ vs.StringBuilder ................. 356

1、在循环和多个表达式中不能 +，频繁创建 SB 性能影响；
2、在单个表达式中可以用 +，编译器直接做了优化；

If you try to take shortcuts and do something like append(a + ": " + c), the compiler will jump in and start making more StringBuilder objects again.
**StringBuilder**

1. operation：
跟数组一样，按下标读数
`insert( ), replace( ), substring( ) and even reverse( )`
```
StringBuilder sb = new StringBuilder(); 
sb.delete(int x.int y); (x：inclusive,y：exlusive)
```
2. StringBuilder vs Stringbuffer
Java used StringBuffer, which ensured thread safety  and so was significantly more expensive. but, StringBuffer operations is faster.
3. notes:
<1> If you try to take shortcuts and do something like append(a + ": " + c), the compiler will jump in and start making more StringBuilder objects again.
<2> 在循环和多个表达式中不能 +，频繁创建 SB 性能影响；
<3> 在单个表达式中可以用 +，编译器直接做了优化；

- Unintended recursion ....... 359
**toString() print address**
If you really do want to print the address of the object, the solution is to call the ObjecttoString( ) method, which does just that. So instead of saying this, you'd say super.toString( ).

- Operations on Strings ....... 361

- Formatting output ............. 362
    printf() .................................... 363
    System.out.format() ............ 363
    The Formatter class ............... 363
    Format specifiers ...................... 364
    Formatter conversions ........... 366
    String.format() ..................... 368

- Regular expressions ........... 370
  
    Basics .........................................370 
    Creating regular expressions ..... 372
    Quantifiers ................................. 374
    Pattern and Matcher ............. 375
    split() ........................................382
    Replace operations .................... 383
    reset() .......................................384
    Regular expressions and Java I/O .............................. 385
- Scanning input ................... 386
  
   Scanner delimiters ................. 388
    Scanning with regular expressions ................... 389
- StringTokenizer ............. 389

## Type Information ***
 - [x] done 

- 获取class reference:
1.有该对象，object.getClass();
2.没有该对象，Class.forName("name")(初始化)/X.class(不初始化)
- class reference转Object:
`class.getInstance()`(要有默认构造器)

- 类加载机制:
java会为每一个class创建一个.class文件，当你创建它的对象时，JVM class loader 处理你的程序；当你调用它的static member,所有的class都会被动态加载到JVM里(构造方法也是static，因此new 一个对象作为调用static member)

---
- The need for RTTI .............. 393 
Java allows you to discover information about objects and classes at run time,This takes two forms: "traditional" RTTI and Reflection
- The Class object ................ 395 
**RTTI 原理**：
1.each time you write and compile a new class, a single Class object is also created (and stored, appropriately enough, in an identically named .class file).JVM class loader help you make an object of that class

2. All classes are loaded into the JVM dynamically, upon the first use of a class.This happens when the program makes the first reference to a static member of that class.
**生成并编译一个类时，会生成Class object，并生成并保存至.calss file,when the program makes the first reference to a static member of that class（the constructor is also a static method），JVM会用class loader加载所有的class file，并找到对应的Class object,进而create type information,and the static initialization is performed upon class loading.** 

**Get a reference to the Class object**:

1.  the static forName( ) method,
`Class.forName()`  class loading,everywhere!!!(if you dont have the object of that type)
2. the class literal:`FancyToy.class;` no class loading,Class literals work with regular classes as well as interfaces, arrays, and primitive types.TYPE that exists for each of the primitive wrapper classes.
3. `object.getClass()` no class loading(if you have the object of that type)

`Object o=Class.forInstance();` class transfer to object(you must have that object's default constructor)
Class literals ............................... 399 
**Initialization**:
eg:InitializeTest
Initialization is delayed until the first reference to a static method (the constructor is implicitly static) or to a non-compile-time constant static field

**newInstance()**:
In any event, because of the vagueness, the return value of up.newlnstance( )is not a precise type, but just an Object.

Generic class references ............ 401 

New cast syntax ........................ 403 
**class.cast(object)**:
```
Building b = new House(); 
Class<House> houseType = House.class; 
House h = houseType.cast(b); 
h = (House)b; // ... or just do this. 
```
- Checking before a cast ....... 404 
**forms of RTTI**:
1.The classic cast; e.g., "(Shape)," which uses RTTI to make sure the cast is correct.
This will throw a ClassCastException if you抳e performed a bad cast.
2.The Class object representing the type of your object. The Class object can be queried for useful runtime information.
3.This is the keyword instanceof, It’s important to use instanceof before a downcast when you don’t have other information that tells you the type of the object 


Using class literals .................... 409 

A dynamic instanceof .............. 411 

Counting recursively .................. 412 

- Registered factories ........... 413 
 the Factory Method design pattern 
`public interface Factory<T> { T create(); } `
- instanceof vs. Class equivalence......................... 416 
`obj instanceof ClassName` ask is ClassName yourself(true) or your farther
`class.isInstance(obj)`ask is obj yourself(true) or your son 
`A.getclass()==A.class/A.getclass().equals(A.class) ` both true
- Reflection: runtime  class information ................ 417 
**exist reason**
1. component-based programming ,in which you build projects using Rapid Application Development in IDE
2. RMI(remote method invocation):provide the ability to create and excute objects on remote platforms
3. can access every method,filed,even in innerclass,annoymous innerclass and private;
**difference between RTTI and reflection**:
RTTI:
the compiler opens and examines the .class file at compile time.
reflection:
the .class file is unavailable at compile time; it is opened and examined by the runtime environment.

A class method extractor ........... 418 
**regex utilize**:
`Pattern p = Pattern.compile("\\w+\\.|native\\s|final\\s");`
` p.matcher(method.toString()).replaceAll(""));`strips off the name qualifiers using regular expression
- Dynamic proxies ................ 420 
proxy design pattern p420
A proxy can be helpful anytime you’d like to separate extra operations into a different place than the "real object

- Null Objects ........................ 424 
**Null Objects function**:
可以利用null obeject做成假数据
>The place where Null Objects seem to be most useful is "closer to the data," with objects that represent entities in the problem space.

eg:Person里的内部类NullPerson，NULL字段，补充Position里的空职位
Mock Objects & Stubs ................ 429 

- Interfaces and type information ................ 430 
`Father s=new Son();`//s只能调用Father的资源，除非(Son)s(Son有访问权限)

**class methods**
`getClass().getClassLoader(); `
`getClass().getName()/getSimpleName()); `
`c.get***()`
`c.is***()`
**get and invoke method**
```
Method g=class.getDeclaredMethod(methodName)
g.setAccessible(true);
g.invoke(a);
```
**get and set field**
```
WithPrivateFinalField pf = new WithPrivateFinalField(); 

Field f=getClass().getDeclaredField("s2") (详见GetFieldTest)
f.setAccessible(true); 
f.set(pf, "No, you’re not!"); 
```


## Generics
<? extends T>
<? super  T>
## Arrays ***
- 填充数组方法：
1. 填充同一类型(Arrays):
`public static void fill(Object[] a, Object val)`
2. 填充指定类型
填充数组是基于填充容器
` Generated.array(T[] a, Generator<T> gen)`

- six basic static utility methods :
equals(),fill(),sort(),binarySearch(),toString(),hashCode()
1. equals()判断 数组的长度及每个元素是否相等(Object.equals())

2. sort() 数组排序一种是默认排序(字典序)，一种是自定义
自定义排序：
有一个数组A[x],一般是用Arrays.sort(A[] a),A这个类必须实现Comparable重写compareTo(A a1);
```
int compareTo(A a1){
return (i < a1.i ? -1 : (i == a1.i ? 0 : 1));
}(-1正序，1倒序)
```
也可以用Arrays.sort(A[] a，Collections.reverseOrder() )倒序

也可以用Arrays.sort(A[] a，Comparator c) Comparator子类来自定义哪个字段排序，重写的compare()方法语法与compareTo(）一样

在对String排序时，String.CASE_INSENSITIVE_ORDER 可忽略大小写



---
## Containers in Depth ***
- 填充容器方法：
1.填充同一类型(工具类Collections)：
```
Collections:
public static <T> List<T> nCopies(int n, T o)
public static <T> void fill(List<? super T> list, T obj)

```
 2.填充指定类型((既可以自定义也可以用RandomGenerator或CountingGenerator,RandomGenerator等工具类)因为几乎所有Collection的构造方法都有一个Collection参数来对其初始化
 ```
 new Container(new CollectionData/CollectionData.list(Object o(? extend Genetator),int num)) 
 ```

---

## I/O ***
## Enumerated Types 
## Annotations
## Concurrency ***  
- [x] done 
#### Basic threading
---
- Excutors
1. shutdown()，shutdownNow()区别
shutdown()有序关闭之前提交的任务，不关闭新的任务
shutdownNow()关闭所有正在执行的任务，尝试用interrupt关闭，
thread.interrupted()判断(without throwing an exception.)，sleep()的InterruptedException catch,wait()的InterruptedException catch等都可以结束，如果没有这些判断或catch InterruptedException,无法结束(详见JDK)

>typical  implementations will cancel via {@link Thread#interrupt}, so any task that fails to respond to interrupts may never terminat

- Daemon threads
设置thread deamon两种方式：threadfactory和thread.setDeamon(true)(before thread.start())

- Joining a thread 
thread.join()：A.join()指先等A走完

#### Sharing resources: 
- Atomicity and volatility
 >p854
 >
 > **one object one lock**
#### Terminating tasks
- Thread.currentThread().isInterrupted()用作判断，不改变thread status,而Thread.interrupted()用作termination,改变thread status

#### Cooperation between tasks 
- wait(),notify(),notifyAll()
    1    in fact,wait(),notify(),notifyAll() are only used in synchronized methods or block,or it will throw IllegalMonitorStateException
        
        Class x{
        otherObject ob=new otherObject();
        synchronized(ob){
        wait()}
        }(synchronized object与调用wait的object不一致也会抛IllegalMonitorStateException)
    
    
    ​    
    2   wait() will suspend this task and release the lock,only when notify/notifyall() being called,and this task reacquire the lock it released in wait(),can it be be waken.btw,方法走完也会释放锁
    3   wait()需要用同一object的notify()/notifyAll()才能唤醒

---
[TOC]

---
附录：
- net.mindview.util包： 
ConvertTo.primitive(primitive[] p)将primitive数组转成wrapper数组

---

issues:
MapData.map

notes:

-  design pattern:
1. the factory Method design pattern 
`public interface Factory<T> { T create(); } `
2. proxy design pattern:
p420
A proxy can be helpful anytime you’d like to separate extra operations into a different place than the "real object


- static final 与final区别:
两者都修饰的是常量，一个是静态，一个不是


**这本书练习题及特别是答案涉及很多知识，特别不错**
在从前往后看时，先看的是中文版，到Containers in Depth才开始英文版
刚开始看英文版的时候没有一字一句看(1)，是抱着试看的态度，再加上每章看完没有提炼总结知识点(目录(1)需要记忆的(2))与难点(3)，现在回过头来虽然有点后悔，但是毕竟是第一本用心看的书(1)加上英文书(2)。

done的说明看过英文版