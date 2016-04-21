##Mediator ( 中介者模式 ) ##

中介者模式是封装一系列的对象交互的成熟模式，其关键是将对象之间的交互封装在称作中介者的对象中，中介者使各对象不需要显示地相互引用，这些对象只包含中介者的引用。当系统中某个对象需要和系统中另外一个对象交互时，只需将自己的请求通知中介者即可。 


###模式的结构中包括四种角色：###

* 中介者（Mediator） 
* 具体中介者（ConcreteMediator） 
* 同事（Colleague） 
* 具体同事（ConcreteColleague） 


### 同事（Colleague） : Colleague.java ###
    
    public interface Colleague{
        public void giveMess(String [] mess);
        public void receiverMess(String mess);
        public void setName(String name);
        public String getName();
    }
注：本问题中，只需要一个具体中介者，我们并不需要一个中介者（Mediator）接口 。


### 具体中介者（Mediator） : ConcreteMediator.java ###
    
    public class ConcreteMediator{
        ColleagueA colleagueA;
        ColleagueB colleagueB;
        ColleagueC colleagueC;
        public void registerColleagueA(ColleagueA colleagueA){
           this.colleagueA=colleagueA;
        }
        public void registerColleagueB(ColleagueB colleagueB){
           this.colleagueB=colleagueB;
        }
        public void registerColleagueC(ColleagueC colleagueC){
           this.colleagueC=colleagueC;
        }
        public void deliverMess(Colleague colleague,String [] mess){
           if(colleague==colleagueA){
              if(mess.length>=2){
                colleagueB.receiverMess(colleague.getName()+mess[0]);
                colleagueC.receiverMess(colleague.getName()+mess[1]);
              } 
           }
           else if(colleague==colleagueB){
              if(mess.length>=2){
                colleagueA.receiverMess(colleague.getName()+mess[0]);
                colleagueC.receiverMess(colleague.getName()+mess[1]);
              }  
           }
           else if(colleague==colleagueC){
              if(mess.length>=2){
                colleagueA.receiverMess(colleague.getName()+mess[0]);
                colleagueB.receiverMess(colleague.getName()+mess[1]);
              }  
           }    
        }
    }
    



###具体同事（ConcreteColleague）_1: ColleagueA.java ###
    
    public class ColleagueA implements Colleague{
        ConcreteMediator mediator; String name;
        ColleagueA(ConcreteMediator mediator){
           this.mediator=mediator;
           mediator.registerColleagueA(this);
        }
        public void setName(String name){
           this.name=name;
        }
        public String getName(){
            return name;
        } 
        public void giveMess(String [] mess){
            mediator.deliverMess(this,mess);
        }
        public void receiverMess(String mess){
           System.out.println(name+"收到的信息:");
           System.out.println("\t"+mess);
        }
    }
    
###具体同事（ConcreteColleague）_2: ColleagueB.java ###
    
    public class ColleagueB implements Colleague{
        ConcreteMediator mediator;              
        String name;
        ColleagueB(ConcreteMediator mediator){
           this.mediator=mediator;
           mediator.registerColleagueB(this);
        }
        public void setName(String name){
           this.name=name;
        }
        public String getName(){
            return name;
        } 
       public void giveMess(String [] mess){
            mediator.deliverMess(this,mess);
        }
        public void receiverMess(String mess){
           System.out.println(name+"收到的信息:");
           System.out.println("\t"+mess);
        }
    }
    



###具体同事（ConcreteColleague）_3: ColleagueC.java ###
    
    public class ColleagueC implements Colleague{
        ConcreteMediator mediator;              
        String name;
        ColleagueC(ConcreteMediator mediator){
           this.mediator=mediator;
           mediator.registerColleagueC(this);
        }
        public void setName(String name){
           this.name=name;
        }
        public String getName(){
            return name;
        } 
        public void giveMess(String [] mess){
            mediator.deliverMess(this,mess);
        }
        public void receiverMess(String mess){
           System.out.println(name+"收到的信息:");
           System.out.println("\t"+mess);
        }
    }
    
    


###应用 Application.java###

     public class Application{
        public static void main(String args[]){
           ConcreteMediator mediator=new ConcreteMediator();
           ColleagueA colleagueA=new ColleagueA(mediator);
           ColleagueB colleagueB=new ColleagueB(mediator);
           ColleagueC colleagueC=new ColleagueC(mediator);
           colleagueA.setName("A国");
           colleagueB.setName("B国");
           colleagueC.setName("C国");
           String [] messA={"要求归还曾抢夺的100斤土豆","要求归还曾抢夺的20头牛"};  
           colleagueA.giveMess(messA);
           String [] messB={"要求归还曾抢夺的10只公鸡","要求归还曾抢夺的15匹马"};
           colleagueB.giveMess(messB);
           String [] messC={"要求归还曾抢夺的300斤小麦","要求归还曾抢夺的50头驴"};
           colleagueC.giveMess(messC);
        }
    }
    


###中介者模式的优点###

* 可以避免许多的对象为了之间的通信而相互显示引用，不仅系统难于维护，而且也使其他系统难以复用这些对象。
* 可以通过中介者将原本分布于多个对象之间的交互行为集中在一起。当这些对象之间需要改变之间的通信行为时，只需使用一个具体中介者即可，不必修改各个具体同事的代码，即这些同事可被重用。
* 具体中介者使得各个具体同事完全解耦，修改任何一个具体同事的代码不会影响到其他同事。
* 具体中介者集中了同事之间是如何交互的细节，使得系统比较清楚地知道整个系统中的同事是如何交互的。
* 当一些对象想互相通信，但又无法相互包含对方的引用，那么使用中介者模式就可以使得这些对象互相通信。
