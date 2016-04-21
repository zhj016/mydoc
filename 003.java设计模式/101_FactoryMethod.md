## FactoryMethod  工厂方法 ##


* 客户类和工厂类分开。
* 消费者任何时候需要某种产品，只需向工厂请求即可。
* 消费者无须修改就可以接纳新产品。
* 缺点是当产品修改时，工厂类也要做相应的修改。

### Factory Method 实例 1 ###

    public class Factory{ 　　
        public static Sample creator(int which){
        　　if (which==1)
        　　　　return new SampleA();
        　　else if (which==2)
        　　　　return new SampleB();
        　　}
    }
    

### Factory Method 实例 2 ###


    interface IFactory {
    	public ICar createCar();
    }
    
    class Factory implements IFactory {
    	public ICar createCar() {
    		Engine engine = new Engine();
    		Underpan underpan = new Underpan();	 		
    		Wheel wheel = new Wheel();
    		ICar	car = new Car(underpan, wheel, engine);
    		return car;	
        }
    }

    public class Client {
    	public static void main(String[] args) {		
        	IFactory factory = new Factory();	
        	ICar car = factory.createCar();				
        	car.show();	
    	}
    }
    

