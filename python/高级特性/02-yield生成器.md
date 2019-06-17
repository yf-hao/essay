## generator 基础
在python的函数（function）定义中，只要出现了yield表达式（Yield expression），那么事实上定义的是一个generator function， 调用这个generator function返回值是一个generator。这根普通的函数调用有所区别。For example：
```python
def gen_generator():
    yield  1

def gen_value():
    return 1

if __name__== '__main__':
    ret = gen_generator()
    print(ret) # <generator object gen_generator at 0x1023d6258>
    print(type(ret)) # <class 'generator'>
    ret = gen_value()
    print(ret) # 1
    print(type(ret)) # <class 'int'>
```
从上面的代码可以看出，gen_generator()函数返回的是一个generator实例。

generator遵循迭代器（iterator）协议，迭代器协议需要实现__iter__、__next__接口
  ```python
    mygenerator = (x*x for x in range(3))  # 解析式生成的generator对象
    print(mygenerator.__iter__()) # <generator object <genexpr> at 0x105f060a0>
    print(mygenerator.__next__()) # 0
    print(mygenerator) # 等价于mygenerator.__iter__()
    print(next(mygenerator))# 等价于mygenerator.__next__()。这次输出结果为1
  ```
使用yield 表达式可以使函数变得可迭代，并且能够暂停函数体中代码的执行。yield 是一个类似 return 的关键字，迭代过程中遇到yield时就返回yield后面(右边)的值。下一次迭代时，不是从函数体开头进行迭代，而是从上一次运行中遇到的yield的下一行代码开始执行。 For example：
```python
def gen_eg():
    print("Before any yield")
    yield 'first yield'
    print('between yield')
    yield 'second yield'
    print('no yield')
gen = gen_eg()

print(next(gen)) # 第一次调用
# Before any yield
# first yield
print(next(gen)) # 第二次调用。从第一次迭代遇到的yield下一行开始
# between yield
# second yield
print(next(gen)) # 第三次调用。迭代中没有遇到yield会StopIteration。
# no yield
# Traceback (most recent call last):
#   File "/Users/free.hao/PycharmProjects/Books/d.py", line 28, in <module>
#     print(next(gen))
# StopIteration
```
　　调用gen_eg()方法并没有输出任何内容，说明函数体的代码尚未开始执行。当第一次调用next方法，generator会执行到yield表达式处，返回yield表达式的内容，然后暂停（挂起）在这个地方，所以第一次调用next时会打印第一句并返回“first yield”。 暂停意味着方法的局部变量，指针信息，运行环境都保存起来，直到下一次调用next方法恢复。第二次调用next之后就暂停在最后一个yield，再次调用next()方法，则会抛出StopIteration异常。　

　因为for语句能自动捕获StopIteration异常，所以generator（本质上是任何iterator）较为常用的方法是在循环中使用：　
```python
def count_num(n):
    while n > 0:
        yield n
        n -= 1


if __name__ == '__main__':
    for i in count_num(5):
        print(i)

```
## generator 使用场景

### 节省内存
　　为什么使用generator呢，最重要的原因是可以按需生成并“返回”结果，而不是一次性产生所有的返回值，况且有时候根本就不知道“所有的返回值”。比如对于下面的代码：
```python
RANGE_NUM = 100
    for i in [x*x for x in range(RANGE_NUM)]: # 第一种方法：对列表进行迭代
        # do sth for example
        print i

    for i in (x*x for x in range(RANGE_NUM)): # 第二种方法：对generator进行迭代
        # do sth for example
        print i
```

在上面的代码中，两个for语句输出是一样的，代码字面上看来也就是中括号与小括号的区别。但这点区别差异是很大的，第一种方法返回值是一个列表，第二个方法返回的是一个generator对象。随着RANGE_NUM的变大，第一种方法返回的列表也越大，占用的内存也越大；但是对于第二种方法没有任何区别。

我们再来看一个可以“返回”无穷多次的例子：
```python
def fib():
    a, b = 1, 1
    while True:
        yield a
        a, b = b, a+b 
```
这个generator拥有生成无数多“返回值”的能力，使用者可以自己决定什么时候停止迭代:
```python
num = 0;
for f in fib():
    if (num < 10):
        print(f)
        num += 1
```
### Generator可用于产生数据流
Generator可用于产生数据流， generator并不立刻产生返回值，而是等到被需要的时候才会产生返回值，相当于一个主动拉取的过程(pull)，比如现在有一个日志文件，每行产生一条记录，对于每一条记录，不同部门的人可能处理方式不同，但是我们可以提供一个公用的、按需生成的数据流。
```python
def gen_data_from_file(file_name):
    for line in file(file_name):
        yield line

def gen_words(line):
    for word in (w for w in line.split() if w.strip()):
        yield word

def count_words(file_name):
    word_map = {}
    for line in gen_data_from_file(file_name):
        for word in gen_words(line):
            if word not in word_map:
                word_map[word] = 0
            word_map[word] += 1
    return word_map

def count_total_chars(file_name):
    total = 0
    for line in gen_data_from_file(file_name):
        total += len(line)
    return total
    
if __name__ == '__main__':
    print count_words('test.txt'), count_total_chars('test.txt')
```
上面的例子来自08年的PyCon一个讲座。gen_words gen_data_from_file是数据生产者，而count_words count_total_chars是数据的消费者。可以看到，数据只有在需要的时候去拉取的，而不是提前准备好。另外gen_words中 (w for w in line.split() if w.strip()) 也是产生了一个generator

