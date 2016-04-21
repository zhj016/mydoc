##Memento ( 备忘录模式 ) ##

备忘录模式是关于怎样保存对象状态的成熟模式，其关键是提供一个备忘录对象，该备忘录负责存储一个对象的状态，程序可以在磁盘或内存中保存这个备忘录，这样一来，程序就可以根据对象的备忘录将该对象恢复到备忘录中所存储的状态。 


### 模式的结构中包括三种角色：###

* 原发者（Originator） 
* 备忘录（Memento） 
* 负责人（Caretaker） 


###原发者（Originator）: ReadPhrase.java ###
    
    package tom.jiafei;
    import java.io.*;
    public class ReadPhrase {
         long readPosition;
         File file;
         RandomAccessFile in;
         String phrase=null; 
         public ReadPhrase(File file){
            this.file=file;
            try{ 
                  in=new RandomAccessFile(file,"r");
            }
            catch(IOException exp){ }
        } 
        public Memento createMemento(){
              Memento mem=new Memento();
              mem.setPositionState(readPosition);
              return mem;
        }
        public void restoreFromMemento(Memento mem){
             readPosition=mem.getPositionState();
       }
        public String readLine(){
             try{     in.seek(readPosition); 
                        phrase=in.readLine();
                        if(phrase!=null){
                           byte b[]= phrase.getBytes("iso-8859-1");
                           phrase=new String(b);         
                       }
                       readPosition=in.getFilePointer();   
             }
             catch(IOException exp){}
             return phrase;
        }
        public void closeRead(){
             try{   in.close();
             }
             catch(IOException exp){ }
        }
    }
    

###备忘录（Memento）: Memento.java ###
    
    package tom.jiafei;
    public class  Memento implements java.io.Serializable{
          private long state;
           void setPositionState(long state){
                  this.state=state;
           } 
           long getPositionState(){
                   return state;
           } 
    }
    


###负责人（Caretaker）：Caretaker.java ###
    
    import tom.jiafei.*;
    import java.io.*;
    public class Caretaker{
          File file;
          private Memento  memento=null;
          Caretaker(){
               file=new File("saveObject.txt");
          }
          public  Memento getMemento(){
               if(file.exists()) {
                   try{
                         FileInputStream  in=new FileInputStream("saveObject.txt");
                         ObjectInputStream  inObject=new ObjectInputStream(in);
                         memento=(Memento)inObject.readObject();
                   }
                   catch(Exception exp){}
               }
               return  memento;
          }
          public void saveMemento(Memento  memento){
                try{     FileOutputStream  out=new FileOutputStream("saveObject.txt");
                         ObjectOutputStream  outObject=new ObjectOutputStream(out);
                         outObject.writeObject(memento);
                   }
                   catch(Exception exp){}  
          }
    }
    
    


###应用: Application.java ###
    
    import tom.jiafei.*;
    import java.util.Scanner;
    import java.io.*;
    public class Application{
         public static void main(String args[]) {
                Scanner reader=new Scanner(System.in);
                ReadPhrase  readPhrase=new ReadPhrase(new File("phrase.txt"));
                File favorPhrase=new File("favorPhrase.txt");
                RandomAccessFile out=null;
                try{    out=new RandomAccessFile(favorPhrase,"rw");
                }
                catch(IOException exp){}
                System.out.println("是否从上次读取的位置继续读取成语（输入y或n）");
                String answer=reader.nextLine();
                if(answer.startsWith("y")||answer.startsWith("Y")){
                      Caretaker  caretaker=new Caretaker();       //创建负责人
                      Memento memento=caretaker.getMemento();     //得到备忘录
                      if(memento!=null)
                        readPhrase.restoreFromMemento(memento); //使用备忘录恢复状态
                }
                String phrase=null;
                while((phrase=readPhrase.readLine())!=null){
                     System.out.println(phrase);
                     System.out.println("是否将该成语保存到"+favorPhrase.getName());
                     answer=reader.nextLine();
                     
                    if(answer.startsWith("y")||answer.startsWith("Y")){
                       try{     out.seek(favorPhrase.length());
                                   byte [] b=phrase.getBytes();
                                   out.write(b); 
                                   out.writeChar('\n');
                      }
                      catch(IOException exp){}
                 }
                  System.out.println("是否继续读取成语？(输入y或n)");
                 answer=reader.nextLine();
                 if(answer.startsWith("y")||answer.startsWith("Y"))
                     continue;
                 else{
                      readPhrase.closeRead();
                      Caretaker  caretaker=new Caretaker();             //创建负责人
                      caretaker.saveMemento(readPhrase.createMemento());//保存备忘录
                      try{  out.close();
                      } 
                      catch(IOException exp){}
                      System.exit(0);
                 }     
           }
           System.out.println("读完全部成语");
     }
} 





### 备忘录模式的优点  ###

* 备忘录模式使用备忘录可以把原发者的内部状态保存起来，使得只有很“亲密的”的对象可以访问备忘录中的数据。
* 备忘录模式强调了类设计单一责任原则，即将状态的刻画和保存分开。
