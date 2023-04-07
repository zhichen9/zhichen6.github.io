---
title: VLA Continuum Tutorial 3C391
date: 2022-12-09 14:03:47
toc: true
article:
    highlight:
        theme: atom-one-light
        fold: folded
tags:
    - RadioAstro
    - SIW2022
---

[VLA Continuum Tutorial 3C391-CASA5.5.0](https://casaguides.nrao.edu/index.php?title=VLA_Continuum_Tutorial_3C391-CASA5.5.0)

<!--3C 286 in optical and in radio-->

<!--more-->

After flagging the data.

## **Examining the data**

<div style="text-align:center">
{% asset_img Amp_Time.png '"" "Black dots are observations of flex density calibrator 3C 286 which is a nearly perfect point source. Magenta dots are observations of gain calibrator. Light purple dots in the last are observations of polarization calibrators."' %}
</div></br>

Below we can see the flagging process has taken effect.

<div style="text-align:center">
{% asset_img Amp_Scan.png '"" "Data from Scan 1 has been flagged so we can not see them."' %}
</div></br>

<div style="text-align:center">
{% asset_img Antenna1_Time.png '"" "There is no data from antenna ID 10 and 12 because their corresponding antennas ea13 and ea15 have corrupted data."' %}
</div></br>

<div style="text-align:center">
{% asset_img Amp_UVdist_3C286.png '"" "Visibility amplitudes of 3C 286. Should be a horizontal line after calibration."' %}
</div></br>

<div style="text-align:center">
{% asset_img Amp_UVdist_3C391_C2.png '"" "Visibility amplitudes of 3C 391 (mosaic C2)."' %}
</div></br>

<div style="text-align:center">
{% asset_img Phase_Frequency_3C286_ea01&ea21.png '"" "The slopes are steady over time. The two different lines for each baseline correspond to the RR and LL correlations."' %}
</div></br>

The phase \\(\color{black}\theta=2\pi f \bm{b}\cdot\bm{s}/c\\) is linearly dependent on frequency and the slope is \\(\color{black}2\pi\bm{b}\cdot\bm{s}/c\\). If we set `iteraxis=baseline` in `plotms` function, by clicking on the green arrow Next button we can switch the plots between different baselines and we will see that different baselines have different slopes.

## **Reference Antenna**

Phase solutions are typically referred to a specific antenna. Phase corresponds to position. What we need is actually to align all the source positions to one point and it doesn't matter where the point is.

Often we require the antenna be available over the entire observation. And in general, for calibration purposes, we would like to select an antenna that is close to the center of the array (<font color="blue">but why?</font>).

Use `plotant` to show the antenna positions.

<div style="text-align:center">
{% asset_img ant.png '"" "VLA D-configuration. There are two spectral windows around 4.6 and 7.5 GHz. Observations of 3C 391 in this tutorial focus on 4.6 GHz. And there are 64 frequency channels in that spectral window."' %}
</div></br>

We will use antenna ea21 as the ref antenna later on.


## **Calibrating the Data**

The calibration process in the tutorial is a bit different from the calibration lecture in the workshop. The observed visibility function is related to the true visibility by

\\[\color{black}V_{ij}^\prime=b_{ij}(t)B_i(f,t)B_j^*(f,t)g_i(t)g_j(t)e^{i[\theta_i(t)-\theta_j(t)]}V_{ij}\\]

In `CASA` the task `gencal` can specify calibration values of various types providing a means of antenna-based calibration values mannually.

### **Antenna Position Corrections**

Specify values for \\(\color{black}b_{ij}(t)\\).

### **Initial Flux Density Scaling**

Use task `setjy` to place the model visibility amplitude for the flux density calibrator 3C 286. By comparison with the observed data, determine the \\(\color{black}g_i\\) values.

### **Initial Phase Calibration**

First we calculate the gain with task `gaincal` using all three calibrators to see if there are some bad data.

<div style="text-align:center">
{% asset_img G0all_GainPhase_Time_ea21.png '"" "Gain phase is apparently zero for ref antenna ea21."' %}
</div></br>

<div style="text-align:center">
{% asset_img G0all_GainPhase_Time_ea04.png '"" "For most antennas, we see a fairly smooth variation with time."' %}
</div></br>

<div style="text-align:center">
{% asset_img G0all_GainPhase_Time_ea05.png '"" "There are phase jumps in ea05 gain phase."' %}
</div></br>

Antennas other than ea05 look OK so we flag it from the data. And again this time we use `gaincal` to calculate the gain using only the bandpass calibrator.

<div style="text-align:center">
{% asset_img G0_GainPhase_Time_ea03.png '"" ""' %}
</div></br>

<div style="text-align:center">
{% asset_img G0_GainPhase_Time_ea04.png '"" ""' %}
</div></br>

<font color="blue">Still don't completely understand this calibration step.</font>


### **Delay Calibration**

<div style="text-align:center">
{% asset_img delay.png '"" "This corrects the bandpass delay."' %}
</div></br>

This step solves for the antenna-based delays (See Phase vs. Frequency plot above). Use `gaincal` with gaintype K to solve for the relative delay of each antenna relative to the reference antenna.

也就是说这里修正了不同天线的时间延迟，会让上面那一张 Phase vs. Frequency 的图里的曲线变成水平直线。

### **Bandpass Calibration**

<div style="text-align:center">
{% asset_img Amp_Channel.png '"" "Colorized by antenna2."' %}
</div></br>

The task `bandpass` calculates the amplitude and phase as a function of frequency for each spectral window containing more than on channel. Correspondes to the complex bandpass \\(\color{black}B_i(f,t)\\).

<div style="text-align:center">
{% asset_img BandpassAmp.png '"" "The black and magenta colors are RR and LL correlation respectively."' %}
</div></br>

<div style="text-align:center">
{% asset_img BandpassPhase.png '"" "Bandpass phases are relatively, the slopes are removed by the delay calibration."' %}
</div></br>



### **Gain Calibration**

First, they use flux density calibrator 3C 286 to calculate the appropriate complex gains \\(\color{black}g_i\\) and \\(\color{black}\theta_i\\). Second, to minimize the differences through the atmosphere between the lines of sight to the gain calibrator 3C 286 and the target source, we also need to establish relative gain amplitudes and phases for different antennas using **phase calibrator**. The appropriate complex gains for a direction on the sky close to the target source will be determined from the phase calibrator.

<div style="text-align:center">
{% asset_img G1-phase_Poln0,1.png '"" "Colorized by baseline."' %}
</div></br>

<div style="text-align:center">
{% asset_img G1-amp_Poln0,1.png '"" "Colorized by baseline."' %}
</div></br>

已经开始看不明白了，就不能多写一点公式嘛！

### **Scaling the Amplitude Gains**

我不理解。你为啥不理解？你要理解！真不理解。


### **Applying the Calibration**

Use `applycal` to apply the calibration solutions to flux density calibrators J1331-3030(3C 286), visibility phase calibrator J1822-0938, target fields in the mosaic. Then we now have fully-calibrated visibilities in the CORRECTED-DATA column of the measurement set.

<div style="text-align:center">
{% asset_img 3C286-corrected-Amp_Channel.png '"" "3C286 corrected Amp vs Channel."' %}
</div></br>

<div style="text-align:center">
{% asset_img 3C286-corrected-Phase_Channel.png '"" "3C286 corrected Phase vs Channel."' %}
</div></br>

Then split off the target fields by `split` to create a new, calibrated measurement set containing all the target fields. After that, run `statwt` task to correct the data weights in the measurement set based on the variance of data.

总而言之，校准完毕！

## **Imaging**

Examine the newly calibrated data.

<div style="text-align:center">
{% asset_img 3C391-calibrated-Amp_UVwave.png '"" "3C391 newly calibrated Amp vs UVwave."' %}
</div></br>

### **Imaging parameters**

It is important to have an idea of what values to use for the image pixel (cell) size. The maximum baseline is about 16,000 wavelengths, i.e., the smallest angular scale of 12 arcseconds. <font color="red">The most effective cleaning occurs with at least 4-5 pixels across the synthesized beam</font>. As such, we can chose the value of 2.5 arcseconds as the cell size.

Set the image size = [480,480] in this case to fully cover the supernova remnant and also take into account of FFT efficiency.

### **Multi-scale Mosaic Clean**

Can't believe this is not done automatically. I have to open a graphic viewer and select some clean regions **mannually** at the start of clean algorithm iterations.

Finally use `viewer` to show the cleaned image. In the DATA DISPLAY OPTIONS -> BASIC SETTINGS, I set the colormap to Hot Metal 2 and Scaling Power Cycles to -0.5. Here is what I get

<div style="text-align:center">
{% asset_img 3C391_clean_image.png '"" "3C391 clean image. The left bottom white circle is the beam size."' %}
</div></br>


### **Image Analysis**

Use CASA to determine the peak brightness, flux density and image noise level. Didn't do this.






