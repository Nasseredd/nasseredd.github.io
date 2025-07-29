---
title: "How to Create a Multichannel Mixture of Speech and Noise"
permalink: /blog/speech-and-language-processing/creating-a-mixture
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
    <span>Reading Time: ~15 min</span> • 
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
## Introduction

Multichannel speech and noise mixtures are essential in various applications, such as speech enhancement, source separation, and robust automatic speech recognition (ASR). This article offers a thorough explanation and a step-by-step guide for creating a multichannel mixture of speech and noise, considering spatial characteristics, room acoustics, and microphone configurations. In this article, we would like to create a speech and noise mixture for a binaural speech enhancement for hearing aids. 

## Data

In the following, we will work with a speech signal from the test-clean subset of Librispeech, a noise signal from Freesound, and two room impulse responses generated from recordings made in a room at CERIAH (Institut Pasteur), with which I collaborate as part of the REFINED research project.

```python
import numpy as np
import soundfile as sf

speech, sr = sf.read('speech.wav')
noise, sr = sf.read('noise.wav')

speech_rir = np.load('rir_0.npz')
noise_rir = np.load('rir_90.npz') 
```

## Single-Channel Mixture

In the context of speech enhancement, a mixture refers to a signal that combines multiple audio sources, such as a clean speech and a noise signal, often at a specific signal-to-noise ratio (SNR). A multichannel mixture can be represented as: 

$$
x[t] = s[t] + n[t]
$$

where $$x[t]$$ is the simulated mixture, $$s[t]$$ is the clean speech signal, and $$n[t]$$ is the noise signal. This mixture is considered anechoic since it is generated using assumed dry (anechoic) clean speech and noise signals. It is a single-channel mixture because the two signals were summed into a one-dimensional signal, even though they were originally recorded with two different microphones.

```python
x = speech + noise
```


## Single-Channel Mixture with respect to a desired SNR

#### Signal-to-Noise Ratio

The signal-to-noise Ratio (SNR) is a measure that quantifies the relative strength of a desired signal (e.g. clean speech) compared to a background noise. A higher SNR indicates a clearer signal with less noise, while a lower SNR means the noise is more dominant than the signal.

 SNR is typically expressed in decibel (dB) and is defined as: 

$$
\text{SNR}_{\text{dB}} = 10\,\text{log}_{10} \bigg( \frac{P_s}{P_n} \bigg)
$$

where $$P_s$$ is the power of the signal and $$P_n$$ is the power of the noise.

Precisely, 

- if $$\text{SNR}_{\text{dB}} = 0$$, it means the speech and noise energies are on the same level.
- if $$\text{SNR}_{\text{dB}} > 0$$, it means the speech energy is higher than the noise energy.
- if $$\text{SNR}_{\text{dB}} < 0$$, it means the speech energy is lower than the noise energy.

### Scaling noise to achieve the desired SNR

To generate a mixture that satisfies a given $$\text{SNR}_{\text{dB}}$$, we scale either the speech signal or the noise signal accordingly. Indeed, our goal is to determine the appropriate gain factor $$\alpha$$ so that the speech and noise energies achieve the desired $$\text{SNR}_{\text{dB}}$$ level. 

To this end, let’s break down the $$\text{SNR}_{\text{dB}}$$ formula to determine the target scaling factor. Since we choose to scale the noise signal, we define: 

$$
n’[t] = \alpha \cdot n[t]
$$

Thus, the signal-to-noise ratio can be rewritten as:

$$
\text{SNR}_{\text{dB}} = 10\,\text{log}_{10} \bigg( \frac{P_s}{P_{n’}} \bigg)
$$

where $$n’[t]$$ represents the appropriately scaled noise signal needed to achieve the desired SNR level. 

Expanding the power terms: 

