---
title: "Comparing Librosa, Soundfile and Torchaudio"
permalink: /blog/speech-and-language-processing/comparing-audio-libraries
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
    <span>Reading Time: ~5 min</span> • 
    <span>Last Modified: July 29, 2025</span>
  </p>
  <p style="margin: 2px 0 0 0;">
    <span>Keywords: </span>
    <span>#SpeechProcessing,</span>
    <span>#Python,</span>
    <span>#Librosa,</span>
    <span>#Soundfile,</span>
    <span>#PyTorch.</span>
  </p>
</div>

<!-- Article -->

## Introduction

When working with audio in Python, you’ll often reach for libraries like librosa, soundfile, and torchaudio. While they all provide simple interfaces for loading audio data, they behave quite differently—especially when it comes to sample rates, output shapes, and data types.

Let’s walk through a practical comparison to understand what happens under the hood when you load the same audio file using these three libraries. First, import the necessary libraries:

```python
import librosa
import soundfile as sf
import torchaudio
```

##### Sample rate

Assume the path to your audio file is stored in the variable audio_path. We'll load the audio using each library and inspect the output shapes and sample rates.

```python
speech_librosa, sr = librosa.load(audio_path)
print(speech_librosa.shape, sr)

speech_sf, sr = sf.read(audio_path)
print(speech_sf.shape, sr)

speech_torch, sr = torchaudio.load(audio_path)
print(speech_torch.shape, sr)
```

Example output might look like this:

```shell
(113227,) 22050
(82160,) 16000
torch.Size([1, 82160]) 16000
```

These differences highlight how each library interprets and processes audio. Librosa differs from soundfile and torchaudio by automatically resampling audio to 22,050 Hz unless explicitly told otherwise. In contrast, both soundfile and torchaudio preserve the audio file’s original sampling rate, making them better suited for tasks where maintaining the native resolution is important, such as speech recognition or dataset fidelity.

##### Normalization

All three libraries normalize 16-bit PCM audio to the [-1.0, 1.0] range by default. This normalization ensures consistency in amplitude representation regardless of the original bit depth, which is especially useful when preparing data for further processing or model training. While the scaling behavior is similar, slight variations may appear due to internal precision or data type differences.