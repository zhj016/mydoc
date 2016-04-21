## TemplateMethod ( 模板方法 ) ##


* 定义一个操作中的算法的骨架，而将一些步骤延迟到子类中。模板方法使得子类可以不改变一个算法的结构即可重定义该算法的某些特定步骤
* 模板方法是关于怎样将若干个方法集成到一个方法中，以便形成一个解决问题的算法骨架。模板方法模式的关键是在一个抽象类中定义一个算法的骨架，即将若干个方法集成到一个方法中，并称该方法为一个模板方法，或简称为模板。 


###模式的结构中包括两种角色：###

* 抽象模板（Abstract Template） 
* 具体模板（Concrete Template） 


抽象模板（Abstract Template）: AbstractTemplate.java 

    import java.io.*;
    public abstract  class  AbstractTemplate{
          File [] allFiles;
          File dir;
          AbstractTemplate(File dir){
               this.dir=dir;
          }
           public final void  showFileName(){
                allFiles=dir.listFiles();
                sort();
                printFiles();
          }
          public abstract void sort();
          public abstract void printFiles();
    }
    
    


具体模板（Concrete Template）_1: ConcreteTemplate1.java 

    import java.io.*;
    import java.awt.*;
    import java.util.Date;
    import java.text.SimpleDateFormat;
    public  class ConcreteTemplate1 extends  AbstractTemplate{
           ConcreteTemplate1(File dir){
               super(dir);
          }
          public void sort(){
               for(int i=0;i<allFiles.length;i++)
                    for(int j=i+1;j<allFiles.length;j++)
                          if(allFiles[j].lastModified()<allFiles[i].lastModified()){
                                File file=allFiles[j];
                                allFiles[j]=allFiles[i];
                                allFiles[i]=file;
                          }
          }
          public void printFiles(){
                 for(int i=0;i<allFiles.length;i++){
                     long time=allFiles[i].lastModified();
                     Date date=new Date(time);
                     SimpleDateFormat matter= new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
                     String str=matter.format(date);
                     String name=allFiles[i].getName();
                     int k=i+1;
                     System.out.println(k+" "+name+"("+str+")");
                }
          }
    }
    
    

具体模板（Concrete Template）_2:ConcreteTemplate2.java 

    import java.io.*;
    import java.awt.*;
    public  class ConcreteTemplate2 extends  AbstractTemplate{
           ConcreteTemplate2(File dir){
               super(dir);
          }
          public void sort(){
               for(int i=0;i<allFiles.length;i++)
                    for(int j=i+1;j<allFiles.length;j++)
                          if(allFiles[j].length()<allFiles[i].length()){
                                File file=allFiles[j];
                                allFiles[j]=allFiles[i];
                                allFiles[i]=file;
                          }
          }
          public void printFiles(){
                 for(int i=0;i<allFiles.length;i++){
                     long fileSize=allFiles[i].length() ;
                     String name=allFiles[i].getName();
                     int k=i+1;
                     System.out.println(k+" "+name+"("+fileSize+" 字节)");
                }
          }
    }

应用 Application.java

    import java.io.File;
    public class Application{
         public static void main(String args[]) {
             File dir=new File("d:/javaExample");
             AbstractTemplate  template=new ConcreteTemplate1(dir);
             System.out.println(dir.getPath()+"目录下的文件：");
             template.showFileName();
             template=new ConcreteTemplate2(dir);
             System.out.println(dir.getPath()+"目录下的文件：");
             template.showFileName();
         }
    } 
    
    


