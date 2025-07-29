---
title: "From a Real-Valued Signal to the FFT and Its Spectrum"
permalink: /blog/speech-and-language-processing/fft
author_profile: true
---

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

## Introduction

Ever wondered how we turn a real-world signal, like audio, into its frequency components? In this post, we’ll dive into the Fast Fourier Transform (FFT), a powerful tool that converts a real-valued signal $$ x[n] $$ into its complex-valued frequency domain $$ X[f] $$. We’ll explore the math behind it, compute the FFT using Python libraries like NumPy and PyTorch, and visualize the spectrum to reveal the signal’s frequency content.

But before we dive in, let’s grab the essential tools. 

<details>
<summary><strong>Imports</strong></summary>

We'll rely on the following imports for all the practical demonstrations in this article.

  <pre><code>import torch
import scipy
import numpy as np
import soundfile as sf
import matplotlib.pyplot as plt</code></pre>
</details>

## From a Real-Valued Signal to the FFT and Its Spectrum

Let’s start with the definition. For a real-valued discrete-time signal $$x[n]$$ of length $$N$$, its Discrete Fourier Transform (DFT), often computed using the Fast Fourier Transform (FFT), is given by:

$$
\forall f \in \{0, N-1\}, \quad X[f] = \sum_{n=0}^{N-1} x[n] \cdot e^{-j 2\pi f n / N}
$$

where 
* $$ x[n] $$ is the input signal in the time domain (real-valued),
* $$ X[f] $$ is the complex-valued output in the frequency domain,
* $$ j $$ is the imaginary unit, where$$ j^2 = -1 $$, 
* $$ N $$ is both the number of time-domain samples and the number of frequency bins.


<style>
.highlighted-example {
  background-color: #f6fff6; /* very light green */
  padding: 1rem;
  border-radius: 8px;
  margin: 1rem 0;
}
</style>

<div class="highlighted-example">
<p>Let’s walk through an example. Suppose a simple real-valued signal \( x[n] = [1, 0, 1] \). We’ll compute the FFT — that is, the values of \(X[f]\) for each frequency index \( f \):</p>

<ul>
  <li>
    for \(f = 0\):

    $$
    \begin{align}
    X[0] &= x[0] \cdot e^{-j 2\pi \cdot 0 \cdot 0 / 3} + x[1] \cdot e^{-j 2\pi \cdot 0 \cdot 1 / 3} + x[2] \cdot e^{-j 2\pi \cdot 0 \cdot 2 / 3} \\
         &= 1\cdot1 + 0\cdot1 + 1\cdot1 \\
         &= 2
    \end{align}
    $$
  </li>

  <li>
    for \(f = 1\):

    $$
    \begin{align}
    X[1] &= x[0] \cdot e^{-j 2\pi \cdot 1 \cdot 0 / 3} + x[1] \cdot e^{-j 2\pi \cdot 1 \cdot 1 / 3} + x[2] \cdot e^{-j 2\pi \cdot 1 \cdot 2 / 3} \\
         &= 1\cdot1 + 0\cdot(-\frac{1}{2} - j \frac{\sqrt{3}}{2}) + 1\cdot(-\frac{1}{2} + j \frac{\sqrt{3}}{2}) \\
         &= \frac{1}{2} + j \frac{\sqrt{3}}{2}
    \end{align}
    $$
  </li>

  <li>
    for \(f = 2\):

    $$
    \begin{align}
    X[2] &= x[0] \cdot e^{-j 2\pi \cdot 2 \cdot 0 / 3} + x[1] \cdot e^{-j 2\pi \cdot 2 \cdot 1 / 3} + x[2] \cdot e^{-j 2\pi \cdot 2 \cdot 2 / 3} \\
         &= 1\cdot1 + 0\cdot(-\frac{1}{2} + j \frac{\sqrt{3}}{2}) + 1\cdot(-\frac{1}{2} - j \frac{\sqrt{3}}{2}) \\
         &= \frac{1}{2} - j \frac{\sqrt{3}}{2}
    \end{align}
    $$
  </li>
</ul>

<p>And that’s it! We’ve just computed the full FFT of a simple real-valued signal as \( X = [2, \frac{1}{2} + j \frac{\sqrt{3}}{2}, \frac{1}{2} + j \frac{\sqrt{3}}{2}]\).</p>

