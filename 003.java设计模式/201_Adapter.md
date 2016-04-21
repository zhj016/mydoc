## Adapter ( 适配器模式 ) ##

将一个类的接口转换成客户希望的另外一个接口。Adapter模式使得原本由于接口不兼容而不能一起工作的那些类可以一起工作。(GoF) 


### Adapter模式的三种角色 ###
* 目标（Target） 
* 被适配者（Adaptee） 
* 适配器（Adapter） 

### 示例代码 ###

    // 图形发送设备   
    public class Target {   
        /**  
         * 传送图形信号  
         */   
        public String request() {  
             return "Graphic sender";   
        }   
    }   

    
    // 显示器   
    public class Client {   
       
       public static void main(String[] args) {   
            Target target = new Targete();   
            System.out.println(target.request());   
        }   
    }
   
    
#### Adaptee 被适配者 ####
另外一种设备却提供不同的接口
    
    public interface adaptee {
        public String getData();
    }

    // 显卡，即我们的适配器   
    public class Adapter extends Target {   
       
        // 被代理的设备   
        private Adaptee apt = null;   
         /**  
         * 装入被代理的设备  
         */   
       public Adapter(Adaptee apt) {   
           this.apt = apt;   
       }   
      
       /**  
        * 被代理的设备传过来的数据转换成为图形输出  
        */   
       public String request() {   
           return apt.getData();   
       }   
    } 
    

    public class Client {   
       
        public static void main(String[] args) {   
            // CPU经过显卡的适配后“变”成了图形发送装置了   
            Target target = new Adapter(new Adaptee());   
            System.out.println(target.request());   
        }   
    } 

### 适配器模式的优点 ###
* 目标（Target）和被适配者（Adaptee）是完全解耦的关系。
* 适配器模式满足“开-闭原则”。当添加一个实现Adaptee接口的新类时，不必修改Adapter，Adapter就能对这个新类的实例进行适配。
