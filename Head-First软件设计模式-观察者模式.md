title: Head-First软件设计模式 观察者模式
date: 2016-01-24 23:32:31
categories: Head-First软件设计模式
tags: Head-First软件设计模式
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g5/M00/02/08/ChMkJlbKzJqIXrX6AA4U3rvQVe0AALI3wCATo4ADhT2375.jpg)
<!--more-->
观察者模式

	观察者模式定义了对象之间的一对多依赖，这样一来，当一个对象改变状态是，它的所有依赖者都会收到通知并更新。

设计原则

	为了交互对象之间的松耦合设计而努力

	找出程序中会变化的方面，然后将其和固定不变的方面相分离

	针对接口编程，不针对实现编程

	多用组合，少用继承

类图

![](http://img1.ph.126.net/-n5PfDYZUI6DsG6rJtTwYA==/4857413673196411534.jpg)

代码

```java
import java.util.ArrayList;
interface Subject {
    public void registerObserver(Observer o);
    public void removeObserver(Observer o);
    public void notifyObservers();
}
interface Observer {
    public void update(float temp, float humidity, float pressure);
}
interface DisplayElement{
    public void display();
}
class WeatherData implements Subject {
    private ArrayList observers;
    private float temperature, humidity, pressure;
    public WeatherData(){  
        observers = new ArrayList();  
    }
    public void registerObserver(Observer o){
        observers.add(o);
    }
    public void removeObserver(Observer o){
        int i = observers.indexOf(o);
        if (i >= 0) {observers.remove(i);}
    }
    public void notifyObservers() {
        for (int i = 0; i < observers.size(); i++) {
            Observer observer = (Observer)observers.get(i);
            observer.update(temperature, humidity, pressure);
        }
    }
    public void measurementsChanged(){
        notifyObservers();
    }
    public void setMeasurements(float temperature,float humidity,float pressure){
        this.temperature=temperature;
        this.humidity=humidity;
        this.pressure=pressure;
        measurementsChanged();
    }
}
class CurrentConditionsDisplay implements Observer,DisplayElement{
    private float temperature;
    private float humidity;
    private Subject weatherData;
    public CurrentConditionsDisplay(Subject weatherData) {
        this.weatherData = weatherData;
        weatherData.registerObserver(this);
    }
    public void update(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        display();
    }
    public void display() {
        System.out.println("Current conditions: " + temperature + "F degrees and " + humidity + "% humidity");
    }
}
public class WeatherStation {
    public static void main(String[] args) {
        WeatherData weatherData = new WeatherData();
        CurrentConditionsDisplay currentDisplay = new CurrentConditionsDisplay(weatherData);
        weatherData.setMeasurements(80, 65, 30.4f);
        weatherData.setMeasurements(82, 70, 29.2f);
        weatherData.setMeasurements(78, 90, 29.2f);
    }
}

```
练习题

	一个电子商务系统，当一个新的消费用户加入系统，希望做以下两个操作：1.向消费者发送一封欢迎邮件 2.向邮局查证消费者地址

参考解答 

（1）类图：
![](http://img2.ph.126.net/_emwBOSqmjcfVLzBdlmEOw==/6598282528042579199.jpg)
（2）代码：
```java
import java.util.ArrayList;
interface Subject{
    public void Attach(Observer o);
    public void Detach(Observer o);
    public void Notify();
}
interface Observer{
    public void update(Customer customer);
}
class Customer implements Subject{
    private ArrayList observers;
    private String customerInfo;
    public Customer(){
        observers = new ArrayList();
    }
    public void Attach(Observer o){
        observers.add(o);
        Notify();
    }
    public void Detach(Observer o){
        observer.remove(o);
    }
    public String getCustomerInfo(){
        return customerInfo;
    }
    public String setCustomerInfo(String customerInfo){
        this.customerInfo = customerInfo;
    }
    public void Notify(){
        for (int i=0;i<observers.size();i++){
            Observer observer=(Observer)observer.get(i);
            observer.update(this);
        }
    }
}
class WelcomLetter implements Observer{
    private String customerInfo;
    public void update(Customer customer){
        this.customerInfo = customer.customerInfo;
        Display();
    }
    pubilic void Display(){
        System.out.println("Welcom!");
    }
}
class AddrVerfication implements Observer{
    private String customerInfo;
    public void update(Customer customer){
        this.customerInfo = customer.customerInfo;
        Display();
    }
    public void Display(){
        System.out.println("Query!");
    }
}
public class TestClient{
    public static void main(String[] args){
        Customer customer = new Customer();
        WelcomLetter welcomLetter = new WelcomLetter(customer);
        AddrVerfication addrVerfication = new AddrVerfication(customer);
        customer.setCustomerInfo("LiMing");
    }
}
```

	某在线股票软件需要提供以下功能：当股票购买者所购买的某支股票
	价格变化幅度达到5%时，系统将自动发送通知（包括新价格）给购买
	该股票的股民。现使用观察者模式设计该系统，绘制类图并编程模拟实现。

参考解答 

（1）类图： 
![](http://img1.ph.126.net/VqT800rC2G6-fqjdJhcdHQ==/6598182472484449657.jpg)

（2）代码：

```java
import java.util.*;
interface Investor{
    public void response(Stock stock);
}
class Stock{
    private ArrayList inverstors;
    private String stockName;
    private double price;
    public Stock(String stockName,double price){
        this.stockName = stockName;
        this.price = price;
        inverstors = new ArrayList();
    }
    public void Attach(Investor invertor){
        invertors.add(investor);
    }
    public void Detach(Investor invertor){
        invertors.remove(invertor);
    }
    public void setStockName(String stockName){
        this.stockName = stockName;
    }
    public String getStockName(){
        return this.sotckName;
    }
    public void setPrice(double price){
        double range = Math.abs(price-this.price)/this.price;
        this.price = price;
        if (range>=0.05){
            this.notifyInvestor();
        }
    }
    public double getPrice(){
        return this.price;
    }
    public void notifyInvestor(){
        for (Object obj:invertors){
            ((Investor)obj).response(this);
        }
    }
}
class ConcreteInvertor implements Investor{
    private String name;
    public ConcreteInvertor(String name){
        this.name=name;
    }
    public void response(Stock stock){
        System.out.print("提升股民："+name);
        System.out.print("-----股票："+stock.getStockName());
        System.out.print("价格波动幅度超过5%-----");
        System.out.println("新价格是："+stock.getPrice());
    }
}
publci TestClient{
    public static void main(String[] args){
        Invertor invertor1,invertor2;
        inverstor1 = new ConcreInvestor("ZhangSan");
        inverstor2 = new ConcreInvestor("LiSi");
        Stock haier = new Stock("Haier",20.00);
        haier.attach(inverstor1);
        haier.attach(inverstor2);
        haier.setPrice(25.00);
    }
}
```
	



