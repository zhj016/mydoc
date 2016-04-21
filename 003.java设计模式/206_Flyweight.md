## Flyweight ( 享元模式 ) ##

GoF对享元模式的描述是：运用共享技术有效地支持大量细粒度的对象。


一个咖啡店有几种口味的咖啡（拿铁、摩卡、卡布奇诺等等），如果这家店接到分订单要几十杯咖啡。那么显然咖啡的口味就可以设置成共享的，而不必为每一杯单独生成。

    import java.util.*;
    public abstract class Order {
        // 执行卖出动作
        public abstract void sell();
    }
    public class FlavorOrder extends Order {
        public String flavor;
        // 获取咖啡口味
        public FlavorOrder(String flavor) {
           this.flavor = flavor;
        }
        @Override
        public void sell() {
           // TODO Auto-generated method stub
           System.out.println("卖出一份" + flavor + "的咖啡。");
        }
    }
    
    
    public class FlavorFactory {
        private Map<String, Order> flavorPool = new HashMap<String, Order>();
        // 静态工厂,负责生成订单对象
        private static FlavorFactory flavorFactory = new FlavorFactory();
        
        private FlavorFactory() 
        {
        }
        
        public static FlavorFactory getInstance() {
           return flavorFactory;
        }
            
        public Order getOrder(String flavor) {
           Order order = null;
           if (flavorPool.containsKey(flavor)) 
           {
                // 如果此映射包含指定键的映射关系，则返回 true
                 order = flavorPool.get(flavor);
           } 
           else 
           {
                order = new FlavorOrder(flavor);
                flavorPool.put(flavor, order);
           }
           return order;
        }
        
        public int getTotalFlavorsMade() {
            return flavorPool.size();
        }
    }
    
    
    