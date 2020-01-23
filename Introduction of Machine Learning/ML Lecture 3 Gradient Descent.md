## Gradient Descent

### Review

​	如下图，其中
$$
\nabla L(\theta)=\left[\begin{array}{ll}{\partial L\left(\theta_{1}\right) / \partial \theta_{1}} \\ {\partial L\left(\theta_{2}\right) / \partial \theta_{2}}\end{array}\right]
$$
​	代表Gradient，是个向量。



![1563528878967](assets/1563528878967.png)



​		Gradient Descent过程可视化如下图：



​			![1563529026721](assets/1563529026721.png)



### 三种梯度下降的方法

#### Tip1 Tuning your learning rates

​	Learning Rate太小，则到最低点的速度很慢；相反，Learning Rate太低的话，则永远在U形曲线两侧徘徊，永远无法到最低点，甚至出现Loss值越来越大的情况。



![1563529196040](assets/1563529196040.png)

  1. 动态调整Learning Rate

     * 简单且流行的方法是每隔几步都通过一些因子来改变Learning Rate。

         * 开始时，距离最低点很远，采用大的Learning Rate。

         * 经过数轮后，快要接近最低点，所以减少Learning Rate。

         * 例如：
             $$
             1 / \mathrm{t} \text { decay: } \eta^{t}=\eta / \sqrt{t+1}
             $$

     * Learning rate不能一直不变

         * 不同的参数可以设置不同的Learning rate。

  2. Adagrad

     将每个参数的Learning rate除以先前微分的均方根。

     如下图，η为Learning rate，g为微分值，σ为前一个参数w的微信的均方根。

     

     ![1563530114552](assets/1563530114552.png)

     

     这样操作以后，每次的Learning rate都不同，具体步骤如下图：

     

     ![1563530477934](assets/1563530477934.png)

     

     从上述步骤可知，Adagrad的表达可简化为：

     

     ![1563530573511](assets/1563530573511.png)

     

     Adagrad越到后面速度越来越慢，这是一个正常现象。

     Question：下图中，普通梯度下降方法中，g(微分)越大，下降速度走的越快。而在Adagrad方法中，Gradient越大，分子代表下降速度越快，分母则起相反效果，这不是矛盾吗？

     ![1563545081665](assets/1563545081665.png)

     解释如下：

     * 直观解释，Adagrad是为了强调反差效果。

         ![1563545634895](assets/1563545634895.png)

         

     * 正式解释

         * 当参数为一个时，如下图，例如一个二次函数，此时最好的Step可能是跟一次微分成正比，二次微分成反比。

             ![1563545851956](assets/1563545851956.png)

             

         * 当存在多个参数时，如下图，上述结论在跨参数时不成立，即微分值越大离最低点越远不一定成立

             ![1563546478687](assets/1563546478687.png)

             

             用一次微分来估计二次微分的大小，如下图，就是sample处很多点来求斜率。

             ![1563547877872](assets/1563547877872.png)

         

#### Tip2 Stochastic Gradient Descent

 让Training更快。

 在常规梯度下降方法中，计算Loss function时考虑所有的训练数据。

 在随机梯度下降方法中，则是每次只取一个xi数据，然后Loss只考虑现在的参数。

 ![1563548120025](assets/1563548120025.png)

 ![1563548472723](assets/1563548472723.png)

 从上图可知，设example总数为20个，常规方法时每计算一个example，就更新一次参数，做一次移动。（需要看完20个example再更新参数）。

 使用随机梯度下降法时，看到一个example就更新一次参数（每一个example就update一个参数）。

 即用常规方法走一步的时候，随机梯度下降已经走20步了。



#### Tip3 Feature Scaling

让不同的特征值具有相同的缩放程度。

![1563551926649](assets/1563551926649.png)

为什么要做Feature Scaling？

![1563588801448](assets/1563588801448.png)



上图左边，W1,W2做相同的变化，w1对loss时具有较小的微分，w1方向较为平滑；w2对y影响比较大， 所以对loss影响比较大，w2方向是比较尖的。

上图右边中，w1和w2对loss有差不多的影响力。

图左边，对X1,X2影响差别很大，更新参数更困难，并不是朝着最低点走，需要更多步才能到最低点。

图右边，从不同的起点开始，都向最低点移动，效率更高。



Scaling的常见方法：

![1563589530593](assets/1563589530593.png)



###   Gradient Descent Theory

1. Taylor Series

    ![1563590300208](assets/1563590300208.png)

    ![1563590494961](assets/1563590494961.png)

    

2. Multivariable Taylor Series

    ![1563590581989](assets/1563590581989.png)

    

3. Formal Derivation

    在红色圈中找最小到Loss最小的点，一直迭代下去，找到最小点为止。

    那么如何完成这个找Loss最小的点呢？

    ![1563590181647](assets/1563590181647.png)

    ​	将Loss function用泰勒级数做简化，如下图所示。

    ![1563590622563](assets/1563590622563.png)

    ![1563590748449](assets/1563590748449.png)

    

    ​	此时按照下图中的计算方法，可找到最小的Loss。

    ![1563590808685](assets/1563590808685.png)

    

    ​		此时，便可以推导出计算步骤就正好为gradient descent。（要求learning rate足够小，接近无穷小？）

    ![1563590957817](assets/1563590957817.png)

    ​	

### More Limitation of Gradient Descent

* 在梯度下降过程中，容易卡在Local Minimum的地方。

* 卡在saddle point的地方（微分值为0的地方）。

* 在Plateau处速度慢。

    ![1563591310498](assets/1563591310498.png)