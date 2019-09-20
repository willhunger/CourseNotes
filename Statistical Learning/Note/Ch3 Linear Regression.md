## Linear Regression

### 1. Simple Linear Regression

1. 仅有一个参数X的简单线性回归

    首先假定一个模型如下：
    $$
    Y=\beta_{0}+\beta_{1} X+\epsilon
    $$
    β0和β1是两个未知的常量，分布代表截距和斜率

    可用下面的公式来估计参数：
    $$
    \hat{y}=\hat{\beta}_{0}+\hat{\beta}_{1} x
    $$
    
2. 最小二乘法估计参数

    根据变量X的第i个值，用上式来估计Y。

    1. 根据残差公式：

    $$
    e_{i}=y_{i}-\hat{y}_{i}
    $$

    ​	i代表第i个残差，即第i个观察到的响应值和第i个用线性模型测出的响应值之间的差距。

    ​	定义残差平方和（residual sum of squares，RSS）为：
    $$
    \mathrm{RSS}=e_{1}^{2}+e_{2}^{2}+\cdots+e_{n}^{2}
    \\
    \mathrm{RSS}=\left(y_{1}-\hat{\beta}_{0}-\hat{\beta}_{1} x_{1}\right)^{2}+\left(y_{2}-\hat{\beta}_{0}-\hat{\beta}_{1} x_{2}\right)^{2}+\ldots+\left(y_{n}-\hat{\beta}_{0}-\hat{\beta}_{1} x_{n}\right)^{2}
    $$

    2. 最小二乘法通过选择β0和β1来使得RSS达到最小，如下：
        $$
        \begin{aligned} \hat{\beta}_{1} &=\frac{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)\left(y_{i}-\overline{y}\right)}{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)^{2}} 
        \\ 
        \hat{\beta}_{0} &=\overline{y}-\hat{\beta}_{1} \overline{x} \end{aligned}
        \\
        \overline{y}和\overline{x}为样本均值
        $$

    

3. 衡量参数准确性

    1. 标准差衡量参数估计值与参数值
        $$
        \begin{array}{l}{\operatorname{SE}\left(\hat{\beta}_{1}\right)^{2}=\frac{\sigma^{2}}{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)^{2}}, \quad \operatorname{SE}\left(\hat{\beta}_{0}\right)^{2}=\sigma^{2}\left[\frac{1}{n}+\frac{\overline{x}^{2}}{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)^{2}}\right]} 
        \\ 
        {\text { where } \sigma^{2}=\operatorname{Var}(\epsilon)}\end{array}
        $$
        σ方代表Var(ϵ)，对其的估计为残差标准误（residual standard error），定义为：
        $$
        R S E=\sqrt{R S S /(n-2)}
        $$

    2. 置信区间（confidence intervals）

        标准误差可用于计算置信区间。95%的置信区间被定义为一个取值范围：该范围内有95%的概率会包含未知参数的真实值。

        对于线性回归模型，β1的95%的置信区间约为：
        $$
        \hat{\beta}_{1} \pm 2 \cdot \operatorname{SE}\left(\hat{\beta}_{1}\right)
        $$
        也就是说，这个区间中，
        $$
        \left[\hat{\beta}_{1}-2 \cdot \operatorname{SE}\left(\hat{\beta}_{1}\right), \hat{\beta}_{1}+2 \cdot \operatorname{SE}\left(\hat{\beta}_{1}\right)\right]
        $$
        有约95%的可能会包含β1的真实值。

        
    

### 2. Hypothesis Testing and Confidence Intervals 

​	标准误差也能用来对系数进行假设检验。最常用的假设检验包括

​	零假设(null hypothesis) : H0：X和Y之间没有关系

​	备择假设(alternative hypothesis)：Ha：X和Y之间有一定的关系

1. 从数学角度上讲，是为了检验：
    $$
    \begin{array}{c}{H_{0} : \beta_{1}=0} 
    {\text { versus }} 
    {\qquad H_{A} : \beta_{1} \neq 0}\end{array}
    $$
    如果β1为0，模型就变成
    $$
    Y=\beta_{0}+\epsilon
    $$
    X和Y就不相关了。

2. 为了检验零假设，需要计算t统计量（t-statistic）：
    $$
    t=\frac{\hat{\beta}_{1}-0}{\operatorname{SE}\left(\hat{\beta}_{1}\right)}
    $$
    如果β1为0，那么上式将服从自由度为n-2的t分布。

