## Iterator ( 迭代器模式 ) ##


GOF给出的定义为：提供一种方法访问一个容器（container）对象中各个元素，而又不 
                     需暴露该对象的内部细节。 

    
    Iterator it = list.iterator();
    while(it.hasNext())
    {
    　//using “it.next();”do some businesss logic
    }