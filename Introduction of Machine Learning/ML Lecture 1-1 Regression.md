## Regression

Regression 通过输出一个scalar(数量，标量)来达到预测，如股市预测，自动驾驶(根据路况改变方向盘角度)，商品推荐，这节课通过预测Pokemon精灵进化后的CP值为例讲解。

### Step1 Model

确定Model，即找到一个函数集。如Pokemon的例子，建立的函数有两个参数分别为w和b，首先假定进化后的CP值只和进化前的CP有关系。

![1563095339353](assets/1563095339353.png)

### Step2 Goodness of Function

准备好Training Data(例子中为10组Pokemon精灵的数据)，将这些数据建立好坐标轴。

![1563095528042](assets/1563095528042.png)

通过上图可知，我们想要找到一个函数来拟合这些坐标点，为了选出最好的函数，需要建立一个Loss Function来评估找到估计的误差，即函数的好坏。具体的Loss Function的定义如下图：

![1563095970345](assets/1563095970345.png)

​	

​	将函数f的w,b作为x,y轴，则在下图中每个点都代表了一个函数f,颜色的深度代表L(w,b)，即f的好坏。因此smallest点对于的函数f即为我们想要的最优解，如下图。

​	![1563096541083](assets/1563096541083.png)

### Step3 Best Function

1. 对于上一步骤中的smallest点对于的f为Best Function，可以用什么方法在Loss Function上找到这个函数呢？具体要怎么计算呢？

    一种方式是线性代数的基本方法来求w和b；另外一种是，当特征值多时，Gradient Descent(梯度下降)法来求。

    ​	![1563097101241](assets/1563097101241.png)

2. Gradient Descent

    当仅考虑一个参数w时，L(w)的分布如下图所示，需要在L(w)值最低点。具体操作步骤如下：

     1. 首先随机选取一个点w0，计算在该点处的微分（即斜率）。

     2. 如果计算的微分为正，则减小w值，否则，则增大f值。

     3. 具体的减少的w值由两个因素决定。

        * 微分值。如果微分值很大或很小，则表示此处的函数图像为陡峭处，那么距离最低点还有很大距离，故此时需要移动很大的距离。
        * 步长，即事先自主定义好的常数项η ，η 被称为learning rate(学习率)。

        ![1563097291864](assets/1563097291864.png)

    	4. 按照下公式，一直迭代，经过大量的参数更新，便能达到最低点。
        $$
        W^{1} \leftarrow W^{0} - η\frac{dL}{dw}|_{w=w_{0}}
        \\
        W^{2} \leftarrow W^{1} - η\frac{dL}{dw}|_{w=w_{1}}
        $$
        如果在这个过程中遇到某点w的微分为0（到达Local minimum），此时为Local optimal，但此时的并非最优解。但是在linear regression上，是不存Local minimum的。

        ​	![1563106565228](assets/1563106565228.png)

    

    当存在两个或多个参数时呢？反复进行下图步骤，最后就可以找到一个Loss比较小的w和b的值。

    Gradient 代表的就是下图红框的那个向量。

    ​	![1563107057053](assets/1563107057053.png)

    ​	是否会出现起始位置不一样，找到的最终位置不一样呢？如下图一样？

    ​	![1563107573538](assets/1563107573538.png)

    ​	答案是不会。在Linear regression中，仅仅存在一个坑，L为凸函数，不存在Local optimal。

    经过上面的Gradient Descent方法，最终能找到最佳f。

### How’s the results? - Generalization

通过上面的步骤，我们得到了最终的f，现在通过10组数据来检测结果如何。

如下图，比较Training Error和Testing Error便可以知道模型好坏。

![1563107945734](assets/1563107945734.png)

​	下面将模型换成二次方程，三次方程，四次方程...然后对比Training Error 和Testing Error。



​		![1563108422505](assets/1563108422505.png)

![1563108443961](assets/1563108443961.png)

​	![1563108482018](assets/1563108482018.png)

​	![1563108499335](assets/1563108499335.png)

​	通过对比方程的次数时，Training Error 越来越小，但是Testing Error却表现得更差了。这种情形被称为Overfitting(过拟合)。

​	![1563108798396](assets/1563108798396.png)

## More Data

如果模型要设计到更到的Pokemon物种呢？

1. 更加周全的设计覆盖其他物种的f

    ![1563109213421](assets/1563109213421.png)

2. 上述设计的f的testing error依然很大，因此还有因素影响，例如Pokemon精灵的体重，身高和HP值。重新设计了一个Model。然而testing error还是很高，overfitting了。

    ![1563109447107](assets/1563109447107.png)

3. 接下来通过Regularization来调整。

    我们更加期待平滑的函数，函数越平滑，受噪声影响也就越少。通过调整参数λ就能找到更平滑。

    在下图L中，未加入b参数，做Regularization的时候，不需要考虑bias，因为预期的是找到平滑的f，但是调整bias的值，并不能改变f的平滑程度，b只是上下移动f而已。

    ![1563109576347](assets/1563109576347.png)

    ![1563109633954](assets/1563109633954.png)

### Conclusion

Gradient descent，Overfitting，Regularization

参考资料：[[机器学习入门] 李宏毅机器学习笔记-2 （Regression：Case Study ；回归：案例研究）](https://blog.csdn.net/soulmeetliang/article/details/72619885)

