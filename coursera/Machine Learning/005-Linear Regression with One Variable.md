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

### 1.3 监督学习的工作原理
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

## 2. cost funciton

In this video we'll define something called the cost function, this will let us figure out how to fit the best possible straight line to our data.

In linear progression, we have a training set that I showed here remember on notation M was the number of training examples, so maybe m equals 47. And the form of our hypothesis,which we use to make predictions is this linear function.

![](https://i.loli.net/2019/03/30/5c9f27c3a7229.png)

To introduce a little bit more terminology, these $\theta_0$ and $\theta_1$, they stabilize what I call the parameters of the model. And what we're going to do in this video is talk about how to go about choosing these two parameter values, $\theta_0$ and $\theta_1$. With different choices of the parameter's $\theta_0$ and $\theta_1$, we get different hypothesis, different hypothesis functions. 
![](https://i.loli.net/2019/03/30/5c9f2869d4419.png)
I know some of you will probably be already familiar with what I am going to do on the slide, but just for review, here are a few examples. If theta 0 is 1.5 and theta 1 is 0, then the hypothesis function will look like this.
Because your hypothesis function will be h of x equals 1.5 plus 0 times x which is this constant value function which is phat at 1.5. If theta0 = 0, theta1 = 0.5, then the hypothesis will look like this, and it should pass through this point 2,1 so that you now have h(x). Or really h of theta(x), but sometimes I'll just omit theta for brevity. So h(x) will be equal to just 0.5 times x, which looks like that. And finally, if theta zero equals one, and theta one equals 0.5, then we end up with a hypothesis that looks like this. Let's see, it should pass through the two-two point. Like so, and this is my new vector of x, or my new h subscript theta of x. Whatever way you remember, I said that this is h subscript theta of x, but that's a shorthand, sometimes I'll just write this as h of x.
![](https://i.loli.net/2019/03/30/5c9f28bc2c12c.png)
In linear regression, we have a training set, like maybe the one I've plotted here. What we want to do, is come up with values for the parameters theta zero and theta one so that the straight line we get out of this, corresponds to a straight line that somehow fits the data well, like maybe that line over there.

![](https://i.loli.net/2019/03/30/5c9f28df6e7f4.png)
So, how do we come up with values, theta zero, theta one, that corresponds to a good fit to the data?

**The idea is we get to choose our parameters theta 0, theta 1 so that h of x, meaning the value we predict on input x, that this is at least close to the values y for the examples in our training set, for our training examples.** 

So in our training set, we've given a number of examples where we know X decides the wholes and we know the actual price is was sold for. So, let's try to choose values for the parameters so that, at least in the training set, given the X in the training set we make reason of the active predictions for the Y values. Let's formalize this. So linear regression, what we're going to do is, I'm going to want to solve a minimization problem. So I'll write minimize over $\theta_0,\theta_1$. And I want this to be small, right? I want the difference between h(x) and y to be small. And one thing I might do is try to minimize the square difference between the output of the hypothesis and the actual price of a house. 


Okay. So lets find some details. You remember that I was using the notation $(x^{(i)},y^{(i)})$ to represent the ith training example. So what I want really is to sum over my training set, something i = 1 to m, of the square difference between, this is the prediction of my hypothesis when it is input to size of house number i.

Right? Minus the actual price that house number I was sold for, and I want to minimize the sum of my training set, sum from I equals one through M, of the difference of this squared error, the square difference between the predicted price of a house, and the price that it was actually sold for. 
$$
\min_{\theta_0,\theta_1} \sum_{i=1}^m(h_\theta(x^{(i)})-y^{i})^2   
$$

And just remind you of notation, m here was the size of my training set right? I'm going to actually look at we are 1 over m times that so let's try to minimize my average minimize one over 2m. Putting the 2 at the constant one half in front, it may just sound the math probably easier so minimizing one-half of something, right, should give you the same values of the process, theta 0 theta 1, as minimizing that function.

$$
\min_{\theta_0,\theta_1} \frac{1}{2m}\sum_{i=1}^m(h_\theta(x^{(i)})-y^{i})^2   
$$


And this notation, minimize over theta 0 theta 1, this means you'll find  the values of theta 0 and theta 1 that causes this expression to be minimized and this expression depends on theta 0 and theta 1

And just to rewrite this out a little bit more cleanly, what I'm going to do is, by convention we usually define a cost function,

$$
J(\theta_0, \theta_1) = \frac{1}{2m}\sum_{i=1}^m(\hat{y^{(i)}}-y^{(i)})^2 =\frac{1}{2m}\sum_{i=1}^m(h_\theta(x^{(i)})-y^{(i)})^2 
$$
> To break it apart, it is $\frac{1}{2}\bar{x}$ where $\bar{x}$is the mean of the squares of $h_\theta (x^{(i)}) - y^{(i)}$


This is my cost function.so, this cost function is also called the squared error function.

what we want to do is minimized this funciton:
$$
\min_{\theta_0,\theta_1} J(\theta_0,\theta_1)
$$

When sometimes called the squared error cost function and it turns out that why do we take the squares of the erros. It turns out that these squared error cost function is a reasonable choice and works well for problems for most regression programs. There are other cost functions that will work pretty well. But the square cost function is probably the most commonly used one for regression problems. Later in this class we'll talk about alternative cost functions as well, but this choice that we just had should be a pretty reasonable thing to try for most linear regression problems.

So far we've just seen a mathematical definition of this cost function. In case this function j of theta zero, theta one. In case this function seems a little bit abstract, and you still don't have a good sense of what it's doing, in the next video, in the next couple videos, I'm actually going to go a little bit deeper into what the cause function "J" is doing and try to give you better intuition about what is computing and why we want to use it...