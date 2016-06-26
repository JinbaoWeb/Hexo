title: Head-First软件设计模式 策略模式
date: 2016-01-24 23:25:59
categories: Head-First软件设计模式
tags: Head-First软件设计模式
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g1/M09/01/0F/Cg-4jlSKTnuIdPRUABESoqIBpXUAAO1OAKtKVgAERK6840.jpg)
<!--more-->
策略模式


	策略模式定义了算法族，分别封装起来，让它们之间可以互相替换，此模式让算法的变化独立于使用算法的客户

设计原则

	多用组合，少用继承

	针对接口编程，而不是针对实现编程

	找出应用中可能需要变化之处，把它们独立出来，不要和那些不需要变化的代码混在一起

类图

![](http://img2.ph.126.net/gf4hafSMKWb61PY0LfSSIQ==/6631243687565219156.jpg)

代码

```java
/*TestDuck.java*/
interface FlyBehavior{
    public void fly();
}
class FlyWithWings implements FlyBehavior{
    public void fly(){
        System.out.println("I'm flying!");
    }
}
class FlyNoWay implements FlyBehavior{
    public void fly(){
        System.out.println("I can't fly!");
    }
}
interface QuackBehavior{
    public void quack();
}
class Quack implements QuackBehavior{
    public void quack(){
        System.out.println("Quack!");
    }
}
class MuteQuack implements QuackBehavior{
    public void quack(){
        System.out.println("Silence!");
    }
}
class Squeak implements QuackBehavior{
    public void quack(){
        System.out.println("Squeak!");
    }
}
abstract class Duck {
    FlyBehavior flyBehavior;
    QuackBehavior quackBehavior;
    public Duck() {}
    abstract void display();
    public void performFly() {
        flyBehavior.fly();
    }
    public void performQuack() {
        quackBehavior.quack();
    } 
    public void swim() {
        System.out.println("All ducks float, even decoys!");
    }
}
class MallardDuck extends Duck{
    public MallardDuck(){
        quackBehavior = new Quack();
        flyBehavior = new FlyWithWings();
    }
    public void display(){
        System.out.println("I'm a real Mallard duck!");
    }
}
public class TestDuck{
    public static void main(String[] args){
        Duck mallard = new MallardDuck();
        mallard.performQuack();
        mallard.performFly();
    }
}

```

练习题

	某电影院售票系统为不同类型的用户提供不同打折方式（Discount），学生凭学生证享受8折优惠（StudentDiscount），
	儿童享受减免10元优惠（ChildrenDiscount），VIP用户除享受半价优惠还可积分（VIPDiscount）。

参考代码：

```java
/*Client.java*/
interface Discount{
    public double calculate(double price);       
}
class StudentDiscrount implements Discount{
    public double calculate(double price){   
        return price*0.8;  
    }
}
class ChildrenDiscrount implements Discount{
    public double calculate(double price){   
        return price-10;   
    }
}
class VIPDiscrount implements Discount{
    public double calculate(double price){   
        System.out.println("增加积分!");
        return price*0.5;
    }
}
class MovieTicket{     
    private double price;
    private Discount discount;
    public void setPrice(double price){    
        this.price=price;  
    }
    public void setDiscount(Discount discount){
        this.discount=  discount;
    }
    public double getPrice(){ 
        return discount.calculate(price);
    }
}
class Client{      
    public static void main(String args[]){
        MovieTicket mt = new MovieTicket();
        mt.setPrice(50);
        double currentPrice;
        Discount obj;
        obj = new StudentDiscrount();
        mt.setDiscount(obj);
        currentPrice = mt.getPrice();
        System.out.println("折后价："+currentPrice);
        obj = new VIPDiscrount();
        mt.setDiscount(obj);
        currentPrice = mt.getPrice();
        System.out.println("折后价："+currentPrice);
    }
}
```
