title: Head-First软件设计模式 装饰者模式
date: 2016-01-24 23:37:28
categories: Head-First软件设计模式
tags: Head-First软件设计模式
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g5/M00/02/08/ChMkJlbKzJuIJddqAAUeo0nmp9gAALI3wEVkPsABR67500.jpg)
<!--more-->
装饰者模式

	装饰者模式动态地将责任附加到对象上，若要扩展功能，装饰者提供了比继承更有弹性的替代方案

设计原则

	类应该对扩展开放，对修改关闭

类图

![](http://img1.ph.126.net/AckSsrLeNGrPFV9L-VV29w==/6631418509914040216.jpg)

代码

```java
abstract class Beverage{
    String description = "Unknown Beverage";
    public String getDescription(){
        return description;
    }
    public abstract double cost():
}
abstract class CondimentDecorator extends Beverage {
    public abstract String getDescription();
}
class Espresso extends Beverage {
    public Espresso() {
        description = “Espresso”;
    }
    public double cost() {
        return 1.99;
    }
}
class HouseBlend extends Beverage {
    public HouseBlend() {
        description = “House Blend Coffee”;
    }
    public double cost() {
        return 0.89;
    } 
}
class Mocha extends CondimentDecorator {
    Beverage beverage; // 被包装的beverage
    public Mocha(Beverage beverage) {
        this.beverage = beverage;
    }
    public String getDescription() {
        return beverage.getDescription() + “, Mocha”;
    }
    public double cost() {
        return 0.20 + beverage.cost();
    }
}
class StarbuzzCoffee {
    public static void main(String args[]) {
    Beverage beverage = new Espresso();
    System.out.println(beverage.getDescription() + “$” + beverage.cost());
    Beverage beverage2 = new DarkRoast();
    beverage2 = new Mocha(beverage2);
    beverage2 = new Mocha(beverage2);
    beverage2 = new Whip(beverage2);
    System.out.println(beverage2.getDescription() + “$” + beverage2.cost());
    Beverage beverage3 = new HouseBlend();
    beverage3 = new Soy(beverage3);
    beverage3 = new Mocha(beverage3);
    beverage3 = new Whip(beverage3);
    System.out.println(beverage3.getDescription() + “$” + beverage3.cost());
    }
}

```
