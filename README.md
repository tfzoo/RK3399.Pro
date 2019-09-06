﻿# [activation](https://github.com/tfzoo/activation) 
## [激活函数](https://github.com/tfzoo/activation/wiki) 

如果不用Activation Function，每一层输出都是上层输入的线性函数，无论多少层输出都是输入的线性组合，与没有隐藏层效果相当，这是最原始的感知机（Perceptron）；激活函数给神经元引入了非线性因素，使得神经网络可以任意逼近任何非线性函数，这样神经网络就可以应用到众多的非线性模型中。

### Sigmoid

$ f(x) = sigmoid(x) = \frac{1}{1+e^{-x}} 

Logistic Sigmoid（Sigmoid）给神经网络引进了概率的概念，值域[0,1]，可以将实数映射到[0,1]区间用做二分类。特别的，如果是非常大的负数，那么输出就是0；如果是非常大的正数，输出就是1。

在特征相差比较复杂或是相差不是特别大时效果比较好。
它的导数是非零的，并且很容易计算（是其初始输出的函数）。

* 在深度神经网络中梯度反向传递时导致梯度爆炸和梯度消失，其中梯度爆炸发生的概率非常小，而梯度消失发生的概率比较大。
* Sigmoid 的 output 不是0均值（即zero-centered）。这是不可取的，因为这会导致后一层的神经元将得到上一层输出的非0均值的信号作为输入。
* 其解析式中含有幂运算，计算机求解时相对来讲比较耗时。


### Tanh

$ f(x) = tanh(x) = \frac{e^x-e^{-x}}{e^x+e^{-x}} 

双曲正切函数（Tanh），值域[-1,1]，逐渐取代 Sigmoid 函数作为标准的激活函数，为奇函数（关于原点对称），解决了Sigmoid函数的不是zero-centered输出问题。为了解决学习缓慢和/或梯度消失问题，可以使用这个函数的更加平缓的变体（log-log、softsign、symmetrical sigmoid 等等）

它是完全可微分的，反对称，对称中心在原点。tanh在特征相差明显时的效果会很好，在循环过程中会不断扩大特征效果。

实际上，tanh函数只是规模变化的sigmoid函数，将sigmoid函数值放大2倍之后再向下平移1个单位：tanh(x) = 2sigmoid(2x) - 1 。

### ReLU

$ f(x) = max(0, x) 

修正线性单元（Rectified linear unit，ReLU）是神经网络中最常用的激活函数用于隐层神经元输出，输入信号 <0 时，输出都是0，>0 的情况下输出等于输入，输出不是zero-centered，并不是全区间可导。

它保留了 step 函数的生物学启发（只有输入超出阈值时神经元才激活），不过当输入为正的时候，导数不为零，从而允许基于梯度的学习（尽管在 x=0 的时候，导数是未定义的）。使用这个函数能使计算变得很快，因为无论是函数还是其导数都不包含复杂的数学运算。

* 解决了gradient vanishing问题 (在正区间)
* 计算速度非常快，只需要判断输入是否大于0
* 收敛速度远快于sigmoid和tanh

然而，当输入为负值的时候，ReLU 的学习速度可能会变得很慢，甚至使神经元直接无效，因为此时输入小于零而梯度为零，从而其权重无法得到更新，在剩下的训练过程中会一直保持静默。

一个非常大的梯度流过一个 ReLU 神经元，更新过参数之后，这个神经元再也不会对任何数据有激活现象，需要小心设置 learning rate


###  [天府动物园 tfzoo：tensorflow models zoo](http://www.tfzoo.com)
####   qitas@qitas.cn
[![sites](tfzoo/tfzoo.png)](http://www.tfzoo.com)