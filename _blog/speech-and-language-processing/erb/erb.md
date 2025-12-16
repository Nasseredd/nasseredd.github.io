---
title: "Equivalent Rectangular Bandwidth (ERB)"
permalink: /blog/speech-and-language-processing/erb
author_profile: true
---

<!-- Breadcrumb -->
<nav aria-label="breadcrumb" style="font-family: system-ui, sans-serif; font-size: 14px; margin-bottom: 1rem;">
  <style>
    .breadcrumb a {
      color: #666;
      text-decoration: none;
      transition: color 0.2s ease-in-out;
    }
    .breadcrumb a:hover {
      color: #333;
      text-decoration: underline;
    }
    .breadcrumb-separator {
      margin: 0 0.3rem;
      color: #999;
    }
  </style>

  <ol class="breadcrumb" style="display: flex; list-style: none; padding: 0; margin: 0; gap: 0.25rem;">
    <li style="display: flex; align-items: center;">
      <a href="/">Home</a>
      <span class="breadcrumb-separator">/</span>
    </li>
    <li style="display: flex; align-items: center;">
      <a href="/blog/">Blog</a>
      <span class="breadcrumb-separator">/</span>
    </li>
    <li style="display: flex; align-items: center;">
      <a href="/blog/speech-and-language-processing/">Speech and Language Processing</a>
    </li>
  </ol>
</nav>

<!-- Header -->

<div style="font-family: system-ui, sans-serif; font-size: 14px; color: #203657; margin-bottom: 1rem; line-height: 1.5;">
  <p style="margin: 0;">
    <span>Reading Time: ~20 min</span> • 
    <span>Last Modified: December 16, 2025</span>
  </p>
  <p style="margin: 2px 0 0 0;">
    <span>Keywords: </span>
    <span>#SignalProcessing,</span>
    <span>#SpeechProcessing,</span>
    <span>#Psychoacoustics,</span>
    <span>#ERB,</span>
    <span>#Filterbank,</span>
    <span>#STFT.</span>
  </p>
</div>

<!-- Article -->
## Introduction

<div style="text-align: justify; line-height: 1.6;">

    <p>
    The equivalent rectangular bandwidth (ERB) is a psychoacoustic frequency scale that models the frequency resolution of the human auditory system. It is widely used in speech processing, audio coding, and hearing research to design frequency representations that better match human perception.
    </p>

    <p>
    In many audio and speech applications, signals are first analyzed using a short-time Fourier transform (STFT), which provides a linear-frequency representation. However, human auditory perception does not resolve frequencies linearly: it has higher resolution at low frequencies and lower resolution at high frequencies. ERB filterbanks address this mismatch by grouping linear-frequency bins into perceptually motivated frequency bands.
    </p>

    <p>
    To convert a linear-frequency STFT into an ERB-band representation, we define a filterbank matrix that projects linear FFT bins onto ERB bands. Each ERB band is associated with one filter, which is fully characterized by three elements: its center frequency, its bandwidth, and its frequency response shape.
    </p>

    <p>
    Two related but distinct concepts are involved in ERB filterbank design. The ERB-rate defines a nonlinear perceptual frequency axis and is used to determine how filters are spaced perceptually. In contrast, the ERB bandwidth specifies the physical width (in Hz) of each filter at a given center frequency. Together, they define both the placement and the extent of the filters on the linear frequency axis.
    </p>

    <p>
    In the following, we assume that the time-domain signal has already been transformed into the linear-frequency STFT domain. Let \(X(f_k, t)\) denote the STFT, where \(f_k = \frac{k}{N} f_s\) is the \(k\)-th FFT frequency bin, \(N\) is the FFT size, \(t\) is the time-frame index, and \(f_s\) is the sampling frequency. We now explain how to construct an ERB filterbank and apply it to this representation.
    </p>

</div>

## Center frequencies
<div style="text-align: justify; line-height: 1.6;">

<p>In this section, we first explain the motivation behind each step involved in defining the center frequencies, without yet focusing on the computational procedure. Once the underlying ideas are clear, we then present the exact algorithmic steps required to compute the center frequencies.</p>

<p>By definition, the center frequency of a filter is the frequency at which its frequency response reaches its maximum value. It characterizes the location of the filter along the frequency axis, that is, the frequency region that the filter primarily captures. In an ERB filterbank, center frequencies are expressed on the linear (physical) frequency axis, but their distribution along this axis follows a non-linear, perceptually motivated spacing.</p>

<p>To clarify this distinction, let us illustrate it with a simple example. This first figure represents a linear-frequency axis, which is the coordinate system itself. Each tick corresponds to a physical frequency expressed in Hertz (Hz), and the distance between consecutive ticks is constant. This axis is therefore linear by construction.</p>

