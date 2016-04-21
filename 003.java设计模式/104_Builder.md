## Builder ( 建造者模式 ) ##

* 将产品的内部表象和产品的生成过程分割开来，从而使一个建造过程生成具有不同的内部表象的产品对象。
* 建造模式使得产品内部表象可以独立的变化，客户不必知道产品内部组成的细节。
* 建造模式可以强制实行一种分步骤进行的建造过程。 


### Builder模式的四种角色：###
* 产品（Product） 
* 抽象生成器（Builder） 
* 具体生成器（ConcreteBuilder） 
* 指挥者（Director） 


###抽象生成器
	
	    public interface Builder { 　　
	        void buildPartA(); 
	        void buildPartB(); 
	        void buildPartC(); 
	        Product getResult(); 
	    } 
    
###指挥者

    public class Director { 　　
        private Builder builder; 
        public Director( Builder builder ) { 
            this.builder = builder; 
        } 
        public void construct() { 
            builder.buildPartA();
            builder.buildPartB();
            builder.buildPartC(); 　　
        } 
    } 
    

### Builder模式的优点 ###

* 生成器模式将对象的构造过程封装在具体生成器中，用户使用不同的具体生成器就可以得到该对象的不同表示。
* 生成器模式将对象的构造过程从创建该对象的类中分离出来，使得用户无须了解该对象的具体组件。
* 可以更加精细有效地控制对象的构造过程。生成器将对象的构造过程分解成若干步骤，这就使得程序可以更加精细，有效地控制整个对象的构造。
* 生成器模式将对象的构造过程与创建该对象类解耦，使得对象的创建更加灵活有弹性。
* 当增加新的具体生成器时，不必修改指挥者的代码，即该模式满足开-闭原则。