3. p值（p-value）

    观测值大于等于|t|的概率。

4. 评价模型的准确性

    * RSE反映响应值会偏离真正的回归直线额平均量，即对模型失拟(lack of fit)的度量。
        $$
        \mathrm{RSE}=\sqrt{\frac{1}{n-2} \mathrm{RSS}}=\sqrt{\frac{1}{n-2} \sum_{i=1}^{n}\left(y_{i}-\hat{y}_{i}\right)^{2}}
        \\
        \mathrm{RSS}=\sum_{i=1}^{n}\left(y_{i}-\hat{y}_{i}\right)^{2}
        $$

    * R²统计量
        $$
        R^{2}=\frac{\mathrm{TSS}-\mathrm{RSS}}{\mathrm{TSS}}=1-\frac{\mathrm{RSS}}{\mathrm{TSS}}
        \\
        \text{其中TSS是总平方和，即Y的Variance(总方差),}
        \mathrm{TSS}=\sum\left(y_{i}-\overline{y}\right)^{2}
        $$
        R²测量的是Y的变异中能被X解释的部分所占比例。R²统计量接近1说明回归可以解释响应变量的大部分变异。R²统计量接近0说明回归没有解释太多响应变量的变异，这可能因为线性模型是错误的，也可能因为固有误差项σ2较大，抑或两者兼有。

        同样，相关性(Correlation)的定义为：
        $$
        \operatorname{Cor}(X, Y)=\frac{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)\left(y_{i}-\overline{y}\right)}{\sqrt{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)^{2}} \sqrt{\sum_{i=1}^{n}\left(y_{i}-\overline{y}\right)^{2}}}
        $$
        相关性也衡量了X和Y之间的线性关系。这意味着r=Cor(X，Y)可以代替R²评估线性模型的拟合度。

        事实上，在简单线性回归模型中，R²= r² 。换言之，相关系数的平方与R²统计量相等。



### 3. Multiple Linear Regression

1. 多元线性回归：
    $$
    Y=\beta_{0}+\beta_{1} X_{1}+\beta_{2} X_{2}+\cdots+\beta_{p} X_{p}+\epsilon
    $$
    βj可解释为在所有其他变量不变化的情况，Xj增加的一个单位对Y产生的平均效果。

    预测变量之间的相关性可能导致的问题：

    - 所有参数的方差可能增大
    - 模型可解释性降低，因为当Xj改变时，其余变量也可能同时改变

2. 估计回归参数

    最小二乘法，选择多个参数使得残差平方和最小。
    $$
    \begin{aligned} \mathrm{RSS} &=\sum_{i=1}^{n}\left(y_{i}-\hat{y}_{i}\right)^{2} \\ &=\sum_{i=1}^{n}\left(y_{i}-\hat{\beta}_{0}-\hat{\beta}_{1} x_{i 1}-\hat{\beta}_{2} x_{i 2}-\cdots-\hat{\beta}_{p} x_{i p}\right)^{2} \end{aligned}
    $$
    

### 4. Some important questions

一些要探讨的问题如下：

* 预测变量X1，X2，...，Xp中是否至少有一个可以用来预测响应变量？
* 所有预测变量都有助于解释Y吗?或仅仅是预测变量的一个子集对预测有用？
* 模型对数据的拟合程度如何?
* 给定一组预测变量的值，响应值应预测为多少?所作预测的准确程度如何?

解决方法如下：

1. 响应变量和假设变量之前是否存在关系？

    用检验假设来回答。

    检验零假设为：H0: β1 = β2 = β3  = βP = 0;

    对应的备择假设为：Ha：至少有一个βj不为0

    用下面公式计算F统计量：
    $$
    F=\frac{(\mathrm{TSS}-\mathrm{RSS}) / p}{\mathrm{RSS} /(n-p-1)} \sim F_{p, n-p-1}
    $$
    如果线性关系存在，则
    $$
    E\{\mathrm{RSS} /(n-p-1)\}=\sigma^{2}
    $$
    如果线性关系不存在，则
    $$
    E\{(\mathrm{TSS}-\mathrm{RSS}) / p\}=\sigma^{2}
    $$
    为什么不用各个变量的P值而要看整体的F统计量呢？

    因为F统计量和p和n都有关系，它会根据预测变量的个数进行调整。

    注：F检定一般适用于p < n的情况。若p > n,则待估系数βj的个数比可用于估计的观测个数还多。这种情况下，不能用最小二乘法拟合多元线性模型，所以不能使用F统计量。可选择使用向前选择。

