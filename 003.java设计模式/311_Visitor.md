## Visitor ( 访问者模式 ) ##

* 访问者模式的目的是封装一些施加于某种数据结构元素之上的操作。一旦这些操作需要修改的话，接受这个操作的数据结构可以保持不变。
* 访问者模式适用于数据结构相对未定的系统，它把数据结构和作用于结构上的操作之间的耦合解脱开，使得操作集合可以相对自由的演化。
* 访问者模式使得增加新的操作变的很容易，就是增加一个新的访问者类。访问者模式将有关的行为集中到一个访问者对象中，而不是分散到一个个的节点类中。

	    
	    
	    public abstract class Customer {
	             private String customerId;
	             private String name;
	             public String getCustomerId() 
	             {
	                       return customerId;
	             }
	             public void setCustomerId(String customerId) 
	             {
	                      this.customerId = customerId;
	             }
	             public String getName() 
	             {
	                      return name;
	             }
	             public void setName(String name) 
	             {
	                     this.name = name;
	             }
	     
	             /**
	              * 接受访问者的访问
	              * @param visitor
	              */
	             public abstract void accept(Visitor visitor);
	    } 
	    
	    

	    
	    /**
	     * 企业客户
	     */
	    public class EnterpriseCustomer extends Customer 
	    {
	              private String registerAddress;
	               public String getRegisterAddress() 
	               {
	                      return registerAddress;
	              }
	              public void setRegisterAddress(String registerAddress) 
	              {
	                        this.registerAddress = registerAddress;
	              }
	              @Override
	              public void accept(Visitor visitor) 
	              {
	                       //回调访问者对象的方法
	                       visitor.visitEnterpriseCustomer(this);
	              }
	    }
	    
	    
	    /**
	     * 访问者接口
	     */
	    public interface Visitor {
	    
	              /**
	               * 访问企业客户，相当于给企业客户添加访问者功能
	               * @param ec 企业客户对象
	               */
	              public void visitEnterpriseCustomer(EnterpriseCustomer ec);
	              /**
	               * 访问个人客户，相当于给个人客户添加访问者的功能
	               * @param pc
	               */
	              public void visitPersonalCustomer(PersonalCustomer pc);
	    }
	    
	
	    
	    /**
	     * 具体的访问者，实现对客户的偏好分析
	     */
	    public class PredilectionAnalyzeVisitor implements Visitor {
	    
	               @Override
	               public void visitEnterpriseCustomer(EnterpriseCustomer ec) {
	                       // TODO 根据以往的购买历史、潜在购买意向，以及客户所在行业的发展趋势、客户的发展趋势等的分析
	                       System.out.println("现在对企业客户" + ec.getName() + "进行产品偏好分析");
	               }
	    
	               @Override
	               public void visitPersonalCustomer(PersonalCustomer pc) {
	                       System.out.println("现在对个人客户" + pc.getName() + "进行产品偏好分析");
	               }
	    
	    }
	    
	    
	    /**
	     * 具体的访问者，实现客户提出服务请求的功能
	     */
	    public class ServiceRequestVisitor implements Visitor {
	    
	               @Override
	                public void visitEnterpriseCustomer(EnterpriseCustomer ec) {
	                           // TODO 企业客户提出的具体服务请求
	                           System.out.println(ec.getName() + "企业提出服务请求");
	                }
	    
	                @Override
	                public void visitPersonalCustomer(PersonalCustomer pc) {
	                          // TODO 个人客户提出的具体服务请求
	                         System.out.println("客户" + pc.getName() + "提出服务请求");
	                }
	    
	    }
	    
	    public class ObjectStructure {
	    
	              /**
	               * 要操作的客户集合
	               */
	              private Collection<Customer> col = new ArrayList<Customer>();
	              /**
	               * 提供客户端操作的高层接口，具体的功能由客户端传入的访问者决定
	               * @param visitor 客户端需要的访问者
	               */
	              public void handleRequest(Visitor visitor) {
	                        for(Customer cm : col) {
	                                 cm.accept(visitor);
	                         }
	              }
	              /**
	               * 组建对象结构，想对象中添加元素
	               * 不同的对象结构有不同的构建方式
	               * @param ele 加入到对象的结构元素
	               */
	              public void addElement(Customer ele) {
	                        this.col.add(ele);
	              }
	    }
	    
	
	
	    public class Client {
	        public static void main(String[] args) {
	                        ObjectStructure os = new ObjectStructure();
	                        Customer cml = new EnterpriseCustomer();
	                        cml.setName("ABC集团");
	                        os.addElement(cml);
	                        ServiceRequestVisitor srVisitor = new ServiceRequestVisitor();
	                        os.handleRequest(srVisitor);
	      
	                        PredilectionAnalyzeVisitor paVisitor = new PredilectionAnalyzeVisitor();
	                        os.handleRequest(paVisitor);
	      
	                       WorthAnalyzeVisitor waVisitor = new WorthAnalyzeVisitor();
	                       os.handleRequest(waVisitor);
	        }
	    }