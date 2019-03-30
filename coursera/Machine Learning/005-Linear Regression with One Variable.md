Linear regression predicts a real-valued output based on an input value. We discuss the application of linear regression to housing price prediction, present the notion of a cost function, and introduce the gradient descent method for learning.

## 1. Model Representation

### 1.1 给定训练集
Our first learning algorithm will be linear regression. In this video, you'll see what the model looks like and more importantly you'll see what the overall process of supervised learning looks like. 

Let's use some motivating example of predicting housing prices. 

![](https://i.loli.net/2019/03/30/5c9eb148c17d6.png)

We're going to use a data set of housing prices from the city of Portland, Oregon. 

And here I'm gonna plot my data set of a number of houses that were different sizes that were sold for a range of different prices. Let's say that given this data set, you have a friend that's trying to sell a house and let's see if friend's house is size of 1250 square feet and you want to tell them how much they might be able to sell the house for. 

![](https://i.loli.net/2019/03/30/5c9eb220af8ee.png)

Well one thing you could do is fit a model. Maybe fit a straight line to this data. 
![](https://i.loli.net/2019/03/30/5c9eb256de1d1.png)
Looks something like that and based on that, maybe you could tell your friend that let's say maybe he can sell the house for around $220,000. So this is an example of a supervised learning algorithm. 

And it's supervised learning because we're given the, quotes, "right answer" for each of our examples. Namely we're told what was the actual house, what was the actual price of each of the houses in our data set were sold.

for and moreover, this is an example of a regression problem where the term regression refers to the fact that we are predicting a real-valued output namely the price. And just to remind you the other most common type of supervised learning problem is called the classification problem where we predict discrete-valued outputs such as if we are looking at cancer tumors and trying to decide if a tumor is malignant or benign. So that's a zero-one valued discrete output. 

More formally, in supervised learning, we have a data set and this data set is called a training set. So for housing prices example, we have a training set of different housing prices and our job is to learn from this data how to predict prices of the houses. 

### 1.2 定义表示符号
Let's define some notation that we're using throughout this course. We're going to define quite a lot of symbols. It's okay if you don't remember all the symbols right now but as the course progresses it will be useful 
- m : denote the number of training examples 
So in this data set, if I have, you know, let's say 47 rows in this table. Then I have 47 training examples and m equals 47
- x : denote the input variables often also called the feature
- y : denote my output variables or the target variable which I'm going to predict 
- $(x^{(i)},y^{(i)})$ : refer to the ith training example 
the superscript i in parentheses that's just an index into my training set and refers to the ith row in this table,okay? So this is not x to the power of i, y to the power of i. Instead $(x^{(i)},y^{(i)})$  just refers to the ith row of this table. 

![](https://i.loli.net/2019/03/30/5c9ec8f3de3c7.png)
So for example, $x^{(1)}$ refers to the input value for the first training example so that's 2104. That's this x in the first row. $x^{(2)}$ will be equal to 1416 right? $y^{(1)}$ will be equal to 460.  

## 1.3 监督学习的工作原理
So here's how this supervised learning algorithm works. 
 
 ![](https://i.loli.net/2019/03/30/5c9ecaea0c8ff.png)
We saw that with the training set like our training set of housing prices and we feed that to our learning algorithm. Is the job of a learning algorithm to then output a function which by convention is usually denoted lowercase h and h stands for hypothesis And what the job of the hypothesis is, is, is a function that takes as input the size of a house like maybe the size of the new house your friend's trying to sell so it takes in the value of x and it tries to output the estimated value of y for the corresponding house. 
 
So h is a function that maps from x's to y's. People often ask me, you know, why is this function called hypothesis. Some of you may know the meaning of the term hypothesis, from the dictionary or from science or whatever. It turns out that in machine learning, this is a name that was used in the early days of machine learning and it kinda stuck. 'Cause maybe not a great name for this sort of function, for mapping from sizes of houses to the predictions, that you know.... I think the term hypothesis, maybe isn't the best possible name for this, but this is the standard terminology that people use in machine learning. So don't worry too much about why people call it that.
 
### 1.4  假设函数的模型
When designing a learning algorithm, the next thing we need to decide is how do we represent this hypothesis h. For this and the next few videos, I'm going to choose our initial choice , for representing the hypothesis, will be the following. We're going to represent h as follows.
 $$
 h_\theta(x) = \theta_0+\theta_1x
 $$ 
 sometimes there's a shorthand, I'll just write $h_\theta(x)$ as a $h(x)$. But more often I'll write it as a subscript theta over there.

And plotting this in the pictures:
![](https://i.loli.net/2019/03/30/5c9ecc2f4c41c.png)
All this means is that, we are going to predict that y is a linear function of x. Right, so that's the data set and what this function is doing, is predicting that y is some straight line function of x. 

And why a linear function? Well, sometimes we'll want to fit more complicated, perhaps non-linear functions as well. But since this linear case is the simple building block, we will start with this example first of fitting linear functions, and we will build on this to eventually have more complex models, and more complex learning algorithms. Let me also give this particular model a name. This model is called linear regression or this, for example, is actually linear regression with one variable, with the variable being x. Predicting all the prices as functions of one variable X. And another name for this model is univariate(单变量) linear regression. And univariate is just a fancy way of saying one variable. So, that's linear regression. In the next video we'll start to talk about just how we go about implementing this model.