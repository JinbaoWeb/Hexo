title: Head-First软件设计模式 适配器模式和外观模式
date: 2016-01-24 23:44:28
categories: Head-First软件设计模式
tags: Head-First软件设计模式
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g5/M00/02/08/ChMkJ1bKzJuIF5JgACBFEJARCe4AALI3wDGUyEAIEUo607.jpg)
<!--more-->
适配器模式和外观模式

	适配器模式将一个类的接口，转换成客户期望的另一个接口。适配器让原本接口不兼容的类可以合作无间。 

	外观模式提供了一个统一的接口，用来访问子系统中的一群接口。外观定义了一个高层接口，让子系统更容易使用。

设计原则

	最少知识原则：一个对象应当对其他对象有尽可能少的了解,不和陌生人说话。

类图
![](http://img0.ph.126.net/Nw9uLHxncc2spUJtVAvtVw==/6598105506670509852.jpg)


代码
```java
public interface Duck {
    public void quack();
    public void fly();
}
public interface Turkey {
    public void gobble();
    public void fly();
}
public class MallardDuck implements Duck {
    public void quack() {System.out.println("Quack");}
    public void fly() {System.out.println("I'm flying");}
}
public class WildTurkey implements Turkey {
    public void gobble() {System.out.println("Gobble gobble");}
    public void fly() {System.out.println("I'm flying a short distance");}
}
public class TurkeyAdapter implements Duck {
    Turkey turkey;
    public TurkeyAdapter(Turkey turkey) {
        this.turkey = turkey;
    }    
    public void quack() {
        turkey.gobble();
    }
    public void fly() {
        for(int i=0; i < 5; i++) {
            turkey.fly();
        }
    }
}
public class DuckTestDrive {
    public static void main(String[] args) {
        MallardDuck duck = new MallardDuck();
        WildTurkey turkey = new WildTurkey();
        Duck turkeyAdapter = new TurkeyAdapter(turkey);
        System.out.println("The Turkey says...");
        turkey.gobble();
        turkey.fly();
        System.out.println("\nThe Duck says...");
        testDuck(duck);
        System.out.println("\nThe TurkeyAdapter says...");
        testDuck(turkeyAdapter);
    }
    static void testDuck(Duck duck) {
        duck.quack();
        duck.fly();
    }
}

```
```java
class HomeTheaterFacade{
    Amplifier amp;
    Tuner tuner;
    DvdPlayer dvd;
    CdPlayer cd;
    Projector projector;
    TheaterLights lights;
    Screen screen;
    PopcornPopper popper;
    public HomeTheaterFacade(Amplifier amp,Tuner tuner,DvdPlayer dvd,CdPlayer cd,Projector projector,TheaterLights lights,Screen screen,PopcornPopper popper){
        this.amp=amp;
        this.tuner=tuner;
        this.dvd=dvd;
        this.cd=cd;
        this.projector=projector;
        this.lights=lights;
        this.screen=screen;
        this.popper=popper;
    }
    public void watchMovie(String movie) {
        System.out.println("Get ready to watch a movie...");
        popper.on();
        popper.pop();
        lights.dim(10);
        screen.down();
        projector.on();
        projector.wideScreenMode();
        amp.on();
        amp.setDvd(dvd);
        amp.setSurroundSound();
        amp.setVolume(5);
        dvd.on();
        dvd.play(movie);
    }
    public void endMovid(){
        System.out.println("Shutting movie theater down ...");
        popper.off();
        lights.on();
        screen.up();
        projector.off();
        amp.off();
        dvd.stop();
        dvd.eject();
        dvd.off();
    }
}
public class HomeTheaterTestDrive {
    public static void main(String[] args) {
        Amplifier amp = new Amplifier("Top-O-Line Amplifier");
        Tuner tuner = new Tuner("Top-O-Line AM/FM Tuner", amp);
        DvdPlayer dvd = new DvdPlayer("Top-O-Line DVD Player", amp);
        CdPlayer cd = new CdPlayer("Top-O-Line CD Player", amp);
        Projector projector = new Projector("Top-O-Line Projector", dvd);
        TheaterLights lights = new TheaterLights("Theater Ceiling Lights");
        Screen screen = new Screen("Theater Screen");
        PopcornPopper popper = new PopcornPopper("Popcorn Popper");
        HomeTheaterFacade homeTheater = new HomeTheaterFacade(amp, tuner, dvd, cd, projector, homeTheater.watchMovie("Raiders of the Lost Ark");
            homeTheater.endMovie();
    }
}
```

作业

	现有一个接口DataOperation定义了排序方法sort(int [])， 和
	查找方法search(int [],int)，已知类QuickSort的quickSort(int [])
	方法实现了快速排序算法，类BinarySearch的binarySearch(int [], int)
	方法实现了二分查找算法，现使用适配器模式设计一个系统，在不修改源代码的情况下将类QuickSort和类BinarySearch的方法适配
	到DataOperation接口中。绘制类图。

（1）类图 
![](http://img0.ph.126.net/eHuwydoyKkRPipHKvd0eYw==/6631275573402428604.jpg)

（2）代码

```java
class OperationAdapter implements DataOperation{
    private QuickSort sortObj;
    private BinarySearch searchObj;
    public OperationAdapter(QuickSort sortObj,BinarySearch searchObj){
        this.sortObj = sortObj;
        this.searchObj = searchObj;
    }
    public int[] sort(int array[]){
        return sortObj.quickSort(array);
    }
    public int search(int array[],int key){
        return serchObj.binarySearch(array,key);
    }
}
class Client{
    public static void main(String[] args){
        DataOperation operation;
        QuickSort sortObj = new QuickSort();
        BinarySearch searchObj = new BinarySearch();
        operation = new OperationAdapter(sortObj,searchObj);
        int array[] = {13,24,15,36,26,17,68,34};
        int result[];
        int value;
        System.out.println("排序结果：")
        result = operation.sort(array);
        for (int i:array){
            System.out.print(i+",");
        }
        System.out.println();
        System.out.println("查找关键字24：");
        value = operation.search(result,24);
        if (value!=-1){
            System.out.println("找到关键字24.");
        }
        else{
            System.out.println("没有找到关键字24.");
        }
    }
}
```
