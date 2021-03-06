---
title: 数据降维 & PCA
date: "2018-12-06 13:30:00"
categories:
- 机器学习
- 机器学习
tags:
- 非监督学习
- PCA
- 机器学习
toc: true
typora-root-url: ..\..\..
---

### 1. 数据降维

#### 数据降维目的

数据降维是对数据进行压缩的一个强有力的工具，也是一个非监督学习算法。有几个不同的原因可能会让我们在进行建模的过程中对数据进行降维处理，一、数据压缩，不仅能让我们的数据占用比较少的计算机资源(硬盘、内存), 还可以通过减少特征的方式，来让我们的机器学习算法运行的更加快速;  二、数据可视化， 当数据的特征特别多的时候，我们没有可视化的方案，将一个多维的数据进行可视化展示，但是我们可以通过PCA来将数据进行压缩成维度比较少的形式，再进行展示；

#### 什么是数据降维

![1544076335965](/img/1544076335965.png)

这里按照一个将二维的数据降维成一维来进行举例：

假设我们的数据有两个特征: x1： 长度， 单位是cm ； x2：是用英寸表示的同一个物体的长度。

所以，这两个特征给了我们高度冗余表示，两个特征基本上用一个就可以表示了一个实例的长度特征，所以我们可以通过降维来减少这两个特征造成的冗余；

将数据从二维降至一维： 假使我们要采用两种不同的仪器来测量一些东西的尺寸，其中一个仪器测量结果的单位是英寸，另一个仪器测量的结果是厘米，我们希望将测量的结果作为我们机器学习的特征。现在的问题的是，两种仪器对同一个东西测量的结果不完全相等（由于误差、精度等），而将两者都作为特征有些重复，因而，我们希望将这个二维的数据降至一维。

> 将我们的数据集的特征减少冗余，在保持误差基本不变的情况，减少特征的数量，这就是数据的降维；

### 2.数据压缩

下面介绍将冗余数据进行压缩的方法

**将二维数据降维至一维**:

![1544077545143](/img/1544077545143.png)

假设我们有这样一批特征，x1为学生学习的积极程度， x2为学生知识的掌握程度，这两个特征可能都可以代表学生的学习成果。所以，相比这两种特征，我们可能更倾向于获得特征--学生的知识掌握程度z, 来代替x1， x2两个特征。所以，我们真正关心的，可能是上面那条红色的线的方向，以及特征映射到其上的点，代表学生的知识量;

![1544077883986](/img/1544077883986.png)

上面这幅图表示，将二维数据降维成一位数据的过程

**将三维数据降维至二维:**

过程是与上面类似的，我们将三维向量投射到一个二维的平面上，强迫使得所有的数据都在同一个平面上，降至二维的特征向量。

![1544078620734](/img/1544078620734.png)

这样的处理过程可以被用于把任何维度的数据降到任何想要的维度，例如将1000维的特征降至100维。

### 3.数据可视化

在许多及其学习问题中，如果我们能将数据可视化，我们便能寻找到一个更好的解决方案，降维可以帮助我们。

![1544078716089](/img/1544078716089.png)

假使我们有有关于许多不同国家的数据，每一个特征向量都有50个特征（如GDP，人均GDP，平均寿命等）。如果要将这个50维的数据可视化是不可能的。使用降维的方法将其降至2维，我们便可以将其可视化了。

![1544078737110](/img/1544078737110.png)

这样做的问题在于，降维的算法只负责减少维数，新产生的特征的意义就必须由我们自己去发现了。

###  4.主成分分析问题

**主成分分析(PCA)**是最常见的降维算法。
在PCA中，我们要做的是找到一个方向向量（Vector direction），当我们把所有的数据都投射到该向量上时，我们希望投射平均均方误差能尽可能地小。方向向量是一个经过原点的向量，而投射误差是从特征向量向该方向向量作垂线的长度。

![1544079226723](/img/1544079226723.png)



**主成分分析问题的描述：**
问题是要将维数据降至 k 维，目标是找到向量$u^{(i)}, u^{(2)}, ...., u^{(k)}$, 使得所有的实例到向量的总的投射误差最小。

**主成分分析与线性回顾的比较：**
主成分分析与线性回归是两种不同的算法。主成分分析最小化的是投射误差（Projected Error），而线性回归尝试的是最小化预测误差。线性回归的目的是预测结果，而主成分分析不作任何预测。

![1544079761340](/img/1544079761340.png)

上图中，左边的是线性回归的误差（垂直于横轴投影），右边则是主要成分分析的误差（垂直于红线投影）。

PCA将n个特征降维到k个，可以用来进行数据压缩，如果100维的向量最后可以用10维来表示，那么压缩率为90%。但PCA 要保证降维后，还要保证数据的特性损失最小。

PCA技术的一大好处是对数据进行降维的处理。我们可以对新求出的“主元”向量的重要性进行排序，根据需要取前面最重要的部分，将后面的维数省去，可以达到降维从而简化模型或是对数据进行压缩的效果。同时最大程度的保持了原有数据的信息。

**PCA的优点**

PCA技术的一个很大的优点是，它是完全无参数限制的。在PCA的计算过程中完全不需要人为的设定参数或是根据任何经验模型对计算进行干预，最后的结果只与数据相关，与用户是独立的。

**PCA的缺点**

如果用户对观测对象有一定的先验知识，掌握了数据的一些特征，本可以根据经验做一些数据的整合或降维，但使用PCA却无法通过参数化等方法对处理过程进行干预，可能会得不到预期的效果，效率也不高。