### 代替回调

一些编程场景中，一件事情可能需要执行一部分逻辑，然后等待一段时间、或者等待某个异步的结果、或者等待某个状态，然后继续执行另一部分逻辑。比如微服务架构中，服务A执行了一段逻辑之后，去服务B请求一些数据，然后在服务A上继续执行。或者在游戏编程中，一个技能分成分多段，先执行一部分动作（效果），然后等待一段时间，然后再继续。对于这种需要等待、而又不希望阻塞的情况，我们一般使用回调（callback）的方式。下面举一个简单的例子：
```python
def do(a):
    print 'do', a
    CallBackMgr.callback(5, lambda a = a: post_do(a))
 
def post_do(a):
    print 'post_do', a
```
这里的CallBackMgr注册了一个5s后的时间，5s之后再调用lambda函数，可见一段逻辑被分裂到两个函数，而且还需要上下文的传递（如这里的参数a）。我们用yield来修改一下这个例子，yield返回值代表等待的时间。
```python
@yield_dec
def do(a):
    print 'do', a
    yield 5
    print 'post_do', a
```
这里需要实现一个YieldManager， 通过yield_dec这个decrator将do这个generator注册到YieldManager，并在5s后调用next方法。Yield版本实现了和回调一样的功能，但是看起来要清晰许多。下面给出一个简单的实现以供参考：

```python
# -*- coding:utf-8 -*-
import sys
# import Timer
import types
import time

class YieldManager(object):
    def __init__(self, tick_delta = 0.01):
        self.generator_dict = {}
        # self._tick_timer = Timer.addRepeatTimer(tick_delta, lambda: self.tick())

    def tick(self):
        cur = time.time()
        for gene, t in self.generator_dict.items():
            if cur >= t:
                self._do_resume_genetator(gene,cur)

    def _do_resume_genetator(self,gene, cur ):
        try:
            self.on_generator_excute(gene, cur)
        except StopIteration,e:
            self.remove_generator(gene)
        except Exception, e:
            print 'unexcepet error', type(e)
            self.remove_generator(gene)

    def add_generator(self, gen, deadline):
        self.generator_dict[gen] = deadline

    def remove_generator(self, gene):
        del self.generator_dict[gene]

    def on_generator_excute(self, gen, cur_time = None):
        t = gen.next()
        cur_time = cur_time or time.time()
        self.add_generator(gen, t + cur_time)

g_yield_mgr = YieldManager()

def yield_dec(func):
    def _inner_func(*args, **kwargs):
        gen = func(*args, **kwargs)
        if type(gen) is types.GeneratorType:
            g_yield_mgr.on_generator_excute(gen)

        return gen
    return _inner_func

@yield_dec
def do(a):
    print 'do', a
    yield 2.5
    print 'post_do', a
    yield 3
    print 'post_do again', a

if __name__ == '__main__':
    do(1)
    for i in range(1, 10):
        print 'simulate a timer, %s seconds passed' % i
        time.sleep(1)
        g_yield_mgr.tick()
```
## 注意事项
### Yield是不能嵌套的
```python
def visit(data):
    for elem in data:
        if isinstance(elem, tuple) or isinstance(elem, list):
            visit(elem) # here value retuened is generator
        else:
            yield elem
            
if __name__ == '__main__':
    for e in visit([1, 2, (3, 4), 5]):
        print e
```
上面的代码访问嵌套序列里面的每一个元素，我们期望的输出是1 2 3 4 5，而实际输出是1  2  5 。为什么呢，如注释所示，visit是一个generator function，所以第4行返回的是generator object，而代码也没这个generator实例迭代。那么改改代码，对这个临时的generator 进行迭代就行了。
```python
def visit(data):
    for elem in data:
        if isinstance(elem, tuple) or isinstance(elem, list):
            for e in visit(elem):
                yield e
        else:
            yield elem
```
或者在python3.3中 可以使用yield from，这个语法是在pep380加入的
```python
def visit(data):
    for elem in data:
        if isinstance(elem, tuple) or isinstance(elem, list):
            yield from visit(elem)
        else:
            yield elem
```
### 使用return
在python doc中，明确提到是可以使用return的，当generator执行到这里的时候抛出StopIteration异常。
```python
def gen_with_return(range_num):
    if range_num < 0:
        return
    else:
        for i in xrange(range_num):
            yield i

if __name__ == '__main__':
    print list(gen_with_return(-1))
    print list(gen_with_return(1))
```
但是，generator function中的return是不能带任何返回值的
```python
def gen_with_return(range_num):
    if range_num < 0:
        return 0
    else:
        for i in xrange(range_num):
            yield i
```
上面的代码会报错：SyntaxError: 'return' with argument inside generator
https://www.cnblogs.com/xybaby/p/6322376.html
