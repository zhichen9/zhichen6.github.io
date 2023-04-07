---
title: ICARUS博客写作备忘录
date: 2021-10-07 10:59:44
toc: true
tags:
    - blog
---

## <span id='Code'>Code</span>

This is a code block.

{% codeblock test.py lang:python line_number:false https://githun.com GitHub %}
import numpy as np

data = np.random.normal(10)
print(data)
{% endcodeblock %}

<!--more-->

Include code like this, this is a part of code `sinx.f90`:

{% include_code DO WHILE Loop lang:fortran from:7 to:13 sinx.f90 %}

## KaTeX

This is an inline expression \\(a=b+c\\).

This is a block expression.

\\[F(x)=\int_{-\infty}^\infty f(x)\mathrm{d}x \\\ f(x)=F^\prime(x) \\]

Use `\begin{aligned}` and `\end{aligned}` instead of `\begin{split}` and `\end{split}`.

Use `\\\` instead of `\\` to indicate a new line in the expression.


## Image

This is an asset image.

<div style="text-align:center">
{% asset_img kikyo.jpg 400 '"Kikyo" "桔梗，日本漫画《犬夜叉》中的角色，战国时代灵力数一数二的巫女"' %}
</div>


## Quote

This is a quote.

{% blockquote 鲁迅 %}
在我的后园，可以看见墙外有两株树，一株是枣树，还有一株也是枣树。
{% endblockquote %}

## HTML

This is a blank line.

<br/>

This is <font color="red">colored</font> text.

## Info Box

<article class="message message-immersive is-warning">
  <div class="message-body">
    <i class="fas fa-question-circle mr-2"></i>文章内容有误？
  </div>
</article>

## Others

Mail to me <liujy0129@gmail.com>.

Jump to [Code](#Code).

<!--上下标-->
