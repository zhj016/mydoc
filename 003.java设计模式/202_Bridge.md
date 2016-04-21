## Bridge ( 桥接模式 ) ##

桥接模式是一种结构型模式，它主要应对的是： 由于实际的需要，某个类具有两个或两个以上的维度变化，如果只是用继承将无法实现这种需要，或者使得设计变得相当臃肿。

桥接模式的做法是把变化部分抽象出来，使变化部分与主类分离开来，从而将多个维度的变化彻底分离。最后，提供一个管理类来组合不同维度上的变化，通过这种组合来满足业务的需要。


    public interface Peppery{
        String style();
    }
      
    //实现类代表辣椒的风格
    public class PepperyStyle implements Peppery{
         public String style(){
              return "辣味";
         }
    }

    public class PlainStyle implements Peppery{
         public String style(){
              return "清淡" ;
         }
    }
    
    public abstract class AbstractNoodle{
         protected Peppery style;
         public AbstractNoodle(Peppery style){
              this.style = style;   
         }
         public abstract void eat();
    }
    

    //以下是猪肉面实现类
    public class PorkNoodle extends AbstractNoodle{
        public PorkyNodle(Peppery style){
             super(style);
        }
         public void eat(){
               System.out.println( "猪肉面条的口味："+super.style.style());
         }
    }


    //测试类
    public class Test{
         public static void main(String[] args){
             AbstractNoodle noodle = new PorkNoodle(new PepperyStyle());
             noodle.eat();
             AbstractNoodle noodle = new PorkNoodle(new PlainStyle());
             noodle.eat();
         }
    }
    
### Bridge模式四角色 ###
* 抽象（Abstraction）      -- 面条
* 细化抽象（Refined Abstraction）    -- 猪肉面条
* 实现者（Implementor）     -- 辣味
* 具体实现者（Concrete Implementor）   -- 辣与微辣



### Bridge 模式优点 ###

* 桥接模式分离实现与抽象，使得抽象和实现可以独立的扩展。当修改实现的代码时，不影响抽象的代码，反之也一样
满足开闭-原则。
* 抽象和实现者处于同层次，使得系统可独立地扩展这两个层次。增加新的具体实现者，不需要修改细化抽象，反之增加新的细化抽象也不需要修改具体实现。


