title: Head-First软件设计模式 模板方法模式
date: 2016-01-24 23:48:21
categories: Head-First软件设计模式
tags: Head-First软件设计模式
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g5/M00/02/08/ChMkJ1bKzJuIUnsGABGE6T-ANMkAALI3wCi-7cAEYUB421.jpg)
<!--more-->
模板方法模式

	模板方法模式在一个方法中定义一个算法的骨架，而将一些步骤延迟到子类中。模板方法使得子类可以在不改变算法结构的情况下，重新定义算法中的某些步骤。

设计原则

	好莱坞原则：别调用我们，我们会调用你。

类图
![](http://img0.ph.126.net/eVv0B9mfGTYqtf13zdImsA==/6598294622670484731.jpg)

代码

```java
public abstract class CaffeineBeverage {
    final void prepareRecipe() {
        boilWater();
        brew();
        pourInCup();
        addCondiments();
    }
    abstract void brew();
    abstract void addCondiments();
    void boilWater() {
        System.out.println("Boiling water");
    }
    void pourInCup() {
        System.out.println("Pouring into cup");
    }
}
public class Coffee extends CaffeineBeverage {
    public void brew() {
        System.out.println("Dripping Coffee through filter");
    }
    public void addCondiments() {
        System.out.println("Adding Sugar and Milk");
    }
}
public class Tea extends CaffeineBeverage {
    public void brew() {
        System.out.println("Steeping the tea");
    }
    public void addCondiments() {
        System.out.println("Adding Lemon");
    }
}

```
作业

	某软件公司欲为某银行的业务支撑系统开发一个利息计算模块，利息计算流程如下： 
	(1) 系统根据账号和密码验证用户信息，如果用户信息错误，系统显示出错提示； 
	(2) 如果用户信息正确，则根据用户类型的不同使用不同的利息计算公式计算利息（如活期账户和定期账户具有不同的利息计算公式）； 
	(3) 系统显示利息。 
	试使用模板方法模式设计该利息计算模块。

（1）类图 
![](http://img0.ph.126.net/RQdMd9P2D5JhOGjCpNnwoQ==/6598140691042594158.jpg)

（2）代码
```java
abstract class Account{
    public boool Validate(String account,String password){
        Console.WriteLine("账号：{0}",account);
        Console.WriteLine("密码：{0}",password);
        if (account.Equals("Zhang")&&password.Equals("0"))
            return true;
        else
            return false;
    }
    public abstract void CalculateInterest();
    public void Display(){
        Console.WriteLine("显示利息！");
    }
    public void Handle(String account,String password){
        if (!Validate(account,password)){
            Console.WriteLine("账号或者密码错误！");
            return;
        }
        CalculateInterest();
        Display();
    }
}
class CurrentAccount implements Account{
    public override void CalculateInterest(){
        Consele.WriteLine("按活期利率计算利息！");
    }
}
class SavingAccount implements Account{
    public override void CalculateInterest(){
        Consele.WriteLine("按定期利率计算利息！");
    }
}
```
