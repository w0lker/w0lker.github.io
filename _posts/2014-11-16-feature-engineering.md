---
layout: post
title:  "特征工程（Feature Engineering）"
date: 2014-11-15
description: "测试一下"
tags:
categories: other
---




##离散化续篇

在上节中我已经介绍了一些常用的离散化单个连续特征的方法，其中一个是*画图观察趋势*。画图观察趋势的好处是直观、可解释性强，坏处是很麻烦。当要离散化的特征很多时，这种方法可操作性较差。

机器学习中有个很好解释，速度也不错的模型——**决策树模型**。大白话说决策树模型就是一大堆的`if else`。它天生就可以对连续特征分段，所以把它用于离散化连续特征合情合理。我称这种方法为**决策树离散化**方法。

决策树离散化方法通常也是每次离散化一个连续特征，做法如下：

> 单独用此特征和目标值$$y$$训练一个决策树模型，然后把训练获得的模型内的特征分割点作为离散化的离散点。

这种方法当然也可以同时离散化多个连续特征，但是操作起来就更复杂了，实际用的不多。

接下来我们再介绍下[Facebook][fb]最近发表的利用**GBDT**模型来处理特征的方法[^fbgbdt]。

![Facebook GBDT][fb_gbdt]



###使用决策树来抽取特征

[img_ori]: /images/nonlinear_function1.png "样本点"
[img_equal_dist]: /images/nonlinear_function2.png "等距离散离散法"
[img_equal_size]: /images/nonlinear_function3.png "等样本点离散离散法"
[img_watch]: /images/nonlinear_function4.png "画图观察趋势离散法"
[fb_gbdt]: /images/fb_gbdt.png "GBDT离散法"

[fb]: http://www.facebook.com "Facebook"


#References

[^esl]: Trevor Hastie et al, [The Elements of Statistical Learning](http://statweb.stanford.edu/~tibs/ElemStatLearn/), 2001.
[^fhash]: Kilian Weinberger et al, Feature Hashing for Large Scale Multitask Learning, 2010.
[^fbgbdt]: Xinran He et al, Practical Lessons from Predicting Clicks on Ads at Facebook, 2014



#归一化：
  * 有些模型/优化
  * 方法的效果会强烈地依赖于特征是否归一化，如LogisticReg，SVM，NeuralNetwork，SGD等。
  * 有些模型则不受归一化影响，如DecisionTree。
  * 0/1取值的特征通常不需要归一化，归一化会破坏它的稀疏性


#离散化：
 4. 单独用此特征和目标值来训练一个决策树，依据决策树的各节点的划分方法来离散化此特征
  * 特征离散化时不一定要保留所有的取值段对应的特征，可以通过特征选择或者领域知识去掉其中的一部分（经常是头部或尾部）
  * facebook用gbdt抽取特征
  * feature hashing：
    * 可以添加新的原始特征而保持hashing后的特征长度不变
    * 可以保持原始特征的稀疏性，既然hashing时只考虑非0原始特征
    * 可以只hashing其中的一部分原始特征，而保留另一部分原始特征（如那些出现collision就会很影响精度的重要特征）
    * 很适合有个性化的应用，因为此时要加入用户id的话会导致原始特征数量变为 (用户数+1)*特征数
    * The result is increased speed and reduced memory usage, at the expense of inspectability;
    * Paper: Feature Hashing for Large Scale Multitask Learning


#特征抽取：
  * 尽可能人为删除特征里的非线性性，不要期待模型自己能很好地自动处理非线性性
  * 间接特征：通过其他模型抽取的特征
    * 如可以利用LDA的聚类结果作为特征
    * 用户画像
    * Predicting Positive and Negative Links in Online Social Networks
    * 如果有时间概念，一般临近时间内的用户行为会较像，可以考虑把前几天的用户行为作为特征


    这里说的SVM是指最原始的2分类SVM，不考虑SVM的其他各种扩展。为简单起见，我们也只考虑线性SVM，对于带核函数的SVM，利用相似的推导我们可以获得相同的结论：

    > 2分类SVM等于Hinge损失 + L2正则化。

    下面是线性SVM的一般形式，其中目标分类$y \in \\{-1, 1\\}$，$C$为给定的惩罚系数：

    $$
    \begin{aligned}
    \min\limits_{\omega, \gamma, \xi}& \left[
    \frac12 \|\omega\|^2_2 + C \sum_{i=1}^n \xi_i
    \right] \\
    s. t. \ & (\omega^T x_i + \gamma) y_i \geq 1 - \xi_i, \ \forall i = 1, \ldots, n \\
    & \xi_i \geq 0 , \ \forall i = 1, \ldots, n
    \end{aligned}
    $$

    记$m \triangleq f_{\theta}(x) y$（其中$y \in \\{-1, 1\\}$），那么对于2分类问题，最理想的损失函数是**0/1损失**函数。也就当$f\_{\theta}(x)$与$y$有相同符号时，损失为0；而当$f\_{\theta}(x)$与$y$有不同符号时，损失为1。但0/1损失函数既不是处处可微，又不是凸函数，所以直接最小化0/1损失函数很困难。**Hinge损失**是0/1损失的一种近似（见下图）：

    $$
    J_{\text{hinge}}(m) = \max \{0, 1-m\} \ \ \text{。}
    $$

    ![0/1损失与Hinge损失函数][hingeloss]

    Hinge损失的名字是源自它跟打开135度的折叶（hinge）长得很像。

    ![0/1损失与Hinge损失函数][hinge]


    带有L2正则项的Hinge损失优化问题如下：

    $$
    \min\limits_{\omega, \gamma} \left[
    C \sum_{i=1}^n \max \left\{ 0, 1 - (\omega^T x_i + \gamma) y_i \right\}
    + \frac12 \|\omega\|^2_2
    \right] \ \ \text{。}
    $$

    为了与前面的SVM表达式对应，我们把L2正则项中的惩罚系数挪到前面的Hinge损失上了。Hinge损失函数有如下的等价定义：

    $$
    \max \{0, 1-m\} =

    \underset{
    \begin{aligned}
    s.t.& \ \xi \geq 1-m \\
    & \xi \geq 0
    \end{aligned}
    }{\min \xi}
    $$

    利用上面的等价定义，我们可以重写带有L2正则项的Hinge损失优化问题为：

    $$
    \begin{aligned}
    \min\limits_{\omega, \gamma, \xi}& \left[
    C \sum_{i=1}^n \xi_i + \frac12 \|\omega\|^2_2
    \right] \\
    s.t.& \  \xi_i \geq 1 - (\omega^T x_i + \gamma)y_i , \ \forall i = 1, \ldots, n \\
    & \xi_i \geq 0 , \ \forall i = 1, \ldots, n
    \end{aligned}
    $$

    嗯，上式就是本文最开始给出的SVM优化问题了。


    更详细的资料可见参考文献[^graph_ml]。


    [hingeloss]: /images/hingeloss.png "0/1损失与Hinge损失"
    [hinge]: /images/hinge.png "折叶（hinge）"

    #References

    [^graph_ml]: 杉山将，《图解机器学习》第8.5节，2015。