<div style="text-align: center; margin-bottom: 20px;">
  <img src="/files/blog/linear-axis.png" alt="Linear-Axis" style="max-width: 100%; height: auto; margin-top: 1rem;" />
</div>

<p>If we now want to select 6 center frequencies on this same linear-frequency axis and distribute them linearly, we choose them with a constant spacing along the axis. An example of such a linear distribution is shown in the second figure.</p>

<div style="text-align: center; margin-bottom: 20px;">
  <img src="/files/blog/linear-distribution.png" alt="Linear-Distribution" style="max-width: 100%; height: auto; margin-top: 1rem;" />
</div>

<p>In contrast, if we want to select 5 center frequencies on the same linear-frequency axis but distribute them non-linearly, we no longer enforce a constant spacing between consecutive centers. An example of such a non-linear distribution is shown in the third figure. Importantly, the axis remains linear; only the distribution of the center frequencies on this axis becomes non-linear.</p>

<div style="text-align: center; margin-bottom: 20px;">
  <img src="/files/blog/non-linear-distribution.png" alt="Non-Linear-Distribution" style="max-width: 100%; height: auto; margin-top: 1rem;" />
</div>

<p>In this regard, the ERB scale aims to place the center frequencies in a way that is perceptually aligned with the frequency resolution of the human auditory system. In order to know where to place these center frequencies (on the linear axis), we move to the ERB axis. Placing the center frequencies linearly on the ERB axis is equivalent to placing the center frequencies perceptually (non-linear) on the linear axis.</p>

<p>To this end, let \(f_b\) denote the center frequency of the \(b\)-th filter in the filterbank (expressed on the linear frequency axis), and \(e_b\) denote its corresponding ERB-rate coordinate (expressed on the ERB axis). The mapping between these two representations is defined by </p>


$$
e_b = \text{ERB}_{\text{rate}}(f_b) = 21.4 \;\cdot\;\text{log}_{10}(4.37 \;\cdot\; f_b/1000 +1)
$$

<p>Conversely, each ERB-rate coordinate \(e_b\) can be mapped back to its corresponding linear frequency \(f_b\) via the inverse ERB-rate transformation:</p>

$$
f_b = \frac{1000}{4.37} \;\Big( 10^{e_b/21.4} - 1\;\Big)
$$

<p>At this point, we understand that the procedure consists of first selecting ERB-rate coordinates \(e_b\) that are linearly distributed on the ERB axis, and then mapping them back to the center frequencies \(f_b\) that are distributed percentually (non-linearly) on the linear axis using the inverse ERB-rate transformation. </p>

<p>In order to determine the \(e_b\)coordinates, we simply divide the ERB axis in \(B\)desired segments linearly. The resulting coordinates are given by  \(e_b = e_{\text{min}} + b\cdot \Delta\), where the step size \(\Delta\) is defined as \(\Delta = \frac{e_{\text{max}} - e_{\text{min}}}{B-1}\), with \(b = 0, 1, \ldots, B-1.\).</p>

<p>However, this naive separation will lead to problems at edges as the first and the last ERB-rate coordinates (denoted \(e_{min}\) and \(e_{max}\) respectively) will be equal to 0 and </p>

<p>One might be tempted to divide the ERB axis uniformly starting from \(e_{\min}=0\), which corresponds to a center frequency at \(f_{min}=0\ \text{Hz}\). However, this will lead to boundary issues. Although the inverse ERB-rate mapping produces non-negative center frequencies, each filter has a finite bandwidth. As a result, a filter whose center frequency \(f_{min}=0\) will extend below \(0\ \text{Hz}\) once its bandwidth is taken into account. More specifically, since the filter bandwidth is split equally around the center frequency, half of it lies below and half above the center. When the center frequency is at \(f_{\min}=0\), the lower half of the bandwidth extends into negative frequencies, which is undesirable. A similar issue arises at the upper end of the spectrum, where filters placed too close (or equal) to the maximum frequency will extend beyond the intended frequency range \([0, f_s/2]\).</p>

<p>To avoid these edge effects, we first define a valid frequency range \([f_{\min},\,f_{\max}]\), such that \(f_{\text{min}} - \frac{\text{BW}(f_{\text{min}})}{2} \geq 0\)and \(f_{\text{max}} + \frac{\text{BW}(f_{\text{max}})}{2} \leq f_s/2\), with \(\text{BW}(f)\)is the bandwidth of the linear frequency bin \(f\). We then compute the corresponding ERB-rate bounds \(e_{\min}=\mathrm{ERB}_{\mathrm{rate}}(f_{\min})\)and \(e_{\max}=\mathrm{ERB}_{\mathrm{rate}}(f_{\max})\), and finally divide the ERB axis uniformly between \(e_{\min}\)and \(e_{\max}\). This ensures that all resulting center frequencies remain well defined within the target frequency range.</p>

