---
title: Foregrounds in CMB physics
date: 2021-10-19 16:39:12
toc: true
tags:
    - Physics
    - CMB
    - AST9240
---

前景最关键的地方在于给不同类型的前景建模，找到和观测最符合的SED（Spectral Energy Distribution），这样才能在多频段观测的 CMB 实验中进行精确的 component seperation 过程。

<!--more-->

## **Overview**


<div style="text-align:center">
{% asset_img foregrounds_amplitude_temp.png 490 '"" ""' %}
{% asset_img foregrounds_amplitude_pol.png 487 '"" "Temprature (top) and polarization (bottom) amplitude rms as a function of frequency and astrophysical components [Planck Coll. X 2016]"' %}
</div>



## **Synchrotron**

[AST9240 - Synchrotron Emission](https://www.youtube.com/watch?v=T3d15LjFzVA&list=PL0b6j-KLIuQMC1z2JjJYDdypUECWfIkH2&index=8)


### **Start with Single particel to ensemble**

相对论性电子在磁场中的运动方程是

\\[\frac{\mathrm{d}}{\mathrm{d}t}(\gamma m_e \bm{v})=\frac{e}{c}(\bm{v}\times \bm{B})  \\]

磁场不做功，所以有

\\[\frac{\mathrm{d}}{\mathrm{d}t}(\gamma m_e c^2)=0 \\\ \frac{\mathrm{d}\gamma}{\mathrm{d}t}=0 \\]

之前的运动方程变成

\\[ \gamma m_e\frac{\mathrm{d}\bm{v}}{\mathrm{d}t}=\frac{e}{c}(\bm{v}\times\bm{B}) \\]

将速度分解为平行于磁场的方向和垂直于磁场的方向，的到两个方程

\\[\frac{\mathrm{d}\bm{v}_\parallel}{\mathrm{d}t}=0 \\\ \frac{\mathrm{d}\bm{v}_\bot}{\mathrm{d}t}=\frac{e}{\gamma m_e c}\bm{v}_\bot\times\bm{B}  \\]

垂直于磁场方向的运动就是匀速圆周运动。可以的到同步辐射的示意图

<div style="text-align:center">
{% asset_img synchrotron.png 400 '"" ""' %}
</div>
<br/>

**Gyration frequency**

\\[ \omega=\frac{eB}{\gamma m_e c} \\]

**Power emitted**

\\[ P=\frac{2e^2\gamma^4\omega^2 v^2_\bot}{3c^2} \\]

在非相对论的情况下（cyclotron radiation），观测者在任何一个角度看到的磁场频率都是 \\(\omega\\)，观测者看到的频谱在 \\(\omega\\)处有一个非常尖锐的峰值。但是在非相对论的情况下，因为存在集束效应（beamming effect），频谱会拓宽一些。

<div style="text-align:center">
{% asset_img synch_beamming.gif 400 '"" ""' %}
</div>
<br/>

可以证明在频率 \\(\omega\\) 处辐射功率是

\\[ P(\omega)=\frac{\sqrt{3}}{2\pi}\frac{e^3B\sin\alpha}{m_e c^2}F\left(\frac{\omega}{\omega_c}\right) \\]

其中

\\[ \omega_c=\frac{3\gamma^2 eB\sin\alpha}{2m_e c} \\]

假设电子的能量分布符合幂律分布

\\[ N(\gamma)\mathrm{d}\gamma=N_0\gamma^{-p}\mathrm{d}\gamma \\]

那么

\\[ P(\omega)\propto \int_{\gamma_1}^{\gamma_2} F\left(\frac{\omega}{\omega_c} \right)\gamma^{-p} \mathrm{d}\gamma \\]

下面把 \\(x=\omega/\omega_c\\)

\\[ P(\omega)\propto \omega^{-(p-1)/2} \int_{x_1}^{x_2} F(x)x^{(p-3)/2}\mathrm{d}x \\]

只要积分区间足够大，上面就可以简化为

\\[ \color{blue}{ P(\omega)\propto\omega^{-(p-1)/2}  } \\]

可以看出同步辐射的SED只依赖于电子能量分布。在有更强的磁场的地方，电子的能量更高，但是这不会改变同步辐射能谱的形状。我们现在的观测有 \\(p=3\\) 左右。


### **Polarization**

同步辐射的光子中是偏振光子的百分率是

\\[ \Pi=\frac{p+1}{p+7/3} \\]

对于 \\(p=3\\) 的情况，有75%的同步辐射光子都是偏振的。


### **Faraday Rotation**

同步辐射建模的其中一个困难在于法拉第旋转，尤其在低频。

### **Data**

- Halsam
- S-PASS
- C-BASS
- QUIJOTE

### **Spetral Index Variantions**

在不同区域，电子能量分布的谱指数 \\(p\\)是不一样的。

### **Synchrotron-Dust Correlation**

同步辐射和尘埃分布会有一定相关性，但是因为同步辐射同时依赖于磁场强度以及宇宙线的分布，而尘埃是不依赖于磁场强度的，所以相关性不会特别强。






## **Thermal dust**

[AST9240 - Dust](https://www.youtube.com/watch?v=LB8kBo8xd3c&list=PL0b6j-KLIuQMC1z2JjJYDdypUECWfIkH2&index=9)

### **Dust Specs**

- Mainly composed of C, O, Mg, Si and Fe
- From 0.01-0.2 μm in size
- Absorbs starlight (UV), emits thermally (FIR)
- Typically ~1% of ISM mass


### **Observables**

- Extinction: the total extinction is significantly stronger than the polarized extinction
- Thermal Emission

### **Dust Polarization**

The dust must be both aspherical and aligned (under magnetic field).

The composition of dust grains are mostly carbonaceous and silicate in nature. Silicate features indicate robost polarization. Carbonaceous features notably lack polarization signatures.

### **SED: Modified Blackbody Model (MBB)**

\\[ I_\nu=A\left(\frac{\nu}{\nu_0}\right)^\beta B_\nu(T_d) \\]

where \\(A\\) is the amout of dust, \\(\beta\\) represents dust composition, \\(T_d\\) is the dust temperature. Planck found that a single modified blackbody component is adequate for describing the emission thoughout the planck data.

[Meisner and Finkbeiner (2014)](https://arxiv.org/abs/1410.7523) prefers two components.

<div style="text-align:center">
{% asset_img meisner_and_finkbeiner.png 490 '"" ""' %}
</div>
<br/>

除了尘埃颗粒组分上的差别会影响到SED建模的难度，尘埃的空间分布也会影响。

### **SED Variations and Decorrelation**

SED建模还有一些其它困难，比如

- Dust SED may vary along the line of sight
- Decorrelation is a problem in polarization. Line of sight changes in magnetic field directions can enhance SED variations.

第二个没听明白。

### **HI Dust Correlations**

<div style="text-align:center">
{% asset_img Planck_dust_density.png 470 '"" ""' %}
{% asset_img HI_column_density.png 470 '"" "The morphology of these two abservables are very similar."' %}
</div>


## **Free-Free**

在HII区域，电子经过带正电的离子或质子时，受到加速而产生的辐射。轫制辐射本身并不是偏振的，但是在HII区域可能会发生汤姆逊散射从而导致光子的偏振，如果我们有足够高的分辨率在HII区域是可以看到偏振光子的，但是现有的分辨率不够高，所以一般在偏振实验中不考虑轫制辐射。



## **CIB**

CIB是河外一些正在形成恒星的星系辐射的，不同频段之间的CIB并没有什么相关性，所以从CMB中提取CIB信息是一件没那么容易的事情。一般而言可以利用HI来扣除银河系尘埃对CIB的污染。

<div style="text-align:center">
{% asset_img CIB.png 470 '"" ""' %}
</div>


## **CO**

CO分子在115GHz、230GHz、345GHz有发射线，在一些特定的区域比如大麦和小麦，有大约1%的偏振。CO会产生大约在 \\(r\lesssim0.02\\) 的地方产生B模式偏振。


## **AME**

[AST9240 - Anomalous Microwave Emission (AME)](https://www.youtube.com/watch?v=plr_JgwDPlw&list=PL0b6j-KLIuQMC1z2JjJYDdypUECWfIkH2&index=7)

一个电偶极子或磁偶极子在旋转的时候会发出辐射。AME（Anomalous Microwave Emission）现阶段认为是极其小（小于1纳米）的尘埃颗粒在几十GHz上的自旋造成的，这样的辐射来源称为旋转的灰尘（spinning dust）。

## **Zodiacal Emission**

[AST9240 - Zodiacal Emission](https://www.youtube.com/watch?v=Cq1WI7nHgnQ&list=PL0b6j-KLIuQMC1z2JjJYDdypUECWfIkH2&index=5)

<div style="text-align:center">
{% asset_img zodiacal_light.jpeg 400 '"" "Zodiacal light seen from ESO."' %}
</div>
<br/>

上面的图片是可见光波段内太阳系内的尘埃反射太阳光而形成的，这本身不会对CMB实验产生影响，但是这些尘埃被太阳光加热而释放出FIR波段的热辐射会对CMB实验，尤其是高频波段产生干扰。

Zodiacal emission is **spatial dependent**.

<div style="text-align:center">
{% asset_img zodiacal_spatical_dependent.png '"" "Observer location dependent."' %}
</div>
<br/>

黄道辐射和空间位置是相关的，所以最后观测到的黄道辐射和具体的巡天策略有关，不同的实验是不一样的。Planck实验中黄道辐射在857GHz频段最明显，但是对于现阶段的阿里实验，我猜想应该不太需要考虑来自黄道的辐射。

There is no universal template for zodiacal emission. We need to make custom maps for each dataset. To produce such maps, we need
- A model of the interplanetary dust
- Perform line-of-sight integrals for each observation


[Planck 2013 results. XIV. Zodiacal Emission](https://www.aanda.org/articles/aa/pdf/2014/11/aa21562-13.pdf)



<br/>
