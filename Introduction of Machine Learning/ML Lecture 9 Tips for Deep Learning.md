## Tips for Deep Learning

### Recipe of Deep Learning

Deep Learning中的主要流程如下图，但是判断Overfitting的方法如下：

当看到Training Error小而Testing Error比较大时，此时才为Overfitting（并不是单凭Testing Error判断）。

在试图解决overfitting之后仍要再看一下training set上的结果。

![1565491082115](assets/1565491082115.png)



当然，并不是所有的问题都能归结到Overfitting上，如下图，56层和20层神经网络训练出来的模型。

当只看右边坐标时，不能把56层神经网络视为Overfitting，因为此时并不知道Training Error的情况。

当两图对比看时，是发现56层的神经网络没能训练好的原因。（此时也不能视为Underfitting，Underfitting一般被认为是模型参数不够多，不足以解决问题）。

![1565491330377](assets/1565491330377.png)



所以，在对Deep Learning的实践过程中，要思考该方法时为了解决什么问题。解决在Training和Testing两个不同的阶段的问题的方法不同。例如，Dropout方法是为了解决在Testing set上表现不好的问题，如果误用到Training Set上结果只会更差。具体不同阶段的问题可用下图中的方法解决。

![1565508787454](assets/1565508787454.png)



#### 1. Vanishing Gradient Problem（梯度消失问题）

使用sigmoid function时会出现梯度消失的问题（参数的变化经过sigmoid会逐层衰减，对最后的loss影响很小），由下图Sigmoid function的图形可知。

![1565508907988](assets/1565508907988.png)

![1565508968325](assets/1565508968325.png)



用ReLU（计算快，相当于无数sigmoid叠加，解决梯度消失问题）。 
ReLU输出0或x，输出0的ReLU神经元相当于不存在，网络变得瘦长，但是整个网络仍然是非线性的，只有当input改变十分微小的时候才是线性的，因为input不同，输出为0的ReLU神经元也不同。

![1565509257347](assets/1565509257347.png)

![1565509308733](assets/1565509308733.png)



ReLU是Maxout的特例，Maxout可以自适应地学习激活函数。（Activation function，又称激励函数）

![1565509427628](assets/1565509427628.png)

![1565509445564](assets/1565509445564.png)

![1565509464272](assets/1565509464272.png)





#### 2. Adaptive Learning Rate （可调整的Learning Rate）

##### Adagrad

之前有介绍Adagrad方法可以来调整Learning Rate。但是Error Surface非常复杂时该方法失效。

![1565511167160](assets/1565511167160.png)

![1565511232618](assets/1565511232618.png)

##### RMSProp（Root Mean Square Prop）

上述情况情况下可使用RMSProp方法。

![1565511401659](assets/1565511401659.png)

α 小，则倾向于相信新的gradient。

此时，仍然存在下图中的问题：

![1565511597065](assets/1565511597065.png)



##### Momentum

借助物理学中的惯性的方法，如下图。

###### Vanilla Gradient Descent

![1565511689679](assets/1565511689679.png)

###### Momentum

Momentum方法在梯度下降过程中移动时考虑了上一步的移动方法，如下图。

![1565511720669](assets/1565511720669.png)

![1565511738102](assets/1565511738102.png)



此时使用Momentum方法后有可能跃过Local Minima。

![1565511834088](assets/1565511834088.png)

##### Adam (RMSProp + Momentum)

具体算法如下：

![1565512019825](assets/1565512019825.png)





#### 3. Early Stopping 

此处的Testing set指的是Validation Set。

如果Learning rate设得对的话，Training set的loss会逐渐降低，而Testing set和Training set的loss情况并不相同（testing set的loss图像可能为先降后升），这时不需要一直训练得到最小的traing error，而是在testing loss最小的地方停止训练。

![1565512191189](assets/1565512191189.png)



#### 4. Regularization

##### L2正则化

L2正则化可参考Ridge Regression（岭回归）。

L2正则化让function更平滑，而bias与函数平滑程度没有关系。

![1565512853560](assets/1565512853560.png)

此时，新的Loss function如下图。

![1565512943945](assets/1565512943945.png)

正则化在NN中虽有用但不明显。 
NN参数初始值一般接近0，update参数即是要参数原理0。L2正则化（让参数接近0）的作用可能与early stopping类似。



##### L1正则化

L1正则化可参考Lasso方法。

L1 update的速度是|ηλ|。而 L2 update 的速度与w^t 有关（如果w^t 很大，那么改变量也很大）。 

用L1做training，结果比较sparse，参数中有很多接近0的值，也有很多很大的值。 

L2 learn的结果：参数值平均来讲比较小。

![1565513020855](assets/1565513020855.png)



#### 4. Dropout

input layer中每个element也算是一个neuron. 
每次更新参数之前都要resample. 
用dropout，在training上的结果会变差，但在testing上的结果会变好。

![1565513294180](assets/1565513294180.png)



在testing的时候不做dropout，所有neuron都要用。 
如果training时dropout rate = p%, 得参数a, 那么testing时参数a要乘(1 - p%).

![1565513430020](assets/1565513430020.png)

![1565513596401](assets/1565513596401.png)





Dropout是ensemble的一种方式。 

一个复杂model, bias小但variance大，把多个复杂model ensemble起来，variance变小。 

每个dropout后的结构由一个batch来train，但是权重是共享的，每个权重是由多个batch 来train的。



![1565513670669](assets/1565513670669.png)



在testing的时候，把多个结构的结果取平均，与把所有参数乘以(1 - p%)，效果是近似的。 
Dropout用在ReLU、Maxout上效果较好。

![1565513740563](assets/1565513740563.png)



具体例子如下：

![1565513870691](assets/1565513870691.png)