</div>

In summary, the procedure consists of the following steps:

1. Choose the number of desired ERB bands $$B$$.
2. Choose the $$f_{\text{min}}$$ and $$f_{\text{max}}$$ such that $$f_{\text{min}} - \frac{\text{BW}(f_{\text{min}})}{2} \geq 0$$ and $$f_{\text{max}} + \frac{\text{BW}(f_{\text{max}})}{2} \leq f_s/2$$. 
3. Compute the ERB coordinates $$e_{\min} = \text{ERB}_{\text{rate}}(f_{\text{min}})$$ and $$e_{\max} = \text{ERB}_{\text{rate}}(f_{\text{max}})$$.
4. Uniformaly segment the ERB axis to get ERB coordinates $$\{e_b\}^{B-1}_{b=0}$$ such that  $$e_b = e_{\text{min}} + b\cdot \Delta$$ such that $$\Delta = \frac{e_{\text{max}} - e_{\text{min}}}{B-1}$$. 
5. For all $$b$$, compute the center frequency $$f_b$$ using the inverse ERB-rate as $$f_b = \frac{1000}{4.37} (10^{e_b/21.4} - 1)$$. 

## Band widths
<div style="text-align: justify; line-height: 1.6;">

<p>For each ERB center frequency \(f_b\) in the physical axis (linear), the perceptual bandwidth \(\text{BW}_b\) is defined as follows:</p>

$$
\text{BW}_b = \text{ERB}(f_b) = 24.7 \;\Big( 4.37 \times \frac{f_b}{1000} + 1\;\Big)
$$

<p>This gives the effective bandwidth (in Hz) of one auditory filter centered at frequency \(f_b\). It represents the width of an ideal rectangular filter that passes the same power as the true human auditory filter.</p>
</div>

## Filterbank

<div style="text-align: justify; line-height: 1.6;">

<p>Once the center frequencies \(\{f_b\}_{b=0}^{B-1}\) and their corresponding bandwidths \(\{\text{BW}_b\}_{b=0}^{B-1}\) are defined, each ERB filter must be assigned a frequency response shape. The role of this shape is to specify how each linear-frequency bin contributes to a given ERB band.</p>

<p>Let \(H_b(f_k)\) denote the frequency response of the \(b\)-th ERB filter at the linear FFT bin \(f_k\). In general, \(H_b(f_k)\) is a real, non-negative weighting function centered at \(f_b\) with effective support approximately equal to \(\text{BW}_b\).</p>

<p>Several shapes are used in the literature (gammatone, triangular, cosine), but for STFT-domain projections, smooth cosine or triangular shapes are most commonly used due to their numerical stability and ease of implementation.</p>

<p>The choice of the filter affects spectral leakage, overlap between adjacent ERB bands, and numerical conditioning, but does not modify the perceptual spacing governed by the ERB scale itself.</p>

<p>The full ERB filterbank is constructed by stacking the individual ERB filters along ERB-band index \(b\).</p>

<p>Let \(K\) denote the total number of linear FFT frequency bins in the STFT (typically \(K = \frac{N}{2}+1\) and an \(N\)-point FFT).</p>

<p>We define the ERB filterbank matrix \(H \in \mathbb{R}^{B\times K}\), whose entries are given by \(H_{b,k} = H_b(f_k)\) that is the chosen filter shape evaluated at \(f_k\).</p>

<p>In practice, the filters are designed to partially overlap in frequency in order to ensure a smooth spectral coverage and to avoid spectral holes.</p>

<p>Optional : To preserve signal energy after projection, it is common to normalize the filterbank along the ERB axis or along the frequency axis. A typical normalization is \(\sum_{b=0}^{B-1} H_{b,k} = 1\) for all \(k\), which guarantees that each linear-frequency bin contributes fully to the ERB representation without introducing global spectral attenuation or amplification.</p>

<p>This matrix \(H\) completely defines the linear-to-ERB frequency mapping and can be precomputed once for a given configuration \((f_s, N, B, f_{\min}, f_{\max})\).</p>

</div>

## Project the linear-frequency STFT onto the ERB band

<div style="text-align: justify; line-height: 1.6;">

<p>The projection of the linear-frequency STFT onto the ERB bands is performed by applying the ERB filterbank matrix \(H\) to the magnitude spectrum of \(X\).</p>

<p>Let \(\lvert X(f_k,t) \lvert\) denote the STFT magnitude. The ERB-band representation \(X_{\text{ERB}}(b,t)\) is defined as:</p>
</div>

$$
X_{\text{ERB}}(b,t) = \sum^{K-1}_{k=0} H_{b,k} \lvert X(f_k,t) \lvert
$$

This yields an ERB-band energy representation that is perceptually aligned with the frequency resolution of the human auditory system.