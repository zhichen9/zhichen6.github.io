---
title: Sampling Methods
date: 2021-11-08 19:57:16
toc: true
tags:
    - AST9240
---

[MCMC Interactive Gallary](https://chi-feng.github.io/mcmc-demo/app.html)

<!--more-->

# **Gaussian Sampling**

[AST9240 - Gaussian Sampling](https://www.youtube.com/watch?v=TH-X5aVG0Ic&list=PL0b6j-KLIuQMC1z2JjJYDdypUECWfIkH2&index=11)

## **Multidimensional Gaussian**

\\[ \bm{x}\sim\mathcal{N}(\bm{\mu}, C) \\]

where \\(C\\) is covariance matrix

\\[ C=\langle \bm{x}\bm{x}^T\rangle - \langle\bm{x}\rangle\langle\bm{x}\rangle^T \\]

The log-likelihood is

\\[ \ln\mathcal{L}(\bm{x}|\bm{\mu})=\mathrm{const.} - \frac{1}{2}(\bm{x}-\bm{\mu})^TC^{-1}(\bm{x}-\bm{\mu}) \\]

The sample of \\(\bm\mu\\) is

\\[\bm{\mu}=\bm{x}+C^{1/2}\bm{\eta} \\]

\\(C^{1/2}\bm{\eta}\\) is **flunctuation term**, and \\(C^{1/2}\\) satisfies

\\[C^{1/2}(C^{1/2})^T=C\\]

## **d = As+n**

Often we have

\\[\color{red}\bm{d}=A\bm{s}+\bm{n}\\]

and covariance matrix of noise \\(\bm n\\)

\\[ \langle\bm{n}\bm{n}^T\rangle = N \\]

Here \\(A\\) can be pointing matrix, mixing matrix, etc in different contexts. The log-likelihood is

\\[\ln P(\bm{d}|\bm{s}) = \mathrm{const.} - \frac{1}{2}(\bm{d}-A\bm{s})^TN^{-1}(\bm{d}-A\bm{s})\\]

Take derivative of the likelihood and make it equal to zero

\\[ \begin{aligned} \frac{\mathrm{d}\ln\mathcal{L}(\bm{d}|\bm{s})}{\mathrm{d}\bm{s}}&\propto-\frac{\mathrm{d}}{\mathrm{d}\bm{s}}(\bm{d}-A\bm{s})^TN^{-1}(\bm{d}-A\bm{s}) \\\ &=A^TN^{-1}(\bm{d}-A\bm{s})+(\bm{d}-A\bm{s})^TN^{-1}A=0 \end{aligned} \\]

The two terms \\(A^TN^{-1}(\bm{d}-A\bm{s})\\) and \\((\bm{d}-A\bm{s})^TN^{-1}A\\) are equivalent, and we get the maximum likelihood solution

\\[ \bm{s}=(A^TN^{-1}A)^{-1}A^TN^{-1}\bm{d} \\]

上面的求逆从数值上是非常困难的，所以我们经常写成下面这种形式

\\[\color{red} (A^TN^{-1}A)\bm{s}=A^TN^{-1}\bm{d} \\]

这就是 \\(A\bm{x}=\bm{b}\\) 的形式，可以用 Conjugate Gradient 的方法来求解（可以看[Painless conjugate gradient](https://www.cs.cmu.edu/~quake-papers/painless-conjugate-gradient.pdf)快速掌握 CG 算法）。到此为止，我们还差一个 **flunctuation term**，需要求 \\(\bm{s}\\) 的协方差矩阵

\\[ \langle\bm{s}\bm{s}\rangle - \langle\bm{s}\rangle\langle\bm{s}\rangle^T =(A^TN^{-1}A)^{-1} \\]

实际上，上面这个操作把 \\(\bm{n}\\) 的协方差矩阵转换到 \\(\bm{s}\\) 的空间下。如果 \\(\bm{d}\\) 是 TOD 数据，\\(\bm{s}\\) 是一张天图，\\(A\\) 是 mapmaking 的操作，那么这就是把协方差矩阵从时间带到像素空间中，相当于误差传递的过程。

The sample is

\\[ \bm{s}=(A^TN^{-1}A)^{-1}A^TN^{-1}\bm{d}+A^TN^{1/2}\bm{\eta} \\]

## **With a prior on s**

If the prior is gaussian, then

\\[\ln P(\bm{d}|\bm{s}) = \mathrm{const.} - \frac{1}{2}(\bm{d}-A\bm{s})^TN^{-1}(\bm{d}-A\bm{s}) - \frac{1}{2}(\bm{s}-\bm{\mu}_s)^TS^{-1}(\bm{s}-\bm{\mu}_s)\\]

The sample becomes

\\[ (A^TN^{-1}A+S^{-1})\bm{s}=A^TN^{-1}\bm{d}+S^{-1}\bm{\mu}_s+A^TN^{1/2}\bm{\eta}_1+S^{1/2}\bm{\eta}_2 \\]

The covariance matrix of \\(\bm{s}\\) is

\\[ \langle\bm{s}\bm{s}\rangle - \langle\bm{s}\rangle\langle\bm{s}\rangle^T =(A^TN^{-1}A+S^{-1})^{-1} \\]

在前景分析中，各种前景成分的 amplitude 可以采用 Gaussian sampling 的方法，因为 amplitude 和数据的关系是线性的，如果噪声是高斯的，那么前景的 amplitude 也是高斯的。

# **Inversion sampling**

[AST9240 - Inversion Sampling](https://www.youtube.com/watch?v=X9zbSujqnh4&list=PL0b6j-KLIuQMC1z2JjJYDdypUECWfIkH2&index=12)

在前景分析中，谱指数可以用 Inversion sampling 的方法，Inversion sampling 可以应用到任何概率分布上。

# **Metropolis sampling**

[AST9240 - Monte Carlo sampling methods](https://www.youtube.com/watch?v=50nu5_qzedM&list=PL0b6j-KLIuQMC1z2JjJYDdypUECWfIkH2&index=2)

## **Metropolis-Hastings sampling**

Allows for asymmetric transition rules.

# **Gibbs sampling**

Basis of Commander3. See Gibbs Sampling in MCMC Interactive Gallary.

我们本来需要计算 \\( P(h, g, s_\mathrm{cmb}, b|\bm{d}) \\)，采用 Gibbs 采样方法，我们只需要去计算

\\[\begin{aligned} &P(h|\bm{d},g,s_\mathrm{cmb},b) \\\ &P(g|\bm{d}, h, s_\mathrm{cmb}, b) \\\ &P(s_\mathrm{cmb}|\bm{d}, h, g, b) \\\ &P(b|\bm{d}, h, g, s_\mathrm{cmb}) \end{aligned}\\]

而这些都是非常好计算的，甚至有一些有解析的形式。

[Jinyi_gibbs_sampler](https://jinyiliu.github.io/html/Jinyi_gibbs_sampler.html)

</br>
