## 机器学习的定义
What is machine learning? In this video, we will try to define what it is and also try to give you a sense of when you want to use machine learning. 
Even among machine learning practitioners, there isn't a well accepted definition of what is and what isn't machine learning. But let me show you a couple of examples of the ways that people have tried to define it. Here's a definition of what is machine learning as due to Arthur Samuel. He defined described it as: 
```
 the field of study that gives computers the ability to learn without being explicitly programmed.
```

Samuel's claim to fame was that back in the 1950, he wrote a checkers playing program and the amazing thing about this checkers playing program was that Arthur Samuel himself wasn't a very good checkers player. But what he did was he had to programmed maybe tens of thousands of games against himself, and by watching what sorts of board positions tended to lead to wins and what sort of board positions tended to lead to losses, the checkers playing program learned over time what are good board positions and what are bad board positions. And eventually learn to play checkers better than the Arthur Samuel himself was able to. This was a remarkable result. 
Arthur Samuel himself turns out not to be a very good checkers player. But because a computer has the patience to play tens of thousands of games against itself, no human has the patience to play that many games. By doing this, a computer was able to get so much checkers playing experience that it eventually became a better checkers player than Arthur himself.

This is a somewhat informal definition and an older one. Here's a slightly more recent definition by Tom Mitchell who's a friend of Carnegie Melon. So Tom defines machine learning by saying that a well-posed learning problem is defined as follows. 
```
a computer program is said to learn from experience E with respect to some task T and some performance measure P, if its performance on T, as measured by P, improves with experience E.
```
I actually think he came out with this definition just to make it rhyme. For the checkers playing examples, - the experience E would be the experience of having the program play tens of thousands of games itself. 
- The task T would be the task of playing checkers, 
- and the performance measure P will be the probability that wins the next game of checkers against some new opponent.

## 例子
Throughout these videos, besides me trying to teach you stuff, I'll occasionally ask you a question to make sure you understand the content. Here's one.
Let's say your email program watches which emails you do or do not mark as spam. So in an email client like this, you might click the Spam button to report some email as spam but not other emails. And based on which emails you mark as spam, say your email program learns better how to filter spam email. What is the task T in this setting? 
So hopefully you got that this is the right answer:
- classifying emails is the task T. In fact, this definition defines a task T performance measure P and some experience E. 
- And so, watching you label emails as spam or not spam, this would be the experience E and 
- and the fraction of emails correctly classified, that might be a performance measure P. And so on the task of systems performance, on the performance measure P will improve after the experience E.

## 机器学习分类
In this class, I hope to teach you about various different types of learning algorithms. There are several different types of learning algorithms. The main two types are what we call **supervised learning and unsupervised learning**. I'll define what these terms mean more in the next couple videos. It turns out that in supervised learning, the idea is we're going to teach the computer how to do something. Whereas in unsupervised learning, we're going to let it learn by itself. Don't worry if these two terms don't make sense yet. In the next two videos, I'm going to say exactly what these two types of learning are. You might also hear other ghost terms such as **reinforcement learning and recommender systems**. 
These are other types of machine learning algorithms that we'll talk about later. But the two most use types of learning algorithms are probably supervised learning and unsupervised learning. And I'll define them in the next two videos and we'll spend most of this class talking about these two types of learning algorithms. 

## 知道如何使用工具很重要
It turns out what are the other things to spend a lot of time on in this class is practical advice for applying learning algorithms. This is something that I feel pretty strongly about. And exactly something that I don't know if any other university teachers. Teaching about learning algorithms is like giving a set of tools. And equally important or more important than giving you the tools as they teach you how to apply these tools. 

I like to make an analogy to learning to become a carpenter. Imagine that someone is teaching you how to be a carpenter, and they say, here's a hammer, here's a screwdriver, here's a saw, good luck. Well, that's no good. You have all these tools but the more important thing is to learn how to use these tools properly.

There's a huge difference between people that know **how to use these machine learning algorithms**, versus people that don't know how to use these tools well.
Here, in Silicon Valley where I live, when I go visit different companies even at the top Silicon Valley companies, very often I see people trying to apply machine learning algorithms to some problem and sometimes they have been going at for six months. But sometimes when I look at what their doing, I say, I could have told them like, gee, I could have told you six months ago that you should be taking a learning algorithm and applying it in like the slightly modified way and your chance of success will have been much higher. So what we're going to do in this class is actually spend a lot of the time talking about how if you're actually trying to develop a machine learning system, how to make those best practices type decisions about the way in which you build your system. 
So that when you're finally learning algorithim, you're less likely to end up one of those people who end up persuing something after six months that someone else could have figured out just a waste of time for six months. So I'm actually going to spend a lot of time teaching you those sorts of best practices in machine learning and AI and how to get the stuff to work and how the best people do it in Silicon Valley and around the world. 

I hope to make you one of the best people in knowing how to design and build serious machine learning and AI systems. So that's machine learning, and these are the main topics I hope to teach. In the next video, I'm going to define what is supervised learning and after that what is unsupervised learning. And also time to talk about when you would use each of them.