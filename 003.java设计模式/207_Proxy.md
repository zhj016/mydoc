## Proxy ( 代理模式 ) ##

为其他对象提供一种代理以控制对这个对象的访问。在某些情况下，一个客户不想或者不能直接引用另一个对象，而代理对象可以在客户端和目标对象之间起到中介的作用。


###抽象角色：###
    abstract public class Subject
    {      
         abstract public void request();
    }

###真实角色：###
实现了Subject的request()方法。
    public class RealSubject extends Subject{
         public RealSubject()
         { 
         }
         public void request()
         {
               System.out.println("From real subject.");
         }
    } 
    
### 代理角色： ###
    public class ProxySubject extends Subject{
         private RealSubject realSubject; //以真实角色作为代理角色的属性 
          public ProxySubject()
          {
          } 
         public void request()
         { 
            //该方法封装了真实对象的request方法 
             preRequest(); 
             if( realSubject == null )
             {
                   realSubject = new RealSubject();
             }
             realSubject.request(); //此处执行真实对象的request方法 
             postRequest(); 
         }
         private void preRequest()
         { 
              //something you want to do before requesting 
         }
         private void postRequest()
         { 
             //something you want to do after requesting 
         }
    }
    
### 客户端调用：###

    Subject sub=new ProxySubject();
    Sub.request(); 