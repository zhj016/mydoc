## Strategy ( 策略模式 ) ##

* 策略模式针对一组算法，将每一个算法封装到具有共同接口的独立的类中，从而使得它们可以相互替换。
* 策略模式使得算法可以在不影响到客户端的情况下发生变化。
* 策略模式把行为和环境分开。环境类负责维持和查询行为类，
* 各种算法在具体的策略类中提供。由于算法和环境独立开来，算法的增减，修改都不会影响到环境和客户端。 



###在此写了7个java类来描述说明Strategy设计模式:###

1. SortStrategy.java  排序算法策略接口
2. SortBin.java  二分法排序
3. SortBubble.java 冒泡排序
4. SortHeap.java  堆排序
5. SortQuick.java 快速排序
6. Sorter.java 排序算法使用者
7. SortTest.java  带有main方法的测试类