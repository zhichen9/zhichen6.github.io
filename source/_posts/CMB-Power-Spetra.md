---
title: CMB Power Spectra
date: 2021-11-29 13:39:31
toc: true
tags:
    - CMB
---

这是偏数学的背景辐射功率谱介绍，参考 [Tojeiro 2006](https://www.roe.ac.uk/ifa/postgrad/pedagogy/2006_tojeiro.pdf) 和 [Bartlett 2001](https://www.sciencedirect.com/science/article/pii/S1387647300001500) 文章，最早是 [Bond & Efstathiou 1987](https://ui.adsabs.harvard.edu/abs/1987MNRAS.226..655B/abstract) 这篇文章提出的。

<!--more-->

## **Definition**

因为微波背景辐射是各向同性的，以温度扰动为例，所以不同方向处的温度扰动可以写成下面这样的形式

\\[\color{black}\begin{aligned}C(\bm{n},\bm{n}^\prime)&=\langle T(\bm{n})T(\bm{n}^\prime) \rangle_\mathrm{ens}=C(\theta)\\\ &=\frac{1}{4\pi}\sum_\ell (2\ell+1)C_\ell P_\ell(\cos\theta)=\sum_{\ell m}C_\ell Y_{\ell m}^*(\bm{n})Y_{\ell m}(\bm{n}^\prime)\end{aligned}\\]

其中 \\(\bm{n}\cdot\bm{n}^\prime=\cos\theta\\)，将 \\(T(\bm{n})\\) 球谐展开，可以得到

\\[\color{black}C_\ell=\langle a_{\ell m}^* a_{\ell m}^{}  \rangle_\mathrm{ens}\\]

## **Scaling**

\\[\color{black}D_\ell=\frac{\ell(\ell+1)}{2\pi}C_\ell\\]

{% blockquote "Bond, Jaffle & Knox 1998" https://arxiv.org/pdf/astro-ph/9708203.pdf "Estimating the Power Spectrum of the CMB" %}
This is useful for two reasons: it is logarithmic average of \\(D_\ell\\) that gives the variance of the data and (therefore) for scale-invariant theories of structure formation, \\(D_\ell\\) is roughly constant at large scales.
{% endblockquote %}

## **Cosmic Variance**

我们实际只能观测到一张天图，也就是一个随机实现，所以我们能够得到的功率谱实际上是

\\[\color{black}\hat{C}_\ell=\frac{1}{2\ell+1}\sum_m a_\{\ell m\}^* a_\{\ell m\}^{}\\]

所以这会天然地引入误差。





## **Phase**

在从天图提取功率谱的同时，我们会丢失相位信息。

