title: Head-First软件设计模式 单件模式
date: 2016-01-24 23:39:35
categories: Head-First软件设计模式
tags: Head-First软件设计模式
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g5/M00/02/08/ChMkJ1bKzJqIJAyrACRdpmtPBAgAALI3wAAAAAAJF2-402.jpg)
<!--more-->
单件模式

	单件模式确保一个类只有一个实例，并提供一个全局访问点。

类图

![](http://img0.ph.126.net/eYxoRwRAWmCd7NStJspXng==/4883590846030472799.jpg)

代码


(1)单线程
```java
public class Singleton{
    private static Singleton uniqueIntance;
    private Singleton(){}
    public static Singleton getInstance(){
        if (uniqueInstance == NULL)
            uniqueInstance = new Singleton();
        return uniqueInstance;
    }
}

```
(2)多线程，把getInstance()变成同步（sychronized）方法。
```java
public class Singleton{
    private static Singleton uniqueInstance;
    private Singleton(){}
    public static synchronized Singleton getInstance(){
        if (uniqueInstance == NULL)
            uniqueInstance = new Singleton();
        return uniqueInstance;
    }
}
```
(3)多线程，在静态初始化中创建单件。
```java
public class Singleton{
    private static Singleton uniqueIntance = new Singleton();
    private Singleton(){}
    public static Singleton getInstance(){
        return uniqueInstance;
    }
}
```
(4)多线程，用“双重检查加锁”，在getInstance()中减少使用同步。
```java
public class Singleton{
    private volatile static Singleton uniqueInstance;
    private Singleton(){}
    public static Singleton getInstance(){
        if (uniqueInstance == NULL){
            synchronized (Singleton.class){
                if (uniqueInstance == NULL){
                    uniqueInstance = new Singleton();
                }
            }
        }
        return uniqueInstance;
    }
}
```