2. 选定重要变量

    理想情况下可通过尝试不同的模型来进行变量选择，每种模型包括不同变量的自己。但是这种方法受限于变量个数。

    * 向前选择（forward selection）：从零模型开始开始建立线性回归模型，每次加入RSS最小的变量，直至RSS小于一定范围。
    * 向后选择（backward selection）：从包含所有变量的模型开始，移除p值最高的变量，知道满足某种规则。
    * 混合选择（mixed selection）：综合以上两种方法，从零模型开始，不断加入变量，但是加入的同时注意每个变量的p值，保留小于一定阈值的p值对应的变量，去除高于一定阈值的p值对应的变量，直至遍历所有变量。

3. 模型拟合

    R²和RSE

4. 预测

    预测的三类不确定性：

    * 系数β估计的不确定性，与可约误差相关。
    * 模型偏差
    * 随机误差ϵ，即不可约误差。



### 5. Extensions of the linear model

1. 定性预测变量

    设置哑变量（dummy variable），定性预测变量有n nn个水平，则需要创建n−1 n-1n−1个哑变量。

2. 线性模型的扩展

    1. 去除可加性假设

        预测变量之间可能存在交互作用(interaction)。

        考虑两个变量的标准线性回归模型：
        $$
        Y=\beta_{0}+\beta_{1} X_{1}+\beta_{2} X_{2}+\epsilon
        $$
        解决方法是加入第三个变量，名为交互项（interaction term），交互项由X1和X2的乘积构成。

        加入后，可得到模型：
        $$
        Y=\beta_{0}+\beta_{1} X_{1}+\beta_{2} X_{2}+\beta_{3} X_{1} X_{2}+\epsilon
        \\
        =\beta_{0}+\left(\beta_{1}+\beta_{3} X_{2}\right) X_{1}+\beta_{2} X_{2}+\epsilon
        \\
        =\beta_{0}+\tilde{\beta}_{1} X_{1}+\beta_{2} X_{2}+\epsilon
        $$
        实验分层原则(hierarchical principle)规定，如果模型中含有交互项，那么即使主效应的系数的p值不显著，也应包含在模型中。也就是，如果X1和X2具之间的交互作用是重要的，那么即使X1和X2的系数估计的p值较大，这两个变量也应该被包含在模型中。

    2. 非线性关系

        扩展线性模型的方法有：多项式回归(polynomial regression)。

    

    

    

    

### 6. 潜在问题

1. 非线性的响应-预测关系

    用残差图来识别非线性，如存在非线性关系，可在模型中使用预测变量的非线性变化。

2. 误差项自相关

3. 误差项方差非恒定

    线性回归模型的另一个重要假设是误差项的方差是恒定的。线性模型中的假设检验和标准误差、置信区间的计算都依赖于这一假设。

    如果残差图**呈漏斗形(funnel shape)** ，说明误差项方差非恒定或存在**异方差性(heteroscedasticity )**。

    可用加权最小二乘法拟合模型。

4. 离群点

    指Yi远离模型预测值的点。绘制学生会残差图估计。

5. 高杠杆点

    观测点Xi是异常的。

    在简单线性回归中容易辨识高杠杆观测，但是多元线性回归并不明显。

    计算杠杆统计量（leverage statistic）：
    $$
    h_{i}=\frac{1}{n}+\frac{\left(x_{i}-\overline{x}\right)^{2}}{\sum_{i^{\prime}=1}^{n}\left(x_{i^{\prime}}-\overline{x}\right)^{2}}
    $$
    一个大的杠杆统计量对于一个高杠杆点。

6. 共线性

    共线性(collinearity)是指两个或更多的预测变量高度相关。

    共线性降低了回归系数估计的准确性，会导致参数估计值的标准误变大。

    检测共线性的一个简单方法是看预测变量的相关系数矩阵。

    对于多重共线性的评估，使用方差膨胀因子（variance inflation factor, VIF）：
    $$
    \operatorname{VIF}\left(\hat{\beta}_{j}\right)=\frac{1}{1-R_{X_{j}| X_{-j}}^{2}}
    $$
    VIF的最小可能是1，表示完全不存在共线性。通常情况下，VIF超过5或10就有共线问题。

    解决方法有：剔除一个变量或者把共线向量组合成一个单一的预测变量。