---
title: "Normalizing Signals"
permalink: /blog/speech-and-language-processing
author_profile: true
---

### Time-Domain Normalizations

**Peak Normalization**

One common type of normalization is peak normalization, which operates directly on the raw waveform. The goal here is to ensure that the maximum absolute amplitude of the signal reaches a predefined value, typically 1.0. This is done by dividing each sample of the waveform by the maximum absolute value across the entire signal:

$$
x_{\text{norm}}(t) = \frac{x(t)}{\max_t |x(t)|}
$$

This keeps the waveform shape unchanged but scales it so that the largest peak is at the desired level.

**RMS (Root Mean Square) Normalization** 

RMS normalization  adjusts the signal so that its overall energy, measured as root-mean-square (RMS) value, matches a target level. This is especially useful when two signals may have the same peak amplitude but differ in perceived loudness due to different energy distributions. The formula for RMS normalization is:

$$
x_{\text{norm}}(t) = \frac{x(t)}{\text{RMS}(x)} \cdot \text{Target\_RMS}
$$

where $\text{RMS}(x) = \sqrt{\frac{1}{T} \sum_{t=1}^{T} x(t)^2}$, and $T$ is the number of samples in the signal.

**Mean Normalization (DC Offset Removal)** 

A simpler form of normalization is **mean normalization**, also known as DC offset removal. This technique removes any constant bias in the signal by subtracting the mean value:

$$
x_{\text{norm}}(t) = x(t) - \mu
$$

where $\mu$ is the average value of the waveform. Since speech should ideally oscillate around zero, this step ensures the signal is centered.

**Z-Score Normalization (Standardization)** 

A more general form is **z-score normalization** or standardization, which transforms the signal so that it has zero mean and unit variance. This is especially useful in machine learning contexts, where models often assume input features have similar statistical properties. The transformation is defined as:

$$
x_{\text{norm}}(t) = \frac{x(t) - \mu}{\sigma}
$$

where $\mu$ is the mean and $\sigma$ is the standard deviation of the waveform.

### Frequency-Domain Normalizations

**Per-Frame Normalization**

Normalizations can also be applied in the spectral domain, after converting the signal into a time-frequency representation such as a spectrogram. In per-frame normalization, each time frame of the spectrogram is normalized to have zero mean and unit variance across frequency:

$$
S_{\text{norm}}(f, t) = \frac{S(f,t) - \mu_t}{\sigma_t}
$$

Here, $\mu_t$ and $\sigma_t$ are the mean and standard deviation of the spectral values at time $t$, across all frequencies $f$. This kind of normalization helps reduce variations due to environmental noise or loudness that affect the entire frame.

**Per-Frequency Normalization**

Conversely, per-frequency normalization normalizes each frequency bin across time, which is useful when some frequency bands are consistently stronger due to recording conditions or channel characteristics. In this case, the normalization is written as:

$$
S_{\text{norm}}(f, t) = \frac{S(f,t) - \mu_f}{\sigma_f}
$$

where $\mu_f$ and $\sigma_f$ are computed across time for each frequency bin $f$.

### Conclusion

Each of these normalization methods serves a specific purpose and is often combined with others in practical speech processing pipelines. They help ensure that models or algorithms are not biased by irrelevant differences in amplitude or energy that are not part of the speech content itself.
