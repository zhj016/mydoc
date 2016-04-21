## Chain of Responsibility ( 责任链模式 ) ##

使多个对象都有机会处理请求，从而避免请求的发送者和接收者之间的耦合关系。将这些对象连成一条链，并沿着这条链传递该请求，直到有一个对象处理它为止。

### 角色 ###
* 处理者（Handler） 
* 具体处理者（ConcreteHandler） 


### 处理者（Handler）: ###
    Handler.java 
    public interface Handler
    {
       public abstract void handleRequest(String number);
       public abstract void setNextHandler(Handler handler);
    }



### 具体处理者（ConcreteHandler）_1: ###
Beijing.java
    
    import java.util.*;
    public class Beijing implements Handler
    {
         private Handler handler;    
         private ArrayList<String> numberList; 
         Beijing()
         {
            numberList=new ArrayList<String>();
            numberList.add("11129812340930034"); 
            numberList.add("10120810340930632");
            numberList.add("22029812340930034"); 
            numberList.add("32620810340930632");
         }
         public void handleRequest(String number)
         {
            if(numberList.contains(number))
               System.out.println("该人在北京居住");
            else{
               System.out.println("该人不在北京居住");
               if(handler!=null)
                 handler.handleRequest(number);    
            }
         }
         public void setNextHandler(Handler handler)
         {
            this.handler=handler;
         }
    }
    

### 具体处理者（ConcreteHandler）_2: ###

Shanghai.java
    
    import java.util.*;
    public class Shanghai implements Handler
    {
         private Handler handler;            
         private ArrayList<String> numberList; 
         Shanghai()
         {
            numberList=new ArrayList<String>();
            numberList.add("34529812340930034"); 
            numberList.add("98720810340430632");
            numberList.add("36529812340930034"); 
            numberList.add("77720810340930632");
         }
         public void handleRequest(String number)
         {
            if(numberList.contains(number))
               System.out.println("该人在上海居住");
            else{
               System.out.println("该人不在上海居住");
               if(handler!=null)
                  handler.handleRequest(number);     
            }
         }
         public void setNextHandler(Handler handler)
         {
            this.handler=handler;
         }
    }
    
    

### 应用 ###

Application.java

    public class Application{
        private Handler beijing,shanghai,tianjin;   
        public void createChain()
        {       
           beijing=new Beijing();
           shanghai=new Shanghai();
           tianjin=new Tianjin();
           beijing.setNextHandler(shanghai);
           shanghai.setNextHandler(tianjin);
        }
        public void reponseClient(String number)
        {  
           beijing.handleRequest(number);
        }
        public static void main(String args[])
        {
           Application  application=new  Application();
           application.createChain();
           application.reponseClient("77720810340930632");;
        }
    }
    