$$\text{SNR}_{\text{dB}} = 10\,\text{log}_{10} \bigg( \frac{P_s}{P_{n'}} \bigg) = 10\,\text{log}_{10} \bigg( \frac{    1/N \, \sum  s[t]^2     }{      1/N \, \sum  \alpha n[t]^2      } \bigg) = 10\,\text{log}_{10} \bigg( \frac{    \sum  s[t]^2     }{   \alpha^2 \sum  n[t]^2      } \bigg) = 10\,\text{log}_{10} \bigg( \frac{    P_s     }{   \alpha^2 P_n      } \bigg)$$. 

Solving for $$\alpha$$:

$$\frac{\text{SNR}_{\text{dB}} }{10}= \text{log}_{10} \bigg( \frac{    P_s     }{   \alpha^2 P_n      } \bigg)$$

$$10^{\frac{\text{SNR}_{\text{dB}} }{10}}= \frac{    P_s     }{   \alpha^2 P_n      }$$

$$\alpha^2 = \frac{P_s}{P_n} \cdot 10^{-\frac{\text{SNR}_{\text{dB}} }{10}}$$

$$\alpha = \frac{P_s}{P_n} \cdot 10^{-\frac{\text{SNR}_{\text{dB}} }{20}}$$

$$\alpha = \frac{\sum s^2}{\sum n^2} \cdot 10^{-\frac{\text{SNR}_{\text{dB}} }{20}}$$

### Accounting for RMSE-normalized signals

This formulation of $$\alpha$$ do not account for normalized signals using RMSE. If this normalization is applied, replacing $$s$$ and $$n$$ by their normalized verions:

$$
s_{\text{norm}}\frac{s}{\sqrt{\sum s^2}} \;\;,\;\; n_{\text{norm}} = \frac{n}{\sqrt{\sum n^2}}
$$

the equation simplifies to:

$$\alpha = 

\frac{
\sum \big(\frac{s}{\sqrt{\sum s^2}}\big)^2}
{\sum \big(\frac{n}{\sqrt{\sum n^2}}\big)^2} 

\cdot 10^{-
\frac{\text{SNR}_{\text{dB}} }{20}}

= 

\frac
{\frac{\sum s^2}{\sum s^2}}
{\frac{\sum n^2}{\sum n^2}}

\cdot 10^{-
\frac{\text{SNR}_{\text{dB}} }{20}}

= 10^{-
\frac{\text{SNR}_{\text{dB}} }{20}}$$

⚠️ Ensure that if you normalize your signals using $$\text{RMSE}$$, you apply the second equation. Otherwise, the term $$\frac{\sum s^2}{\sum n^2}$$ which should ideally be equal to 1, may deviate in practice, potentially affecting the accuracy of your scaling factor $$\alpha$$.

### Handling Silent Portions in Speech for Accurate Gain Computation

In practice, speech signals often contain silent portions with very low energy. These segments can reduce the overall energy of the speech signal, leading to an inaccurate computation of the gain factor. To address this issue, one approach is to selectively retain only samples with a magnitude above a certain threshold (e.g., 0.01). Alternatively, a Voice Activity Detector (VAD) can be used to extract speech segments while discarding silence, ensuring a more reliable gain computation.

### Final Mixture Computation

Now that we have determined the gain factor $$\alpha$$, we compute the mixture as:

$$
x[t] = s[t] \;+\; \alpha\, n[t]
$$

Case 1: without RMSE normalization
    
```python
desired_snr = 0 
alpha = (np.sum(np.abs(speech)**2) / np.sum(np.abs(noise)**2)) * 10 ** (- desired_snr / 20)
x = speech + (alpha * noise)
```
    
Case 2: with RMSE normalization

```python
speech /= np.sum(np.abs(speech)**2)
noise /= np.sum(np.abs(noise)**2)

desired_snr = 0
alpha = 10 ** (- desired_snr / 20)
x = speech + (alpha * noise)
```

## Multichannel Mixture

What if we want to simulate a mixture inside an enclosed room ?

In our case, a multichannel mixture refers to the combination of speech and noise signals recorded or simulated across multiple microphones. Each microphone captures a distinct version of the signals due to spatial propagation effects. Unlike single-channel mixtures, multichannel mixtures preserve spatial characteristics such as directionality, phase differences, and inter-channel time delays.

A **Room Impulse Response (RIR)** is the acoustic transfer function that characterizes how a sound propagates from a source to a receiver within an enclosed space, capturing reflections, reverberation, and other spatial effects. **Convolving** a signal with an RIR simulates the signal as if it were played in that room because convolution applies the room’s acoustic properties—such as delays, attenuation, and reverberation—to the original sound, making it sound as if it naturally propagated through the environment.

We computed room impulse responses (RIRs) from a recorded signal in an enclosed room at five different positions: 90° and 45° to the right, 0°, and 90° and 45° to the left. The signals were played using five loudspeakers, while a KEMAR mannequin was used to position a PHL hearing aid simulator equipped with two microphones on the right ear and two on the left ear. Each of the five loudspeakers generated four distinct RIRs, representing the signal propagation to the four microphones.

To simulate the $$i$$-th channel of the multichannel mixture, representing the signal propagation on the $$i$$-th microphone, we compute it as:

$$
x_i[t] = h_{s,i} \;*\; s[t] + h_{n,i} \;*\; n[t]
$$

where,

- $$h_{s,i}$$ is the room impulse response for the speech signal $$s$$ recorded with the $$i$$-th microphone.
- $$h_{n,i}$$ is the room impulse response for the noise signal $$n$$ recorded with the $$i$$-th microphone.
- $$*$$ is the convolution operator.

NB: Here, we assume the noise have been scaled, as explained previously, before computing the convolutions. 

Thus, the complete multichannel mixture can be represented as:

$$
\begin{bmatrix} 
x_1[t] \\ 
x_2[t]  \\ 
x_3[t]  \\
x_4[t]  
\end{bmatrix}

= 
\begin{bmatrix} 
h_{s,1} \;*\; s[t] + h_{n,1} \;*\; n[t] \\ 
h_{s,2} \;*\; s[t] + h_{n,2} \;*\; n[t]  \\ 
h_{s,3} \;*\; s[t] + h_{n,3} \;*\; n[t]  \\
h_{s,4} \;*\; s[t] + h_{n,4} \;*\; n[t]  
\end{bmatrix}
$$

This formulation captures the multichannel mixture, where each recorded signal results from the convolution of speech and noise with their respective RIRs at each microphone position.

For instance, we could choose $$h_s^{0°}$$for the speech signal and $$h_s^{90°}$$for the noise signal to simulate speech coming from the front while the noise originates from 90° to the right.

Clearly, if you play this mixture, you will only hear it in stereo (2 channels). However, if you wear your headphones or earphones correctly, you should perceive the noise as coming from the right, i.e. with a higher intensity in the right ear than in the left.
    
**Reverberated speech**

```python
speech_fl = np.convolve(speech_rir['front_left'], speech, mode='full')
speech_rl = np.convolve(speech_rir['rear_left'], speech, mode='full')
speech_fr = np.convolve(speech_rir['front_right'], speech, mode='full')
speech_rr = np.convolve(speech_rir['rear_right'], speech, mode='full')

speech_cnv = np.vstack([speech_fl, speech_rl, speech_fr, speech_rr])
```

**Reverberated noise**

We assume the noise has been scaled! 

```python
noise_fl = np.convolve(noise_rir['front_left'], speech, mode='full')
noise_rl = np.convolve(noise_rir['rear_left'], speech, mode='full')
noise_fr = np.convolve(noise_rir['front_right'], speech, mode='full')
noise_rr = np.convolve(noise_rir['rear_right'], speech, mode='full')

noise_cnv = np.vstack([noise_fl, noise_rl, noise_fr, noise_rr])
```
    
**Multichannel mixture**

```python
x = speech_cnv + noise_cnv
```
