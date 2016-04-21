## Decorator ( 装饰模式 ) ##

* 装饰模式是动态地扩展一个对象的功能，而不需要改变原始类代码的一种成熟模式。
* 在装饰模式中，“具体组件”类和“具体装饰”类是该模式中的最重要的两个角色。
* 具体被装饰者和抽象装饰类都继承于抽象被装饰者类，继承的是类型，而不是行为。
* 行为来自装饰者和基础组件，或与其他装饰者之间的组合关系。

### Decorator四角色 ###

* 抽象组件（Component） 
* 具体组件（ConcreteComponent） 
* 装饰（Decorator） 
* 具体装饰（ConcreteDecotator）
 
#### 抽象组件 ####

    public abstract class Beverage {	
    	public abstract String getDescription(); 	
    	public abstract double cost();
    }
    
#### 具体组件 ####

    public class HouseBlend extends Beverage{
        String description;
    	public HouseBlend(){
    		description = "House Blend Coffee";	
        }
        public String getDescription() { 
            return descripiton;
        }
    	public double cost() {		
    	// TODO Auto-generated method stub
    	   return 0.89;	
        }
    }
    

#### 装饰 ####

    public abstract class CondimentDecorator  extends Beverage
    {
    	protected Beverage beverage;
        public CondimentDecorator (Beverage beverage){		
    	   this.beverage = beverage;	
        }
    }
    

#### 装饰 ####
    public class Mocha extends CondimentDecorator{	
        	
        @Override	public String getDescription() {		
        	// TODO Auto-generated method stub		
        	return beverage.getDescription() + ", Mocha";	
        }	
        @Override	public double cost() {
        	// TODO Auto-generated method stub		
            return 0.20 + beverage.cost();	
        }
    }
    
### Decorator优点 ###

* 被装饰者和装饰者是松耦合关系。由于装饰（Decorator）仅仅依赖于抽象组件（Component），因此具体装饰只知道它要装饰的对象是抽象组件的某一个子类的实例，但不需要知道是哪一个具体子类。
* 装饰模式满足“开-闭原则”。不必修改具体组件，就可以增加新的针对该具体组件的具体装饰。
* 可以使用多个具体装饰来装饰具体组件的实例。



