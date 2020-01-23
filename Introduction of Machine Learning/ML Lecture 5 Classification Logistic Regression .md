## Classification: Logistic Regression

### Logistic Regression Three Steps

1. Step 1: Function Set

    确定一个Function Set，里面有所有可能的w和b参数。

    

    ![1564038820766](assets/1564038820766.png)

    

2. Step 2: Goodness of a Function

    假设下图的training data是根据后验概率产生的，给定一组w和b的模型，就可以去计算某组w和b产生N笔training data的概率。依照下图的L(w,b)计算即可。最大的L(w,b)中的w* 和 b* 才是最大化概率的w和b。

    ![1564039003816](assets/1564039003816.png)

    

    下图做一个数学的转换。将找最大的L转换为找最小的，为了计算方便。同时如果x属于class 1，则y^为1，否则为0。

    ![1564039433454](assets/1564039433454.png)

    

    cross entropy代表的是两个分布的距离。

    ![1564039746257](assets/1564039746257.png)

    我们希望function的output和traget(如果看作是伯努利分布的话)，希望这两个越接近越好。

    

3. Step 3: Find the best function

    怎么找到最好的function呢，用gradient descent就好。数学推导如下图。

    ![1564040022709](assets/1564040022709.png)

    

    ![1564040158182](assets/1564040158182.png)

    

    ![1564040197842](assets/1564040197842.png)

    

    上图紫色标注的数学式代表了现在f的output和理想目标的差距大小。



### Logistic Regression v.s. Linear Regression

![1564040392507](assets/1564040392507.png)



### Logistic Regression + Square Error

![1564040588555](assets/1564040588555.png)

![1564040604233](assets/1564040604233.png)

上图底部，无论据目标很远还是很近，微分算出来都是0。

下图是Cross Entropy和Square Error的Loss和参数的变化。

Cross Entropy在距离目标近的地方微分值很小，距离目标越远微分值越大。

但是选择Square Error时，离目标远的时候，微分值也很小，参数update特别慢，卡在附件。

那又来了一个问题，为什么在Square Error方法时看到微分值很小的时候，就把Learning rate调大一点啊。答案是：如果微分值很小，也可能距离目标值很近。现在不好确定的是，不知道微分值小的时候，距离目标近还是远。

所以，一般选择Cross Entropy好。

![1564040718906](assets/1564040718906.png)



### Discriminative v.s. Generative

使用Logistic Regression称为Discriminaive方法。上一节中的用Gaussian来描述posterior probability称为Generative方法。实际上，这两者的Model function是一模一样的，但是找出来的参数w和b是不一样的。

![1564041311569](assets/1564041311569.png)

![1564041485175](assets/1564041485175.png)

但是Discriminative比Generative结果更为好一些。

具体例子如下：

![1564041562221](assets/1564041562221.png)

![1564041588194](assets/1564041588194.png)

![1564041619171](assets/1564041619171.png)

然而结果小于0.5，朴素贝叶斯方法倾向于选择Class2，与事实不符合。

![1564041797165](assets/1564041797165.png)

* Generative在Training data越少的情况下更为适用。Discriminative受数据量影响较大。
* Generative能脑补，可以把data中有问题的部分忽视掉。
* 在做Disctiminative model时是假设了一个posterior probability，然后去找其中的参数。但是在做generative model的时候，是拆成了prior probability 和 class-depender probability两项，这样做有时候是用好处的，因为prior probability 和 class-depender probability可是是来自不同的来源。以语音辨识为例，prior probability并不需要声音，只需要去网络上爬虫计算某一段文字出现的概率。



### Multi-class Classification

![1564042426091](assets/1564042426091.png)

softmax的output就是拿来当z的posterior probability。

![1564042455775](assets/1564042455775.png)

### Limitation of Logistic Regression

下图的例子中，我们无法使用Logistic Regression对下图来进行分类。因为Logistic Regression的boundary为一条直线，无论在下图中怎么画，也无法画一条直线区分边界。

![1564042824091](assets/1564042824091.png)



我们可以用Feature Transformation来解决。

![1564042970676](assets/1564042970676.png)



怎么让机器自己产生一个好的transformation呢？

![1564043041893](assets/1564043041893.png)

上面的例子使用新方法后：

![1564043112971](assets/1564043112971.png)

![1564043236688](assets/1564043236688.png)

![1564043404840](assets/1564043404840.png)

把Logistics 叫做一个neuron，把这些Logistic 串起来，就是Neural Network。



### Reference

[交叉熵（Cross-Entropy）](https://blog.csdn.net/rtygbwwwerr/article/details/50778098)

[为什么交叉熵（cross-entropy）可以用于计算代价？](https://www.zhihu.com/question/65288314)

[softmax和cross-entropy是什么关系？](https://www.zhihu.com/question/294679135)

