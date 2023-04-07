---
title: Calibration in Radio
date: 2022-11-12 10:50:13
tags:
    - RadioAstro
    - SIW2022
---

- [Calibration](http://www.aoc.nrao.edu/events/synthesis/2022/slides/Calibration-2022.pdf)

觉得这个报告讲得不是很清晰详细，只弄明白了皮毛。

The calibration in this lecture deals primarily with correcting the (baseline-based) visibilities for antenna-based effects.


<!--more-->

## **Solving for Calibration**

We have an imperfect visibility measurment per antenna pair:

\\[\color{black}V_{ij}^\mathrm{obs}(u,v)=J_iJ_j^*V_{ij}^\mathrm{true}(u,v)\\]

The desired visibilieis were corrupted by the factor \\(\color{black}J_iJ_j^*\\). To address all the effects more accurately, we can decompose \\(\color{black}J_i\\) into separate components.

F = ionospheric effects
T = tropospheric effects
P = parallactic angle
E = antenna voltage pattern and gain curve
G = electronic gain
K = geometry
X = **<font color="red">Pol Angle</font>** -- linear polarization position angle
D = **<font color="green">Pol Leakage</font>** -- polarization leakage
B = **<font color="blue">Bandpass</font>** -- bandpass response

Some of these effects may not be so important in your observation. For example if you are observing at high radio frequencies, then ionospheric effects are negligible because they only becomes domianted at lower frequencies (<5GHz). And polarization calibration may not be not important in your data reduction if the intensity distribution is the only thing you care about.

And some of these effects can be derived using external information, the observatory will provide you like F, T, P, E and parts of G, K.

But there are still some left which we need to rely on observing calibrator sources.

**<font color="lime">NOTE</font>** that here the effects we are talking about is mainly direction independent which is to say the corruption factor \\(\color{black}J_i(t)\\) is only a function of time for each antenna and frequency channel. However, direction dependent calibration \\(\color{black}J_i(t,l,m)\\) should be taken into account when it comes to wide field imaging.

### **Advanced Techniques**

- Make use of ancillary hardware when available
- Self calibration
- Baseline-based calibration
- Direction dependent calibration


## **Observaing Calibrator Sources**

<div style="text-align:center">
{% asset_img calibration.png '"" ""' %}
</div></br>

**<font color="red">Flux density</font>**: standard candle with known structure and SED.
**<font color="blue">Delay & Bandpass</font>**: very bright and preferably unresolved source.
**<font color="green">Gain</font>**: bright and preferably unresolved source with accurate position. Ideally very close to the **<font color="orange">traget source</font>** and observe before and after the **<font color="orange">traget source</font>**.

**<font color="red">Pol Angle</font>**: polarized source with full Stokes model.
**<font color="green">Pol Leakage</font>**: unpolarized and preferably unresolved.




