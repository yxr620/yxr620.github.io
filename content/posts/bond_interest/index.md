---
weight: 3
title: "利率与债券"
author: "yxr620"
tags: ["投资"]
categories: ["blog"]
toc:
  enable: true
  auto: true
date: 2022-02-20T20:44:00+08:00
---

### 1. 一些概念

* **到期收益率（yield to maturity）**：使债务工具所有的未来回报的现值与其今天价值相等的利率。

* **回报率**：$R = \frac{C + P_{t + 1} - P_t}{P_t} = \frac{C}{P_t} + \frac{P_{t + 1} - P_t}{P_t} = i_c + g$

  其中$P_t$表示$t$时刻债券价格；$C$表示息票利息；$i_c$表示债券标注的利率；$g$表示资产增值

  注：不是所有债券通用的计算规则。

* **名义利率（nominal interest rate）**：$i$

  **实际利率（real interest rate）**：$r$

  **通货膨胀率（inflation rate）**：$\pi^e$

  上述三种变量的关系如下：
  $$
  \begin{cases}
  i = r + \pi^e + r\pi^e \\\\\\
  r = i - \pi^e\frac{1 + i}{1 + \pi^e}
  \end{cases}
  $$
  

### 2. 四种贷债券的分析

* **普通债券**：到期归还本金和利息，其到期收益率的公式如下：

$$
PV = \frac{CF}{(1 + i)^n}
$$

​	$PV$为借款金额，即现值；$CF$为n年后还款额；$i$为到期收益率。

* **固定支付贷款（fixed-payment loan）**：分期定额还款，其到期收益率公式如下：

$$
PV = \sum_{j = 1}^n \frac{FP}{(1 + i)^j}
$$

​	$FP$为每年固定偿付金额。

* **票息债券（coupon bond）**：每年支付固定利息，n年时偿还本金。其到期收益率公式如下：

$$
PV = \sum_{j = 1}^n\frac{C}{(1 + i)^j} + \frac{F}{(1 + i)^n}
$$

$C$为每年支付的利息；$F$为债券的面值（face value），即最后偿还的金额。

* **贴现发行债券（discount bond）**：到期按照面值偿付。其到期收益率公式如下：

$$
PV = \frac{CF}{(1 + i)^n}
$$

注：一般来讲贴现发行债券更常见，例如美国政府3月期国债就是贴现发行的债券。


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
