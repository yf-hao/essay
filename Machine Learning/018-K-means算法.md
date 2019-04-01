前面学习的算法都是监督学习，而今天我们将开始学习无监督学习：
- clustering（k-means）
- mixture  of Gaussian （混合高斯）
- Jensen's inequality
- EM(Expectation Maximization)

接下来，我们简短的介绍下K-means算法。

在将监督学习的时候，经常会画一副这样的图：
![](https://raw.githubusercontent.com/fray-hao/images/master/20190401120800.png)
使用逻辑回归、svm等算法时，会根据每个样本的标签（正负）进行分类。所以叫做监督学习。

而无监督学习研究的是不同的问题。给定若干个点（样本）构成的数据集合，所有的点没有像监督学习那样给出类标签或者所谓的正确答案，我们需要靠算法本身，来发现数据中的结构。数据集的形式如下：
![](https://raw.githubusercontent.com/fray-hao/images/master/20190401121317.png)

k-均值聚类是一种最常见的无监督的聚类算法，该算法对没有标签的数据集进行训练，然后将数据集聚类成不同的类别。 

https://blog.csdn.net/wyl1813240346/article/details/78855726

https://blog.csdn.net/weixin_39965890/article/details/80400294

https://www.cnblogs.com/llhthinker/p/5494321.html