## Observer ( 观察者模式 ) ##

观察者模式定义了一种一队多的依赖关系，让多个观察者对象同时监听某一个主题对象。这个主题对象在状态上发生变化时，会通知所有观察者对象，使他们能够自动更新自己

### 示例代码 ###
    public interface Observer
    {
        public void update(Observable observable, Object obj);
    }
    
    public abstract class Observable 
    {
        private ArrayList<Observer> list = new ArrayList<Observer>();
        
        public void notifyObservers(String name)
        {
            //notify all the observer here.
        }
        
        public void addObserver(Observer inf)
        {
            list.add(inf);
        }
            
    }
    
    public class product extends Observable{ 
    　　private String name;
    　　private float price;
    　　public String getName()
        {
            return name;
        }
    　　public void setName()
        {
        　　 this.name=name;
        　　 setChanged();
        　　 notifyObservers(name);
    　　}　　　
    }
    
    public class NameObserver implements Observer
    {
     　　private String name=null;
     　　public void update(Observable obj,Object arg)
         {
     　　　　if (arg instanceof String){
        　　　　 name=(String)arg;
        　　　　 System.out.println("NameObserver :name changet to "+name);
    　　　　}
    　　}
    }
    
    

