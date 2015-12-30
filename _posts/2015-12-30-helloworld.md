---
layout: post
title:  "测试文档"
date:   2015-06-30
description: "HelloWorld"
categories: works
---

#### 图片演示
![喜欢的图片](/images/bizhi.jpg)

#### 代码演示
{% highlight c++ linenos %}
#include<iostream>

int main()
{
  std::cout << "hello,world!" << std::endl;
}
#=> prints 'hello,world!' to STDOUT.
{% endhighlight %}

{% highlight java %}
public class Hello {

    public static void main(String[] args) {
        System.out.println("hello,world!");
    }

}
{% endhighlight %}

#### 公式
$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$