<details>
  <summary><strong>Recall</strong></summary>
  <ul>
    <li>\( e^{-j 2\pi / 3} = \cos(-2\pi / 3) + j\cdot \sin(-2\pi / 3) = -\frac{1}{2} - j \frac{\sqrt{3}}{2} \)</li>
    <li>\( e^{-j 4\pi / 3} = \cos(-4\pi / 3) + j\cdot \sin(-4\pi / 3) = -\frac{1}{2} + j \frac{\sqrt{3}}{2} \)</li>
    <li>\( e^{-j 8\pi / 3} = e^{-j 2\pi / 3} = -\frac{1}{2} - j \frac{\sqrt{3}}{2}\)</li>
  </ul>
</details>

</div>

---

## Computing FFT in Python

Let’s begin by loading our first audio signal. Start by downloading a file from <a href="/files/blog/1221-135767-0010.wav" download>this link</a>, corresponding to a male speech signal from [Librispeech corpus](https://www.openslr.org/12). 

```python
import soundfile as sf
signal, sr = sf.read('1221-135767-0010.wav')
print(signal.shape)
print(sr)
```

This signal has `131,200` samples and a sample rate of `16,000 Hz`.

Now, we compute the fast Fourier transform (FFT) using either `numpy`, `scipy` or `torch`:

```python
# Compute FFT using numpy
fft = np.fft.fft(signal)

# Compute FFT using scipy
fft = scipy.fft.fft(signal)

# Compute FFT using torch
signal_pt = torch.from_numpy(signal).float() # convert numpy to torch 
fft = torch.fft.fft(signal_pt)

print(fft.size)
>> 131200
``` 

Each method gives us an output of the same length (131200), corresponding to one frequency bin per time-domain sample. However, Minor numerical differences may arise : NumPy and SciPy's output (e.g., `-1756.95983887`) shows higher decimal precision compared to PyTorch's `-1756.9597`, reflecting slight differences in floating-point arithmetic or rounding conventions, likely due to PyTorch's optimizations for GPU acceleration or performance efficiency. 

---

## Visualizing the FFT: Why Does It Look Mirrored?


```python
plt.plot(fft)
plt.xlabel('Frequency (Hz)')
plt.ylabel('Amplitude')
plt.title('PyTorch FFT')
plt.show()
```

<div style="text-align: center;">
  <img src="/files/blog/FFT.png" alt="FFT" style="max-width: 100%; height: auto; margin-top: 1rem;" />
</div>

> Why does the FFT output look mirrored — and can we simplify it by keeping only the useful part?

First of all, if you try to plot the full complex-valued FFT directly, you’ll encounter a `ComplexWarning` indicating that only the real part is being displayed while the imaginary part is discarded. 

Furthermore, while this plot gives a complete view (of the real part) of the FFT output, it includes both positive and negative frequencies — leading to symmetric redundancy that's often unnecessary for real-valued signals. 

To this end, we retain only the first half of the frequency bins (from $$0$$ to $$\frac{N}{2}$$) which correspond to the positive frequencies, and discard the second half (from $$\frac{N}{2}+1$$ to $$N-1$$) which represent the negative ones.

---
> Positive? Negative? I don’t quite see how the values on the left (or the first half) are “positive” and those on the right (the second half) are “negative”!

Well, I do agree that it’s not straightforward. Let’s break it down.

In fact, each frequency bin $$f$$ in the FFT corresponds to a complex sinusoid with angular frequency $$\omega_f = \frac{2\pi f}{N}$$. 


<div class="highlighted-example">
  <p>Let’s take an example: suppose \( N = 8 \). Then:</p>

  <ul>
    <li>Bin \( f = 1 \in \{ 0, \frac{N}{2} \} \) corresponds to \( \omega = \frac{2\pi}{8} = \frac{\pi}{4} \).</li>
    <li>Bin \( f = 7 \in \{ \frac{N}{2}, N-1 \} \) corresponds to \( \omega = \frac{2\pi \cdot 7}{8} = \frac{14\pi}{8} = \frac{7\pi}{4} \).</li>
  </ul>

  <p>Now, here's the trick: \( \frac{7\pi}{4} \) is equivalent to \( -\frac{\pi}{4} \) (modulo \( 2\pi \)). So bin \( 7 \) represents the negative frequency counterpart of bin \( 1 \).</p>
</div>

If you remember our very first example, you might’ve noticed something interesting — a kind of symmetry in the FFT output. 

<div class="highlighted-example">
  <p>We looked at a simple signal: \( x[n] = [1, 0, 1] \), and its FFT came out as \( X = [2,\; \frac{1}{2} + j \frac{\sqrt{3}}{2},\; \frac{1}{2} - j \frac{\sqrt{3}}{2}] \). See that? \( X[1] \) and \( X[2] \) are complex conjugates of each other — same real part, opposite imaginary parts. This observation isn’t just a happy accident.</p>
</div>

In fact, it’s a general property known as <strong>Hermitian symmetry</strong>: for any real-valued time-domain signal, its FFT satisfies 

$$X[N-f] = \overline{X[f]}$$

<div class="highlighted-example">
  <p>That is, each frequency bin on the “right half” of the FFT is the complex conjugate of a bin on the “left half.” So for our example with \(N = 3\), \(X[2] = \overline{X[1]}\). This symmetry is exactly why we can afford to keep only the positive frequency side when working with real signals — the rest is just mirrored information.</p>


<details>
<summary><strong>Recall</strong></summary>
The conjugate of a complex number \( a + jb \) is \( a - jb \), where \( a \) is the real part, \( b \) is the imaginary part, and \( j = \sqrt{-1} \).  

</details>
</div>

---

## Visualizing the Positive-Frequency FFT 

To begin with, let’s plot the FFT while keeping only the positive frequencies (i.e., the left half) and discarding the negative ones on the right:

```python
plt.plot(fft[:int(len(fft)/2)])
plt.xlabel('Frequency (Hz)')
plt.ylabel('Amplitude')
plt.title('Positive-Frequency FFT')
plt.show()
```

<div style="text-align: center;">
  <img src="/files/blog/pf_FFT.png" alt="FFT" style="max-width: 100%; height: auto; margin-top: 1rem;" />
</div>


**To sum up**: when you plot the FFT directly (e.g., using `plt.plot(fft)`), Python raises a `ComplexWarning` because it only displays the real part — silently discarding the imaginary part. As a result, you lose half the information, and the plot may not accurately reflect the true frequency content (we’ll address this properly in the next section). Moreover, since the FFT of a real-valued signal includes both positive and negative frequencies — which are symmetric — we usually keep and display only the first half.

---

## Computing and Vizualizing the Spectrum 

Because complex numbers are hard to interpret visually, a common solution is to compute the magnitude, which combines information from both the real and imaginary parts. The magnitude of the FFT — known as the **spectrum** — is defined as:

$$
|X[f]| = \sqrt{\text{Re}(X[f])^2 + \text{Im}(X[f])^2}
$$

This gives a complete measure of the amplitude at each frequency component. That’s why plotting $$ \lvert X[f] \lvert $$ is both more informative and widely used in practice.

Let's plot everything. Let's compute first the spectrum from the fft. 

```python
fft = scipy.fft.fft(signal)
spectrum = np.abs(fft)
```

Now let's plot the spectrum directly and vizualize it. 

```python
plt.plot(spectrum)
plt.xlabel('Frequency (Hz)')
plt.ylabel('Amplitude')
plt.title('PyTorch FFT')
plt.show()
```

<div style="text-align: center;">
  <img src="/files/blog/spectrum.png" alt="spectrum" style="max-width: 100%; height: auto; margin-top: 1rem;" />
</div>

As explained previously, you notice a mirror effect corresponding to keeping both positive and negative values. Thus, we discard the negative values and keep only the positive values and we get it as follows: 

```python
plt.plot(spectrum[:int(len(fft)/2)])
plt.xlabel('Frequency (Hz)')
plt.ylabel('Amplitude')
plt.title('Positive-Frequency Spectrum')
plt.show()
```

<div style="text-align: center;">
  <img src="/files/blog/pf_spectrum.png" alt="spectrum" style="max-width: 100%; height: auto; margin-top: 1rem;" />
</div>

## Conclusion

And that’s the magic of the FFT! We’ve journeyed from a real-valued signal to its frequency domain, using the FFT to uncover hidden frequency components. By computing the spectrum $$ \lvert X[f] \rvert$$, we get a clear, visual snapshot of a signal’s amplitude across frequencies. With Python tools like NumPy and PyTorch, and by focusing on positive frequencies, we’ve made sense of complex outputs in a practical way. This process is key in signal processing, helping us analyze everything from audio to vibrations with ease and precision. Keep exploring, and happy signal crunching!




