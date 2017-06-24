# Task-4
一．观察者模式 
  简单地说，观察者模式定义了一个一对多的依赖关系，让一个或多个观察者对象监察一个主题对象。这样一个主题对象在状态上的变化能够通知所有的依赖于此对象的那些观察者对象，使这些观察者对象能够自动更新。
观察者模式（有时又被称为发布（publish ）-订阅（Subscribe）模式、模型-视图（View）模式、源-收听者(Listener)模式或从属者模式）是软件设计模式的一种。在此种模式中，一个目标物件管理所有相依于它的观察者物件，并且在它本身的状态改变时主动发出通知。这通常透过呼叫各观察者所提供的方法来实现。此种模式通常被用来实现事件处理系统。
观察者模式（Observer）完美的将观察者和被观察的对象分离开。举个例子，用户界面可以作为一个观察者，业务数据是被观察者，用户界面观察业务数据的变化，发现数据变化后，就显示在界面上。面向对象设计的一个原则是：系统中的每个类将重点放在某一个功能上，而不是其他方面。一个对象只做一件事情，并且将他做好。观察者模式在模块之间划定了清晰的界限，提高了应用程序的可维护性和重用性。
二.3D彩票的号码 代码实现

3D彩票服务号主题 ObjectFor3d类
package lmq.observer;  
  
import java.util.ArrayList;  
import java.util.List;  
  
public class ObjectFor3D implements Subject  
{  
    private List<Observer> observers = new ArrayList<Observer>();  
    /**      * 3D彩票的号码 
     */  
    private String msg;  
  
    @Override  
    public void registerObserver(Observer observer)  
    {  
        observers.add(observer);  
    }  
  
    @Override      public void removeObserver(Observer observer)  
    {  
        int index = observers.indexOf(observer);  
        if (index >= 0)  
        {  
            observers.remove(index);  
        }  
    }  
  
    @Override  
    public void notifyObservers()      {  
        for (Observer observer : observers)  
        {  
            observer.update(msg);  
        }  
    }  
  
    /** 
     * 主题更新消息 
     *  
     * @param msg      */  
    public void setMsg(String msg)  
    {  
        this.msg = msg;  
          
        notifyObservers();  
    }  
  
}  

模拟两个使用者：
使用者1 Observer1类 :
package lmq.observer;  
  
public class Observer1 implements Observer  
{  
  
    private Subject subject;  
  
    public Observer1(Subject subject)  
    {  
        this.subject = subject;  
        subject.registerObserver(this);  
    }  
  
    @Override  
    public void update(String msg)  
    {  
        System.out.println("observer1 得到 3D 号码  -->" + msg + ", 我要记下来。");  
    }  
  
}  

使用者2 Observer2类 :
package lmq.observer;  
  
public class Observer2 implements Observer  
{  
    private Subject subject ;   
      
    public Observer2(Subject subject)  
    {  
        this.subject = subject  ;  
        subject.registerObserver(this);  
    }  
      
    @Override  
    public void update(String msg)  
    {  
        System.out.println("observer2 得到 3D 号码 -->" + msg + "我要告诉舍友们。");  
    }  
      
       
}  


Test类:

package lmq.test;  
  
import lmq.ObjectFor3D;  
import lmq.Observer;  
import lmq.Observer1;  
import lmq.Observer2;  
import lmq.observer.Subject;  
  
public class Test  
{  
    public static void main(String[] args)  
    {  
        //模拟一个3D的服务号  
        ObjectFor3D subjectFor3d = new ObjectFor3D();  
        //客户1  
        Observer observer1 = new Observer1(subjectFor3d);  
        Observer observer2 = new Observer2(subjectFor3d);  
  
        subjectFor3d.setMsg("20140420的3D号码是：127" );  
        subjectFor3d.setMsg("20140421的3D号码是：333" );  
          
    }  
}  

