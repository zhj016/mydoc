## Prototype (原型模式 ) ##

* 原型模式是从一个对象出发得到一个和自己有相同状态的新对象的成熟模式。
* 该模式的关键是将一个对象定义为原型，并为其提供复制自己的方法。 
* 每一个类都必须配备一个克隆方法。     

###关于浅复制和深复制

1. 浅复制（浅克隆）
被复制对象的所有变量都含有与原来的对象相同的值，而所有的对其他对象的引用仍然指向原来的对象。换言之，浅复制仅仅复制所考虑的对象，而不复制它所引用的对象。

2. 深复制（深克隆）
被复制对象的所有变量都含有与原来的对象相同的值，除去那些引用其他对象的变量。那些引用其他对象的变量将指向被复制过的新对象，而不再是原有的那些被引用的对象。换言之，深复制把要复制的对象所引用的对象都复制了一遍。

**Object对象的clone方法是浅复制**



### 示例代码 ###

    public abstract class AbstractSpoon implements Cloneable
    { 
    　　String spoonName; 
    
    　　public void setName(String Name) {this.spoonName = Name;}
    　　public String getName() {return this.spoonName;}
    
    　　public Object clone() 
    　　{
    　　　　Object object = null;
    　　　　try {
    　　　　　　object = super.clone();
    　　　　} catch (CloneNotSupportedException exception) {
    　　　　　　System.err.println("AbstractSpoon is not Cloneable");
    　　　　}
    　　　　return object;
    　　}
    }

    public class SoupSpoon extends AbstractSpoon
    { 
    　　public SoupSpoon()
    　　{
    　　　　setSpoonName("Soup Spoon"); 
    　　}
    }
    
    public class SaladSpoon extends AbstractSpoon
    { 
    　　public SaladSpoon()
    　　{
    　　　　setSpoonName("Salad Spoon"); 
    　　}
    }
    　


