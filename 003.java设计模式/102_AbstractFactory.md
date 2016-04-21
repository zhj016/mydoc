## AbstractFactory 抽象工厂 ##

抽象工厂模式用来处理不同的工厂生产不同的产品的问题。

比如：

抽象汽车工厂  
  
* 奔驰工厂    
    * 生产奔驰轿车
    * 生产奔驰房车

* 宝马工厂
    * 生产宝马轿车
    * 生产宝马房车

抽象轿车

* 奔驰轿车
* 宝马轿车

抽象房车  

* 奔驰房车    
* 宝马房车

奔驰轿车，奔驰房车在同一个工厂生产。 宝马轿车宝马房车在另外一处工厂生产。

    interface IProduct1 {
    	public void show();
    }
    interface IProduct2 {	
        public void show();
    }
    
    class Product1 implements IProduct1 {
    	public void show() {
    		System.out.println(“这是轿车");	
        }
    }
                   
    class Product2 implements IProduct2 {
     	public void show() {
    		System.out.println(“这是房车");	
        }
    }
    
    interface IFactory {
    	public IProduct1 createProduct1();
    	public IProduct2 createProduct2();
    }
    
    
    class Factory implements IFactory{
    	public IProduct1 createProduct1() {
            return new Product1();	
        }
    	public IProduct2 createProduct2() {
            return new Product2();	
        }
    }

    public class Client {
    	public static void main(String[] args){
            IFactory factory = new Factory();
            factory.createProduct1().show();
            factory.createProduct2().show();
        }
    }
    	
	