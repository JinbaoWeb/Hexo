title: Head-First软件设计模式 命令模式
date: 2016-01-24 23:42:11
categories: Head-First软件设计模式
tags: Head-First软件设计模式
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g5/M00/02/08/ChMkJlbKzJuILKr6AAaywKjnC88AALI3wCazx8ABrLY000.jpg)
<!--more-->
命令模式

	命令模式将“请求”封装成对象，以便使用不同的请求、队列或者日志来参数化其他对象。命令模式也支持可撤销的操作。

类图
![](http://img2.ph.126.net/_WCpqbNiRS6Y4hOtTW6ncg==/6598068123275343731.jpg)


代码
```java
public interface Command{
    public void execute();
}
public class LightOnCommand implements Command {
    Light light;
    public LightOnCommand(Light light) {
        this.light = light;
    }
    public void execute() {
        light.on();
    }
}
public class SimpleRemoteControl {
    Command slot;
    public SimpleRemoteControl() {}
    public void setCommand(Command command) {
        slot = command;
    }
    public void buttonWasPressed() {
        slot.execute();
    }
}
public class RemoteControlTest {
    public static void main(String[] args) {
        SimpleRemoteControl remote = new SimpleRemoteControl();
        Light light = new Light();
        LightOnCommand lightOn = new LightOnCommand(light);
        remote.setCommand(lightOn);
        remote.buttonWasPressed();
    }
}
public interface Command{
    public void execute();
}
public class LightOnCommand implements Command {
    Light light;
    public LightOnCommand(Light light) {
        this.light = light;
    } 
    public void execute() {
        light.on();
    }
}
public class LightOffCommand implements Command {
    Light light;
    public LightOffCommand(Light light) {
        this.light = light;
    } 
    public void execute() {
        light.off();
    }
}
public class StereoOnWithCDCommand implements Command {
    Stereo stereo;
    public StereoOnWithCDCommand(Stereo stereo) {
        this.stereo = stereo;
    } 
    public void execute() {
        stereo.on();
        stereo.setCD();
        stereo.setVolume(11);
    }
}
public class RemoteControl {
    Command[] onCommands;
    Command[] offCommands;
    public RemoteControl() {
        onCommands = new Command[7];
        offCommands = new Command[7];
        Command noCommand = new NoCommand();
        for (int i = 0; i < 7; i++) {
            onCommands[i] = noCommand;
            offCommands[i] = noCommand;
        }
    } 
    public void setCommand(int slot, Command onCommand,  Command offCommand) {
        onCommands[slot] = onCommand;
        offCommands[slot] = offCommand;
    }
    public void onButtonWasPushed(int slot) {
        onCommands[slot].execute();
    }
    public void offButtonWasPushed(int slot) {
        offCommands[slot].execute();
    }
    public String toString() {
        StringBuffer stringBuff = new StringBuffer();
        stringBuff.append("\n------ Remote Control -------\n");
        for (int i = 0; i < onCommands.length; i++) {
            stringBuff.append("[slot " + i + "] " + onCommands[i].getClass().getName() + "    " + offCommands[i].getClass().getName() + "\n");
        }
        return stringBuff.toString();
    }
}
public class RemoteLoader {
    public static void main(String[] args) {
        RemoteControl remoteControl = new RemoteControl();
        Light livingRoomLight = new Light("Living Room");
        Light kitchenLight = new Light("Kitchen");
        CeilingFan ceilingFan= new CeilingFan("Living Room");
        GarageDoor garageDoor = new GarageDoor("");
        Stereo stereo = new Stereo("Living Room");
        LightOnCommand livingRoomLightOn = new LightOnCommand(livingRoomLight);
        LightOffCommand livingRoomLightOff = new LightOffCommand(livingRoomLight);
        LightOnCommand kitchenLightOn = new LightOnCommand(kitchenLight);
        LightOffCommand kitchenLightOff = new LightOffCommand(kitchenLight);
        CeilingFanOnCommand ceilingFanOn = new CeilingFanOnCommand(ceilingFan);
        CeilingFanOffCommand ceilingFanOff = new CeilingFanOffCommand(ceilingFan);
        GarageDoorUpCommand garageDoorUp = new GarageDoorUpCommand(garageDoor);
        GarageDoorDownCommand garageDoorDown = new GarageDoorDownCommand(garageDoor);
        StereoOnWithCDCommand stereoOnWithCD = new StereoOnWithCDCommand(stereo);
        StereoOffCommand  stereoOff = new StereoOffCommand(stereo);
        remoteControl.setCommand(0, livingRoomLightOn, livingRoomLightOff);
        remoteControl.setCommand(1, kitchenLightOn, kitchenLightOff);
        remoteControl.setCommand(2, ceilingFanOn, ceilingFanOff);
        remoteControl.setCommand(3, stereoOnWithCD, stereoOff);
        System.out.println(remoteControl);
        remoteControl.onButtonWasPushed(0);
        remoteControl.offButtonWasPushed(0);
        remoteControl.onButtonWasPushed(1);
        remoteControl.offButtonWasPushed(1);
        remoteControl.onButtonWasPushed(2);
        remoteControl.offButtonWasPushed(2);
        remoteControl.onButtonWasPushed(3);
        remoteControl.offButtonWasPushed(3); 
    } 
}

```
作业

	使用命令模式进行计算器计算，可以是加减乘除等运算，可以进行多层的Undo和Redo操作,如undo(3)，假设起始数据是0。

```java
abstract class Command{
    public abstract void Execute();
    public abstract void UnExecute();
}
class CalculatorCommand implements Command{
    private char operator;
    private int operand;
    private Calculator calculator;
    public CalculatorCommand(Calculator calculator,char operator,int operand){
        this.operator=operator;
        this.calculator=calculator;
        this.operand=operand;
    }
    public char Operator{
        set{operator=value;}
    }
    public int Operand{
        set{operand=value;}
    }
    public override void Execute(){
        calculator.Operation(operator,operand);
    }
    public override void UnExecute(){
        calculator.Operation(Undo(operator),operand);
    }
    private char Undo(char operator){
        switch(operator){
            case '+':return '-';
            case '-':return '+';
            case '*':return '/';
            case '/':return '*';
            default:throw new ArgumentException("operator");
        }
    }
}
class Calculator{
    private int curr=0;
    public void Operation(char operator,int operand){
        switch(operator){
            case '+':curr+=operand;break;
            case '-':curr-=operand;break;
            case '*':curr*=operand;break;
            case '/':curr/=operand;break;
        }
        Console.WriteLine("Current value ={0,3} (following {1} {2})",curr,operator,operand);
    }
}
class User{
    private Calculator calculator = new Calculator();
    private List<Command> commands = new Lise<Command>();
    private int current=0;
    public void Redo(int levels){
        Console.WriteLine("\n---- Redo {0} levels",levels);
        for (int i=0;i<levels;i++){
            if (current<commands.Count-1){
                Command command = commands[current++];
                command.Execte();
            }
        }
    }
    public void Undo(int levels){
        Console.WriteLine("\n---- Undo {0} levels",levels);
        for (int i=0;i<levels;i++){
            if (current>0){
                Command command = command(current--) as Command;
                command.UnExecute();
            }
        }
    }
    public void Compute(char operator,int operand){
        Command command = new CalculatorCommand(calculator,operator,operand);
        command.Execute();
        command.Add(command);
        current++;
    }
}
static void Main(String[] args){
    User user = new User();
    user.Compute('+',100);
    user.Compute('-',50);
    user.Compute('*',10);
    user.Compute('/',2);
    user.Undo(4);
    user.Redo(3);
    Console.ReadKey();
}
```