###  5.主成分分析算法

PCA 减少n维到k维：
第一步是均值归一化。我们需要计算出所有特征的均值，然后令 $x_j = x_j - u_j$。如果特征是在不同的数量级上，我们还需要将其除以标准差 $\sigma^2$ 。
第二步是计算协方差矩阵（covariance matrix） $\Sigma : \sum = \frac { 1 } { m } \sum _ { i - 1 } ^ { n } \left( x ^ { ( i ) } \right) \left( x ^ { ( i ) } \right) ^ { T }$
第三步是计算协方差矩阵$\Sigma$的特征向量（eigenvectors）:
在 Octave 里我们可以利用奇异值分解（singular value decomposition）来求解，`[U, S, V]= svd(sigma)` 。

![1544081181351](/img/1544081181351.png)

对于一个n*n 维度的矩阵，上式中的U是一个具有与数据之间最小投射误差的方向向量构成的矩阵。如果我们希望将数据从n维降至k维，我们只需要从U中选取前k个向量，获得一个维度的n * k矩阵，我们用$U_{reduce}$表示，然后通过如下计算获得要求的新特征向量:$z ^ { ( i ) } : z ^ { ( i ) } = U _ {reduce} ^ { T } * x ^ { ( i ) }$

其中x是 n * 1 维的， 因此结果为 K * 1 维度的；

### 6.选择主成分的数量

主要成分分析是减少投射的平均均方误差：
训练集(经过均值归一化处理后)的方差为: $\frac { 1 } { m } \sum _ { i = 1 } ^ { m } \left\| x ^ { ( i ) } \right\| ^ { 2 }$

我们希望在平均均方误差与训练集方差的比例尽可能小的情况下选择尽可能小的值。

如果我们希望这个比例小于1%，就意味着原本数据的偏差有99%都保留下来了，如果我们选择保留95%的偏差，便能非常显著地降低模型中特征的维度了, 一般这个值最好不要小于90%， 因为那样数据可能就偏离原数据太多了。

**进行主成分选择的步骤(第一种方法):**

1. 我们可以先令k = 1，然后进行主要成分分析，获得$U_{reduce}$和z，然后计算比例是否小于1%;
2. 如果不是的话再令k = K + 1，如此类推，直到找到可以使得比例小于1%的最小 值;

**进行主成分选择的步骤(第二种方法):**

1. 我们可以先令k = 1，然后进行主要成分分析，获得$U_{reduce}$， S , 然后计算平均均方误差与训练集的比例

   备注： S是一个n * n的矩阵，只有对角线上有值，而其它单元都是0，我们可以使用这个矩阵来计算平均均方误差与训练集方差的比例

   ![1544082789155](/img/1544082789155.png)

   计算平均均方误差与训练集的比例公式: 

   ![1544082956382](/img/1544082956382.png)

2. 如果比例大于1%,再令k = K + 1，如此类推，直到找到可以使得比例小于1%的最小 值;

### 7. 重建被压缩的数据

PCA作为压缩算法。在那里你可能需要把1000维的数据压缩100维特征，或具有三维数据压缩到一二维表示。所以，如果这是一个压缩算法，应该能回到这个压缩表示，回到你原有的高维数据的一种近似。

所以， 给定$z^{(i)}$, 可能是100维， 怎么回到原来的$x^{(i)}$, 可能是1000维的数据；

![1544083598999](/img/1544083598999.png)

PCA算法，我们可能有一个这样的样本。如图中样本 $x^{(1)}, x^{(2)}$, 。我们做的是，我们把这些样本投射到图中这个一维平面。然后现在我们需要只使用一个实数，比如 $z^{(1)}$，指定这些点的位置后他们被投射到这一个三维曲面。给定一个点$z^{(1)}$，我们怎么能回去这个原始的二维空间呢？ 为2维，z为1维，$z = U^T_{reduce}x$ ，相反的方程为：$x_{appoz } = U_{reduce} * z$, $x_{appox} \approx x$ 。如图：

![1544083802962](/img/1544083802962.png)

通过以上的步骤得到的数据与原始数据相当相似。所以，这就是你从低维表示z回到未压缩的表示。我们得到的数据和原始数据x非常近似 ，我们也把这个过程称为重建原始数据。但是没有方法可以将数据从低维，没有偏差的还原到高纬。

### 8.PCA使用的总结

**使用PCA的数据进行建模的步骤:**

1. 运用主要成分分析将数据压缩到K个特征
2. 然后对训练集进行训练
3. 在预测或者交叉验证时，采用之前学习而来的$U_{reduce}$， 将输入的特征x转换成特征向量z， 然后在进行预测；

**不要在一下情况使用PCA**

1. 将其用于减少过拟合（减少了特征的数量）。这样做非常不好，不如尝试正则化处理。原因在于主要成分分析只是近似地丢弃掉一些特征，它并不考虑任何与结果变量有关的信息，因此可能会丢失非常重要的特征。然而当我们进行正则化处理时，会考虑到结果变量，不会丢掉重要的数据。
2. 不考虑为什么使用PCA，默认地将主要成分分析作为学习过程中的一部分，这虽然很多时候有效果，最好还是从所有
   原始特征开始，只在有必要的时候（算法运行太慢或者占用太多内存）才考虑采用主要成分分析。

> 总结: PCA如果不是想加快训练速度， 减少资源消耗，没必要使用， 其只可能降低数据信息量， 更要注意，千万不要用PCA来防止过拟合；如果使用， 通过平均均方误差与训练集的比例来确定特征数量K；