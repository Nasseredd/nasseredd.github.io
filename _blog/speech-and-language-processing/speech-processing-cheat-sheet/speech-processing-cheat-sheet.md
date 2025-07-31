---
title: "Speech Processing CheatSheet"
permalink: /blog/speech-and-language-processing/speech-processing-cheat-sheet
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
    <span>Reading Time: ~10 min</span> • 
    <span>Last Modified: July 29, 2025</span>
  </p>
  <p style="margin: 2px 0 0 0;">
    <span>Keywords: </span>
    <span>#SignalProcessing,</span>
    <span>#SpeechProcessing,</span>
    <span>#FFT,</span>
    <span>#STFT.</span>
  </p>
</div>

<!-- Article -->

<style>
  table.no-borders {
    border: none;
    border-collapse: collapse;
    width: 100%;
    /* margin-left: 2em; */
  }
  table.no-borders td {
    border: none;
    padding: 10px 0;
  }
  .expression {
    display: inline-block;
    width: 80px;
    text-align: left;
  }
  .definition {
    display: inline-block;
    width: 270px;
    text-align: left;
  }
  .meaning {
    display: inline-block;
    width: 320px;           /* Set fixed width */
    text-align: left;
    vertical-align: top;
    word-wrap: break-word;  /* Ensures wrapping within width */
    white-space: normal;
    /* background-color: red;  */
  }
  .shape {
    display: inline-block;
    width: 1.5em;
    text-align: center;
    font-weight: bold;
  }
  .header .expression,
  .header .definition,
  .header .meaning {
    font-weight: bold;
  }
  hr {
    border: 0;
    border-top: 1px solid #ccc;
    margin: 10px 0;
  }
</style>

