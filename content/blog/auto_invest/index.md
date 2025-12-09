---
weight: 3
title: "定投原理"
author: "yxr620"
tags: ["投资"]
categories: ["blog"]
toc:
  enable: true
  auto: true
date: 2022-02-19T23:44:00+08:00
---


分析一个定投的原理并且做一些定投的实验。通过原理找出合适定投的产品，并且通过实验验证结论是否正确。

### 1. 定投模型

定投就是每隔一定的时间就对一个投资产品进行固定金额的购买。为了能简化出来定投的数学模型，定义如下符号：

* $x$每次定投的金额
* $0-T$总定投的时间
* $\Delta T$每次定投间隔的时间
* $f(t)$投资产品的价格关于时间的函数（例如一股$f(t)$元）

由定投的总时间和定投的间隔时间我们可以计算出定投的总次数$n = T / \Delta T$，那么投资的总金额就是$TV = nx = xT/\Delta T$。不妨设在$\Delta T$时刻进行第一次投资，那么第$i$次投资获得产品数量$m_i = x / f(i \Delta T)$，总共获得投资产品的数量为$M= \sum_{i = 1}^{n} m_i$。计算出总数量和总成本，就可以计算出平均成本$c$如下：

<div>$$
c = TV / M\\
= \frac{xn}{\sum_{i = i}^{n} \frac{x}{f(i \Delta T)}}\\
= \frac{n}{\sum_{i = 1}^{n} \frac{1}{f(i \Delta T)}}
$$</div>

已知如果想要投资获利，那么投资人的目标是降低手上每一份投资产品的均价尽量低，并且在卖出时的价格尽量高。定投平没有规定卖出的时间，因此定投策略本身无法控制卖出价格。根据上面的分可以看定投主要控制的是买入的平均价格。

买入的平均价格是$c$，这个公式实际上是一个调和平均数的公式。定投的魔力也正是通过这个调和平均数表现出来。如果我们在任意一个时刻all in一个投资产品那么我们得到的产品价格是算数平均数。根据基础的不等式知识知道调和平均数<算数平均数。用公式来说就是：

<div>$$
\frac{n}{\sum_{i = 1}^{n} \frac{1}{f(i \Delta T)}} < \frac{\sum_{i = 1}^n f(i \Delta T)}{n}
$$</div>

右边的公式就是算出平均数，也就是随机一点all in的平均成本。

当然这个算式写出来非常的抽象，不妨说一个形象的理解。定投在投资的时候由于每次投资的金额相等，那么在价格低的时候会买入更多的产品，在高点的时候会购入更少的产品，也就是说自动的对价格进行了购买策略的调正，一定程度上放大了低价区间，缩小了高价区间。

### 2. 定投实验

定投的实验反复被论证：**定投是比大多数基金经理都聪明的投资策略**。而且$89\%$的对冲基金都没有战胜美国的股市的大盘。

#### 2.1 不同投资策略对比

有关定投的实验非常多，实验过程简单明了，结论也非常清晰。在这里介绍一个reddit上面的实验：[源实验](https://www.reddit.com/r/financialindependence/comments/c02ml4/timing_the_market_the_absolute_worst_vs_absolute/)。

这个实验假设三种情景：

* Tiffany是最差的投资者。每个月她存200美元，获得$3\%$的利息。到了金融危机的时候她就在最高点全部买入S&P500美国大盘基金。之后继续存钱直到下一次金融危机继续在最高点投入。这样她会买入4次，分别是1987、1990、2000、2007。经过40年的投资之后（从1979年开始），总共投入96,000美元，资产663,594美元。
* Brittany是最强的投资者。每个月她存200美元，获得$3\%$的利息，然后在每次金融危机最低点买入S&P500。这样40年下来资产为956,838
* Sarah是定投者。每个月投资200美元到S&P500，四十年下来资产为1,386,429。

#### 2.2 不同时间跨度对比

定投的时间间隔不同给人的感觉非常不同。因此在这里做一个不同时间间隔的利润对比。在2012-2022年这十年时间内，分别采用时间间隔为1天、1周、1月。结果如下：

|      | 1天        | 1周        | 1月        |
| ---- | ---------- | ---------- | ---------- |
| 增长 | $191.89\%$ | $207.19\%$ | $198.73\%$ |

根据上面的结果看出当时间长度足够长的时候每一种时间间隔都有差不多的收益，因此不必过于纠结与时间间隔的长短。







<script type="text/javascript"
        async
        src="https://cdn.bootcss.com/mathjax/2.7.3/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
MathJax.Hub.Config({
  tex2jax: {
    inlineMath: [['$','$'], ['\\(','\\)']],
    displayMath: [['$$','$$'], ['\[\[','\]\]']],
    processEscapes: true,
    processEnvironments: true,
    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
    TeX: { equationNumbers: { autoNumber: "AMS" },
         extensions: ["AMSmath.js", "AMSsymbols.js"] }
  }
});

MathJax.Hub.Queue(function() {
    
    
    
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>

<style>
code.has-jax {
    font: inherit;
    font-size: 100%;
    background: inherit;
    border: inherit;
    color: #515151;
}
</style>
