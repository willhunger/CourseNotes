## Deep Learning

### Ups and downs of Deep Learning

![1564194939427](assets/1564194939427.png)



### Three Steps for Deep Learning

#### Step 1 Neural Network

​	每一个logistics regression就是一个Neuron，不同的链接方式构成了不同的神经网络。

![1564194990212](assets/1564194990212.png)



​	Network连接的方式有多种，Fully Connect Feedforward Network是一种常见的方式。

​	![1564195133906](assets/1564195133906.png)

​	

​	如果不加参数，只定义Network的结构，就定义了一个function set。设定好参数就可以把network当成一个function。如下图。

​	![1564195459468](assets/1564195459468.png)

​	

​	由下图可见，这样就组成了一个神经网络。所谓的Deep，就是指有多个Layer。

​	![1564195553205](assets/1564195553205.png)



​	叠的层数越多，准确度就越高。

​	![1564195890928](assets/1564195890928.png)

​	

​	以下时各个Layer叠在一起时的具体操作。

​	![1564196023532](assets/1564196023532.png)

​	![1564196047192](assets/1564196047192.png)

​	![1564196058042](assets/1564196058042.png)

​	

​	至此，GPU进行矩阵运算的优势就显示出来了。

​	![1564196121216](assets/1564196121216.png)

​	具体例子有手写数字识别：

​	![1564196650286](assets/1564196650286.png)



​	那么还怎么具体决定Network的结构呢？

​	![1564196714437](assets/1564196714437.png)



#### Step 2 Goodness of function

​	首先计算Cross Entropy，然后计算Total Loss。

![1564207578023](assets/1564207578023.png)

![1564207589721](assets/1564207589721.png)



#### Step 3 Pick up the best function

​	仍然使用Gradient Descent的方法。

​	![1564207722580](assets/1564207722580.png)



### Universality Theorem

​	有理论说，任何一个连续函数，N维输入，M维输出，都可以用一个Network实现。

![1564207875019](assets/1564207875019.png)