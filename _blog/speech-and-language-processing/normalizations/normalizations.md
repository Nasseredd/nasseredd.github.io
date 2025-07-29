---
title: "Normalizing Signals"
permalink: /blog/speech-and-language-processing/normalizations
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
    <span>Reading Time: ~7 min</span> • 
    <span>Last Modified: July 29, 2025</span>
  </p>
  <p style="margin: 2px 0 0 0;">
    <span>Keywords: </span>
    <span>#SpeechProcessing,</span>
    <span>#Mixture,</span>
    <span>#Noise,</span>
    <span>#Signal-to-Noise Ratio.</span>
  </p>
</div>

<!-- Article -->
## I. Time-Domain Normalizations

**Peak Normalization**

<p style="text-align: justify;">
One common type of normalization is peak normalization, which operates directly on the raw waveform. The goal here is to ensure that the maximum absolute amplitude of the signal reaches a predefined value, typically 1.0. This is done by dividing each sample of the waveform by the maximum absolute value across the entire signal:
</p>

$$
x_{\text{norm}}(t) = \frac{x(t)}{\max_t |x(t)|}
$$

<p style="text-align: justify;">
This keeps the waveform shape unchanged but scales it so that the largest peak is at the desired level.
</p>

**RMS (Root Mean Square) Normalization** 

<p style="text-align: justify;">
RMS normalization  adjusts the signal so that its overall energy, measured as root-mean-square (RMS) value, matches a target level. This is especially useful when two signals may have the same peak amplitude but differ in perceived loudness due to different energy distributions. The formula for RMS normalization is:
</p>

$$
x_{\text{norm}}(t) = \frac{x(t)}{\text{RMS}(x)} \cdot \text{Target}_{RMS}
$$

<p style="text-align: justify;">
where \(\text{RMS}(x) = \sqrt{\frac{1}{T} \sum_{t=1}^{T} x(t)^2}\), and \(T\) is the number of samples in the signal.
</p>

**Mean Normalization (DC Offset Removal)** 

<p style="text-align: justify;">
A simpler form of normalization is mean normalization, also known as DC offset removal. This technique removes any constant bias in the signal by subtracting the mean value:
</p>

$$
x_{\text{norm}}(t) = x(t) - \mu
$$

<p style="text-align: justify;">
  where \(\mu\) is the average value of the waveform. Since speech should ideally oscillate around zero, this step ensures the signal is centered.
</p>

**Z-Score Normalization (Standardization)** 

<p style="text-align: justify;">
A more general form is z-score normalization or standardization, which transforms the signal so that it has zero mean and unit variance. This is especially useful in machine learning contexts, where models often assume input features have similar statistical properties. The transformation is defined as:
</p>

$$
x_{\text{norm}}(t) = \frac{x(t) - \mu}{\sigma}
$$

<p style="text-align: justify;">
where \(\mu\) is the mean and \(\sigma\) is the standard deviation of the waveform.
</p>

## II. Frequency-Domain Normalizations

**Per-Frame Normalization**

<p style="text-align: justify;">
Normalizations can also be applied in the spectral domain, after converting the signal into a time-frequency representation such as a spectrogram. In per-frame normalization, each time frame of the spectrogram is normalized to have zero mean and unit variance across frequency:
</p>

$$
S_{\text{norm}}(f, t) = \frac{S(f,t) - \mu_t}{\sigma_t}
$$

<p style="text-align: justify;">
Here, \(\mu_t\) and \(\sigma_t\) are the mean and standard deviation of the spectral values at time \(t\), across all frequencies \(f\). This kind of normalization helps reduce variations due to environmental noise or loudness that affect the entire frame.
</p>

**Per-Frequency Normalization**

<p style="text-align: justify;">
Conversely, per-frequency normalization normalizes each frequency bin across time, which is useful when some frequency bands are consistently stronger due to recording conditions or channel characteristics. In this case, the normalization is written as:
</p>

$$
S_{\text{norm}}(f, t) = \frac{S(f,t) - \mu_f}{\sigma_f}
$$

<p style="text-align: justify;">
where \(\mu_f\) and \(\sigma_f\) are computed across time for each frequency bin \(f\).
</p>

## Conclusion

<p style="text-align: justify;">
Each of these normalization methods serves a specific purpose and is often combined with others in practical speech processing pipelines. They help ensure that models or algorithms are not biased by irrelevant differences in amplitude or energy that are not part of the speech content itself.
</p>
