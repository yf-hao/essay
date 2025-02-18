前面学习的算法都是监督学习，而今天我们将开始学习无监督学习：
- clustering（k-means）
- mixture  of Gaussian （混合高斯）
- Jensen's inequality
- EM(Expectation Maximization)

接下来，我们简短的介绍下K-means算法。

在将监督学习的时候，经常会画一副这样的图：
![](https://raw.githubusercontent.com/fray-hao/images/master/20190401120800.png)
使用逻辑回归、svm等算法时，会根据每个样本的标签（正负）进行分类。所以叫做监督学习。
监督学习的训练样本可以统一成如下形式，其中x为变量，y为标记:
$$
\text{Training set:}\begin{Bmatrix}
    (x^{(1)},y^{(1)}),  (x^{(2)},y^{(2)}),...,  (x^{(m)},y^{(m)})
\end{Bmatrix}
$$

而无监督学习研究的是不同的问题。给定若干个点（样本）构成的数据集合，所有的点没有像监督学习那样给出类标签或者所谓的正确答案，我们需要靠算法本身，来发现数据中的结构。数据集的形式如下：
![](https://raw.githubusercontent.com/fray-hao/images/master/20190401121317.png)

显然，现实生活中不是所有数据都带有标记(或者说标记是未知的)。所以我们需要对无标记的训练样本进行学习，来揭示数据的内在性质及规律。我们把这种学习称为无监督学习(Unsupervised Learning)。所以，无监督学习的训练样本如下形式，它仅包含特征量。
$$
\text{Training set:}\begin{Bmatrix}
    x^{(1)},x^{(2)},...x^{(m)}
\end{Bmatrix}
$$

k-均值聚类是一种最常见的无监督的聚类算法，该算法对没有标签的数据集进行训练，然后将数据集聚类成不同的类别。 

聚类的基本思想是将数据集中的样本划分为若干个通常是不相交的子集，每个子集称为一个"簇"(cluster)。划分后，每个簇可能有对应的概念(性质)，比如根据页数，句长等特征量给论文做簇数为2的聚类，可能得到一个大部分是包含硕士毕业论文的簇，另一个大部分是包含学士毕业论文的簇。
## 1. 算法步骤

该算法的步骤：
1. 随机初始化K个样本(点)，称之为簇中心(cluster centroids)：
   $$\mu_1,\mu_2,...\mu_k\in \mathbb{R}^n$$
2. 簇分配：对于数据集中的每个数据计算与K个聚类中心的距离，将其与距离最近的聚类中心关联起来，将属于同一个聚类中心的样本聚成一类（也叫作簇）
   $$c^{(i)}:=\arg\min_j||x^{(i)}-\mu_j||$$
    >其中$c^{(i)}$为代表$x^{(i)}$被分配的聚类的索引值，$c^{(i)}\in\{1,2,....k\}$
3. 移动簇中心：对于每一个簇，计算属于该簇的所有样本的平均值，移动簇中心到平均值处
   $$
   \mu_j:=\frac{\sum_{i=1}^m1\{c^{(i)}=j\}x^{(i)}}{\sum_{i=1}^n1\{c^{(i)}=j\}}
   $$
4. 重复步骤2和3，直到找到我们想要的簇

下图演示了以特征量个数和簇数K均为2的情况。
![](https://gitee.com/hyfdbd/img/raw/master/788978-20160515010206539-637882739.gif)

该算法的伪代码如下：
![](https://raw.githubusercontent.com/fray-hao/images/master/20190402090857.png)

## 2.优化目标
首先，我们定义代价函数（也称为失真函数（distortion function））。
1. 能够帮助我们调试学习算法，确保k均值聚类算法是在正确运行中，确保其能收敛 


$$
J(c,\mu) = \frac{1}{m}\sum_{i=1}^m||x^{(i)}-\mu_{c^{(i)}}||^2
$$
k-means算法实际上就是函数J的坐标上升过程。我们从上述的k-均值的伪代码中来分析一下这个过程。
第一个循环是用于对每个样本进行簇分类，，它是用于减少$c_(i)$引起的代价，也就是固定$\mu$，令$c_(i)$最小化：
$$
\min J(c)
$$ 
第二个循环是用于移动聚类中心的位置，它是用来减小$μ_i$引起的代价，也就是固定c,令$u$最小化：
$$
\min J(\mu)
$$

所以我们的优化目标就是:
$$
\min_{c,\mu}J(c,\mu)
$$

## 3. 随机初始化方法

k-means算法不是凸函数，所以有可能得到局部最优值。为了避免找不到全局最优值，可以使一些随机初始化簇中心的方法。

## 异常检测与混合高斯模型

接下来讲一下密度估计（density estimation）。假设你要检测从组装线上生产出的飞机引擎。你会检测它们的各种属性，出于简化，我们只考虑两个属性：heat（发热）、vibrations（振动）。得到这样的数据集合：
![](https://raw.githubusercontent.com/fray-hao/images/master/20190402125418.png)
这时你希望估计出这些数据的概率密度和热量和振动的joint概率分布，因为你希望检测出异常的样本。当一个新的飞机引擎从组装线上生产出来时，你测量它是热量和振动属性。如果你得到一个这样的点， 它有没有检测出的错误，需要不需要进一步检测：
![](https://raw.githubusercontent.com/fray-hao/images/master/20190402133324.png)

如果我们考虑热量和振动的概率分布，并建立P(x)模型。如果发现对于一个新的引擎，P(x)非常小，我们可能就认为它是一个异常的产品。所以它需要在正式使用前进行进一步的检查。这是一个异常检测的例子。

进行异常检测的一般方法是：利用一组数据集合，建立一个常规数据的概率分布模型P(x)。如果对于一个新样本，P(x)的值很小，那么你就可以报告发现了一个异常样本。异常检测通常应用在安全领域。

我们要介绍的就是一些进行密度估计的算法。为了描述我们的算法，我要举一个一维的例子。数据集看起来是两个高斯函数的混合：
![](https://raw.githubusercontent.com/fray-hao/images/master/20190402134502.png)
所以，我要描述的这个模型就叫高斯混合模型。

如果我们能区别每个特征，就能生成两个高斯分布，最终的分布就是两个高斯概率分布的和。
![](https://raw.githubusercontent.com/fray-hao/images/master/20190402135035.png)
但是问题是，我们不知道数据的标签，不知道生成数据的两个高斯分布是怎么样的。尽管我们不知道数据是由哪个分布生成的，我们需要总的是找到一个算法，可以拟合出两个混合在一起的高斯分布。

思路是这样的：
1. 有一个隐藏（latent（hidden/unobserved）隐藏、未被发现的）的随机变量Z。
2. $x^{(i)},z^{(i)}$有一个joint概率分布。根据链式规则：
   $$
   P(x^{(i)},z^{(i)})=P(x^{(i)}|z^{(i)})P(z^{(i)})
   $$
3. 假设$z^{(i)}$服从参数为$\phi的$伯努利多项式分布
   $$
   z^{(i)}\text{\textasciitilde} Multinomial(\phi)
   $$
   多项式分布的参数：
 ![](https://raw.githubusercontent.com/fray-hao/images/master/20190402143121.png)
    那么：
    $$
    x^{(i)}|z^{(i)}=j \text{\textasciitilde}N(\mu_j,\epsilon_j)
    $$
4. 为了让它与高斯判别分析的联系更为明显。假设我们知道$z^{(i)}$,也就是知道每个点来自于哪个高斯分布。那么我们就可以利用极大似然估计，将参数的极大似然估计写出来：
   $$
   L(\phi,\mu,\epsilon) = \sum_{i=1}^m\log p(x^{(i)},z^{(i)};\phi,\mu,\epsilon)
   $$
  利用极大似然估计可以得到和高斯判别分析相同的公式：
  $$
  \begin{aligned}
     & \phi_j = \frac{1}{m}\sum_{i=1}^m 1\{z^{(i)}=j\}
    \\& \mu_j = \frac{\sum_{i=1}^m 1\{z^{(i)}=j\}x^{(i)}}{\sum_{i=1}^m 1\{z^{(i)}=j\}}
    \\& etc..
  \end{aligned}
  $$

如果你知道z的值（z和高斯判别分析中的类标记是一样的作用），之后就可以利用极大似然估计估计出参数的值。但是实际上，我们并不知道z的值，我们知道的只是没有任何标记的数据集。

所以，我们需要用到一个自举过程（bootstrap procedure）。思想是：我们先用模型，尝试猜测z的值。之后用猜测的z的值拟合出参数的值。之后我们进行迭代，可以得到一个对参数值更好的估计。之后再去猜测z的值，之后用极大似然估计求出参数的值

## EM算法
最大期望算法的步骤是这样的：
重复以下步骤直到收敛
1. E-step.根据参数初始值或上一次迭代的模型参数来计算出隐性变量的后验概率，其实就是隐性变量的期望。作为隐藏变量的现估计值。
也就是猜测$z^{(i)}$的值，令：
$$
\begin{aligned}
    w_j^{(i)} &:= P(z^{(i)}=j|x^{(i)},\phi,\mu,\epsilon)
    \\&=\frac{P(x^{(i)}|z^{(i)}=j)P(z^{(i)}=j)}{\sum_{l=1}^kP(x^{(i)}|z^{(i)}=l)P(z^{(i)}=l)}
    \\&=\frac{\frac{1}{(2\pi)^{d/2}|\epsilon_j|^{1/2}}\exp((x^{(i)}-\mu_j)^2\epsilon_j)}{}
\end{aligned}
$$
![](https://raw.githubusercontent.com/fray-hao/images/master/20190402160343.png)
2. M-step(maximization step).更新对参数的估计：

$$
\begin{aligned}
    &\phi_j:=\frac{1}{m}\sum^m_{i=1}w^{(i)}_j
    \\& \mu_j := \frac{\sum_{i=1}^mw_j^{(i)}x^{(i)}}{\sum_{i=1}^mw_j^{(i)}}
    \\& \epsilon_j :=\frac{\sum_{i=1}^mw_i^{(i)}(x^{(i)}-\mu_j)(x^{(i)}-\mu_j)^T}{\sum_{i=1}^mw_j^{(i)}}
\end{aligned}
$$
和高斯判别很相似，不同之处在于，对于混合高斯模型，我们队不同的高斯分布使用了不同的协方差矩阵$\epsilon_j$

![](https://raw.githubusercontent.com/fray-hao/images/master/20190403082403.png)
在M-step中，我们使用$w_j^{(i)}$代替了高斯判别分析中的指示函数$1\{z^{(i)}=j\}$

这个算法展示了EM算法的直观理解。这是EM算法在高斯模型上的一个特例。接下来，我要介绍的是EM算法的一般形式。
https://blog.csdn.net/wyl1813240346/article/details/78855726

https://blog.csdn.net/weixin_39965890/article/details/80400294

https://www.cnblogs.com/llhthinker/p/5494321.html