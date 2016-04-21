## Composite ( 组合模式 ) ##

对象间常常通过树结构来组织（包含）起来，以实现整体-部分的层次结构。

### 组合模式的特点是：###
对象通过实现（继承）统一的接口（抽象类），调用者对单一对象和组合对象的操作具有一致性。整体上可以看做是一个组合对象。

### Composite模式的三角色 ###
* 抽象组件（Component） 
* Composite节点（Composite Node） 
* Leaf节点（Leaf Node）

#### 抽象组件 ####

    public interface MilitaryPerson{
          public void add(MilitaryPerson person) ;
          public void remove(MilitaryPerson person) ;
          public MilitaryPerson getChild(int index); 
          public Iterator<MilitaryPerson>  getAllChildren() ;
          public boolean isLeaf();
          public double getSalary();
          public void setSalary(double salary);
    } 
    
#### Composite节点 ####

    public class MilitaryOfficer implements MilitaryPerson{
          LinkedList<MilitaryPerson> list;
          String name;
          double salary;
          MilitaryOfficer(String name,double salary){
                this.name=name;
                this.salary=salary;
                list=new LinkedList<MilitaryPerson>();
          } 
          public boolean isLeaf()  {return false; } 
          public double getSalary() { return salary; }
          public void setSalary(double salary){
               this.salary=salary;      
          }
    }
    
#### Leaf节点 ####
    
    public class MilitarySoldier implements MilitaryPerson{
          double salary;
          String name;
          MilitarySoldier(String name,double salary){
                this.name=name;
                this.salary=salary;
          }
          public void add(MilitaryPerson person)  {}
          public void remove (MilitaryPerson person){}
          public MilitaryPerson getChild(int index) { return null; }
          public Iterator<MilitaryPerson>  getAllChildren() { return null;}
    
          public boolean isLeaf() { return true;} 
          public double getSalary() { return salary;}
          public void setSalary(double salary){
               this.salary=salary;
          }
    }


#### 应用 ####
    
    public class ComputerSalary{
         public static double computerSalary(MilitaryPerson person){
               double sum=0;
               if(person.isLeaf()==true){
                    sum=sum+person.getSalary();
               }
               if(person.isLeaf()==false){
                    sum=sum+person.getSalary();
                    Iterator<MilitaryPerson> iterator=person.getAllChildren();
                    while(iterator.hasNext()){
                                 MilitaryPerson p= iterator.next();
                                 sum=sum+computerSalary(p);;
                    }
               }
               return sum;
        }
    } 
    

### Composite优点 ###

* 组合模式中包含有个体对象和组合对象，并形成树形结构，使用户可以方便地处理个体对象和组合对象。
* 组合对象和个体对象实现了相同的接口，用户一般不需区分个体对象和组合对象。
* 当增加新的Composite节点和Leaf节点时，用户的重要代码不需要作出修改。