<table class="no-borders">
  <tbody>
    <tr class="header">
        <td><span class="expression">Expression</span></td>
        <td><span class="definition">Definition</span></td>
        <td><span class="meaning">Meaning or Interpretation</span></td>
        <td><span class="shape"></span></td>
    </tr>
    <!--  -->
    <tr><td colspan="3"><div style="border-top: 1px solid #ccc; margin: 4px 0;"></div></td></tr>
    <!-- Waveform -->
    <tr>
      <td><span class="expression">\(x[n]\)</span></td>
      <td><span class="definition">&mdash;</span></td>
      <td><span class="meaning">Discrete signal in waveform</span></td>
      <td><span class="shape">V</span></td>
    </tr>
    <tr>
      <td><span class="expression">\( E(x[n]) \)</span></td>
      <td><span class="definition">\( E(x[n]) = \sum_{n=0}^{N-1} |x[n]|^2 \)</span></td>
      <td><span class="meaning">Energy of the signal in time domain</span></td>
      <td><span class="shape">s</span></td>
    </tr>
    <tr>
      <td><span class="expression">\( P(x[n]) \)</span></td>
      <td><span class="definition">\( P(x[n]) = \frac{E(x[n])}{N} = \frac{1}{N} \sum_{n=0}^{N-1} |x[n]|^2 \)</span></td>
      <td><span class="meaning">Power of the signal in time domain</span></td>
      <td><span class="shape">s</span></td>
    </tr>
    <!--  -->
    <tr><td colspan="3"><div style="border-top: 1px solid #ccc; margin: 4px 0;"></div></td></tr>
    <!-- FFT -->
    <tr>
      <td><span class="expression">\(X[f]\)</span></td>
      <td><span class="definition">\( X[f] = \sum_{n=0}^{N-1} x[n] \cdot e^{-j 2\pi f n / N} \)</span></td>
      <td><span class="meaning">Fast Fourier transform (FFT)</span></td>
      <td><span class="shape">V</span></td>
    </tr>
    <tr>
        <td><span class="expression">\(|X[f]|\)</span></td>
        <td><span class="definition">\( |X[f]| = \sqrt{\text{Re}(X[f])^2 + \text{Im}(X[f])^2} \)</span></td>
        <td><span class="meaning">Magnitude spectrum</span></td>
        <td><span class="shape">V</span></td>
    </tr>
    <tr>
        <td><span class="expression">\(|X[f]|^2\)</span></td>
        <td><span class="definition">\( |X[f]|^2 = \text{Re}(X[f])^2 + \text{Im}(X[f])^2 \)</span></td>
        <td><span class="meaning">Power spectrum</span></td>
        <td><span class="shape">V</span></td>
    </tr>
    <tr>
        <td><span class="expression">\( |X[f]|^{\gamma} \)</span></td>
        <td><span class="definition">\( |X[f]|^{\gamma} = (\text{Re}(X[f])^2 + \text{Im}(X[f])^2)^{\frac{\gamma}{2}} \)</span></td>
        <td><span class="meaning">Power-law spectrum</span></td>
        <td><span class="shape">V</span></td>
    </tr>
    <tr>
      <td><span class="expression">\( E(X[f]) \)</span></td>
      <td><span class="definition">\( E(X[f]) = \sum_{n=0}^{N-1} |X[f]|^2 \)</span></td>
      <td><span class="meaning">Energy of the signal in frequency domain</span></td>
      <td><span class="shape">s</span></td>
    </tr>
    <tr>
      <td><span class="expression">\( P(X[f]) \)</span></td>
      <td><span class="definition">\( P(X[f]) = \frac{E(X[f])}{N} = \frac{1}{N} \sum_{n=0}^{N-1} |X[f]|^2 \)</span></td>
      <td><span class="meaning">Power of the signal in frequency domain</span></td>
      <td><span class="shape">s</span></td>
    </tr>
    <tr>
      <td><span class="expression">\( ||X[f])||_2 \)</span></td>
      <td><span class="definition">\( ||X[f])||_2 = \sqrt{\sum_{n=0}^{N-1} |X[f]|^2} = \sqrt{E(X[f])} \)</span></td>
      <td><span class="meaning">L2-norm (or Euclidean norm) of the FFT or the square root of the energy</span></td>
      <td><span class="shape">s</span></td>
    </tr>
    <tr>
      <td><span class="expression">\( ||X[f])||_2^2 \)</span></td>
      <td><span class="definition">\( ||X[f])||_2^2 = \sum_{n=0}^{N-1} |X[f]|^2 = E(X[f]) \)</span></td>
      <td><span class="meaning">Squared L2-norm (or Euclidean norm) of the FFT or the energy</span></td>
      <td><span class="shape">s</span></td>
    </tr>
    <!--  -->
    <tr><td colspan="3"><div style="border-top: 1px solid #ccc; margin: 4px 0;"></div></td></tr>
    <!-- STFT -->
    <tr>
        <td><span class="expression">\(X[t,f]\)</span></td>
        <td><span class="definition">\( X[t, f] = \sum_{n=0}^{N-1} x[n + tH] \cdot w[n] \cdot e^{-j \frac{2\pi fn}{N}} \)</span></td>
        <td><span class="meaning">Short-time Fourier transform (STFT)</span></td>
        <td><span class="shape">M</span></td>
    </tr>
    <!--  -->
    <tr>
        <td><span class="expression">\(|X[t,f]|\)</span></td>
        <td><span class="definition">\( |X[t,f]| = \sqrt{\text{Re}(X[t,f])^2 + \text{Im}(X[t,f])^2} \)</span></td>
        <td><span class="meaning">Magnitude spectrogram</span></td>
        <td><span class="shape">M</span></td>
    </tr>
    <tr>
        <td><span class="expression">\(|X[t,f]|^2\)</span></td>
        <td><span class="definition">\( |X[t,f]|^2 = \text{Re}(X[t,f])^2 + \text{Im}(X[t,f])^2 \)</span></td>
        <td><span class="meaning">Power spectrogram (commonly called "spectrogram" in DSP)</span></td>
        <td><span class="shape">M</span></td>
    </tr>
    <tr>
        <td><span class="expression">\(|X[t,f]|^{\gamma}\)</span></td>
        <td><span class="definition">\( |X[t,f]|^{\gamma} = (\text{Re}(X[t,f])^2 + \text{Im}(X[t,f])^2)^{\frac{\gamma}{2}} \)</span></td>
        <td><span class="meaning">Power-law spectrogram</span></td>
        <td><span class="shape">M</span></td>
    </tr>
  </tbody>
</table>
<hr>

**s** = scale, **V** = vector, **M** = Matrix 

<details>
  <summary><strong>Mathematical Functions</strong></summary>
  <div style="margin-top: 0.5em; padding-left: 1em;">
    <table style="border: none; border-collapse: collapse;">
      <tbody>
        <tr>
          <td style="border: none; padding-right: 1em; width: 80px; white-space: nowrap;">\(|\cdot|\)</td>
          <td style="border: none;">Absolute value, modulus or magnitude (\( \forall z \in \mathbb{C}; \; |z| = \sqrt{\text{Re}(z)^2 + \text{Im}(z)^2})\)</td>
        </tr>
        <tr>
          <td style="border: none; padding-right: 1em; width: 80px; white-space: nowrap;">\(|| \cdot ||_2\)</td>
          <td style="border: none;">Euclidean norm or \(\mathcal{L}_{2}\)-norm ( \(A \in \mathbb{R}^{m \times n}  \text{or}  \mathbb{C}^{m \times n};\;\ ||A||_F = \sqrt{\sum_{i=1}^m \sum_{j=1}^n |a_{ij}|^2} \))</td>
        </tr>
        <tr>
          <td style="border: none; padding-right: 1em; width: 80px; white-space: nowrap;">\(|| \cdot ||_F\)</td>
          <td style="border: none;">Frobenius norm</td>
        </tr>
      </tbody>
    </table>
  </div>
</details>
