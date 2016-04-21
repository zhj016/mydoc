## Interpreter ( 解释器模式 ) ##

Interpreter Pattern 
  Given a language, define a representation for its grammar along with an interpreter
that uses the representation to interpret sentences in the language. 

解释模式是关于怎样实现一个简单语言的成熟模式，其关键是将每一个语法规则表示成一个类。 


###模式的结构中包括四种角色：###
* 抽象表达式（AbstractExpression） 
* 终结符表达式子（TerminalExpression） 
* 非终结符表达式子（NonterminalExpression） 
* 上下文（Context） 


###抽象表达式（AbstractExpression）: Node.java###
    
    public interface Node{
          public void parse(Context text);
          public void execute();
    } 


### 终结符表达式（TerminalExpression）_1: SubjectPronounOrNounNode.java ###
    
    public class SubjectPronounOrNounNode implements Node{
          String [] word={"You","He","Teacher","Student"};
          String token; 
          boolean boo;
          public void parse(Context context){
                 token=context.nextToken();
                 int i=0;
                 for(i=0;i<word.length;i++){
                    if(token.equalsIgnoreCase(word[i])){
                        boo=true;
                        break;
                    }
                 }
                 if(i==word.length)
                    boo=false;
          }
          public void execute(){
                if(boo){
                    if(token.equalsIgnoreCase(word[0]))
                        System.out.print("你"); 
                    if(token.equalsIgnoreCase(word[1]))
                        System.out.print("他"); 
                    if(token.equalsIgnoreCase(word[2]))
                       System.out.print("老师"); 
                    if(token.equalsIgnoreCase(word[3]))
                        System.out.print("学生"); 
                }
                else{
                     System.out.print(token+"(不是该语言中的语句)");
               }        
         }
    }
    


###终结符表达式（TerminalExpression）_2:ObjectPronounOrNounNode.java ###
    
    public class ObjectPronounOrNounNode implements Node{
          String [] word={"Me","Him","Tiger","Apple"};
          String token; 
          boolean boo;
          public void parse(Context context){
                 token=context.nextToken();
                 int i=0;
                 for(i=0;i<word.length;i++){
                    if(token.equalsIgnoreCase(word[i])){
                        boo=true;
                        break;
                    }
                 }
                 if(i==word.length)
                    boo=false;
          }
          public void execute(){
                if(boo){
                    if(token.equalsIgnoreCase(word[0]))
                        System.out.print("我"); 
                    if(token.equalsIgnoreCase(word[1]))
                        System.out.print("他"); 
                    if(token.equalsIgnoreCase(word[2]))
                       System.out.print("老虎"); 
                    if(token.equalsIgnoreCase(word[3]))
                        System.out.print("苹果"); 
                }
                else{
                    System.out.print(token+"(不是该语言中的语句)");
                }        
         }
    }
    
    

### 终结符表达式（TerminalExpression）_3:VerbNode.java ###
    
    public class VerbNode implements Node{
          String [] word={"Drink","Eat","Look","beat"};
          String token; 
          boolean boo;
          public void parse(Context context){
                 token=context.nextToken();
                 int i=0;
                 for(i=0;i<word.length;i++){
                    if(token.equalsIgnoreCase(word[i])){
                        boo=true;
                        break;
                    }
                 }
                 if(i==word.length)
                    boo=false;
          }
          public void execute(){
                if(boo){
                    if(token.equalsIgnoreCase(word[0]))
                        System.out.print("喝"); 
                    if(token.equalsIgnoreCase(word[1]))
                        System.out.print("吃"); 
                    if(token.equalsIgnoreCase(word[2]))
                       System.out.print("看"); 
                    if(token.equalsIgnoreCase(word[3]))
                        System.out.print("打"); 
                }
                else{
                   System.out.print(token+"(不是该语言中的语句)");
                }        
         }
    } 
    

### 非终结符表达式（TerminalExpression）_1:###
    
    SentenceNode.java 
    public class SentenceNode implements Node{
          Node subjectNode,predicateNode;
          public void parse(Context context){
                subjectNode =new SubjectNode();
                predicateNode=new PredicateNode();
                subjectNode.parse(context);
                predicateNode.parse(context);
          }
          public void execute(){
               subjectNode.execute();
               predicateNode.execute();
         }
    } 
    

###非终结符表达式（TerminalExpression）_2: SubjectNode.java###
    
    public class SubjectNode implements Node{
          Node node;
          public void parse(Context context){
                node =new SubjectPronounOrNounNode();
                node.parse(context);
         }
          public void execute(){
               node.execute();
         }
    }
    
### 非终结符表达式（TerminalExpression）_3: PredicateNode.java###
    
    public class PredicateNode implements Node{
          Node verbNode,objectNode;
          public void parse(Context context){
                verbNode =new VerbNode();
                objectNode=new ObjectNode();
                verbNode.parse(context);
                objectNode.parse(context);
          }
          public void execute(){
              verbNode.execute();
              objectNode.execute();
         }
    } 
    

###非终结符表达式（TerminalExpression）_4: ObjectNode.java###

    public class ObjectNode implements Node{
          Node node;
          public void parse(Context context){
                node =new ObjectPronounOrNounNode();
                node.parse(context);
         }
          public void execute(){
               node.execute();
         }
    }

###上下文（Context）:Context.java###

    
    import java.util.StringTokenizer;
    public class Context{
          StringTokenizer tokenizer;
          String token;
          public Context(String text){
               setContext(text);
         } 
         public void setContext(String text){
              tokenizer=new StringTokenizer(text);
         }
          String nextToken(){
                if(tokenizer.hasMoreTokens()){
                     token=tokenizer.nextToken(); 
               }
               else
                    token="";
               return token;
          } 
    }
    



###应用 Application.java###
    
    
    public class Application{
         public static void main(String args[]){
              String text="Teacher beat tiger";         
              Context context=new Context(text);
              Node node=new SentenceNode();
              node.parse(context);
              node.execute();
              text="You eat  apple";
              context.setContext(text);
              System.out.println();
              node.parse(context);
              node.execute();
               text="you look  him";
              context.setContext(text);
              System.out.println();
              node.parse(context);
              node.execute();
         }
    }
    
    
    
    