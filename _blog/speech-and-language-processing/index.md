---
title: "Speech and Language Processing"
permalink: /blog/speech-and-language-processing
author_profile: true
---

## Fundamentals of Speech Processing

<!-- 
- Sound
- 
- Fast Fourier Transform (FFT)
- Short Time Fourier Transform (STFT)
- Scale : Mel scale, Critical bands, 1/3 octave
- 
 -->

<div style="width: 100%; background-color: #fafafa; border-radius: 8px; padding: 10px; margin-top: 15px; display: flex; flex-direction: column; align-items: flex-start;">
  <a href="{{ site.baseurl }}/blog/speech-and-language-processing/speech-processing-cheat-sheet" 
     style="text-decoration: none; color: inherit; display: flex; flex-direction: column; width: 100%;">
    <div style="display: flex; align-items: center;">
      <img src="{{ site.baseurl }}/files/blog/speech-and-language-processing-.jpg" alt="Article Icon" style="width: 24px; height: 24px; margin-right: 10px; border-radius: 50%; background-color: #fff; padding: 4px;">
      <span style="font-size: 18px; font-weight: bold; color: #333;">Speech Processing CheatSheet</span>
    </div>
    <div style="font-size: 14px; color: #888; margin-top: 5px; margin-left: 34px;">Reading time: 10 min</div>
  </a>
</div>

<div style="width: 100%; background-color: #fafafa; border-radius: 8px; padding: 10px; margin-top: 15px; display: flex; flex-direction: column; align-items: flex-start;">
  <a href="{{ site.baseurl }}/blog/speech-and-language-processing/comparing-audio-libraries" 
     style="text-decoration: none; color: inherit; display: flex; flex-direction: column; width: 100%;">
    <div style="display: flex; align-items: center;">
      <img src="{{ site.baseurl }}/files/blog/speech-and-language-processing-.jpg" alt="Article Icon" style="width: 24px; height: 24px; margin-right: 10px; border-radius: 50%; background-color: #fff; padding: 4px;">
      <span style="font-size: 18px; font-weight: bold; color: #333;">Comparing Librosa, Soundfile and Torchaudio</span>
    </div>
    <div style="font-size: 14px; color: #888; margin-top: 5px; margin-left: 34px;">Reading time: 5 min</div>
  </a>
</div>

<div style="width: 100%; background-color: #fafafa; border-radius: 8px; padding: 10px; margin-top: 15px; display: flex; flex-direction: column; align-items: flex-start;">
  <a href="{{ site.baseurl }}/blog/speech-and-language-processing/normalizations" 
     style="text-decoration: none; color: inherit; display: flex; flex-direction: column; width: 100%;">
    <div style="display: flex; align-items: center;">
      <img src="{{ site.baseurl }}/files/blog/speech-and-language-processing-.jpg" alt="Article Icon" style="width: 24px; height: 24px; margin-right: 10px; border-radius: 50%; background-color: #fff; padding: 4px;">
      <span style="font-size: 18px; font-weight: bold; color: #333;">Normalizing Signals</span>
    </div>
    <div style="font-size: 14px; color: #888; margin-top: 5px; margin-left: 34px;">Reading time: 15 min</div>
  </a>
</div>

<div style="width: 100%; background-color: #fafafa; border-radius: 8px; padding: 10px; margin-top: 15px; display: flex; flex-direction: column; align-items: flex-start;">
  <a href="{{ site.baseurl }}/blog/speech-and-language-processing/fft" 
     style="text-decoration: none; color: inherit; display: flex; flex-direction: column; width: 100%;">
    <div style="display: flex; align-items: center;">
      <img src="{{ site.baseurl }}/files/blog/speech-and-language-processing-.jpg" alt="Article Icon" style="width: 24px; height: 24px; margin-right: 10px; border-radius: 50%; background-color: #fff; padding: 4px;">
      <span style="font-size: 18px; font-weight: bold; color: #333;">From a Real-Valued Signal to the FFT and Its Spectrum</span>
    </div>
    <div style="font-size: 14px; color: #888; margin-top: 5px; margin-left: 34px;">Reading time: 15 min</div>
  </a>
</div>

<div style="width: 100%; background-color: #fafafa; border-radius: 8px; padding: 10px; margin-top: 15px; display: flex; flex-direction: column; align-items: flex-start;">
  <a href="{{ site.baseurl }}/blog/speech-and-language-processing/erb" 
     style="text-decoration: none; color: inherit; display: flex; flex-direction: column; width: 100%;">
    <div style="display: flex; align-items: center;">
      <img src="{{ site.baseurl }}/files/blog/speech-and-language-processing-.jpg" alt="Article Icon" style="width: 24px; height: 24px; margin-right: 10px; border-radius: 50%; background-color: #fff; padding: 4px;">
      <span style="font-size: 18px; font-weight: bold; color: #333;">Equivalent Rectangular Bandwidth (ERB)</span>
    </div>
    <div style="font-size: 14px; color: #888; margin-top: 5px; margin-left: 34px;">Reading time: 15 min</div>
  </a>
</div>

<!-- <div style="width: 100%; background-color: #fafafa; border-radius: 8px; padding: 10px; margin-top: 15px; display: flex; flex-direction: column; align-items: flex-start;">
  <a href="{{ site.baseurl }}/blog/speech-and-language-processing/phoneme-analysis" 
     style="text-decoration: none; color: inherit; display: flex; flex-direction: column; width: 100%;">
    <div style="display: flex; align-items: center;">
      <img src="{{ site.baseurl }}/files/blog/speech-and-language-processing-.jpg" alt="Article Icon" style="width: 24px; height: 24px; margin-right: 10px; border-radius: 50%; background-color: #fff; padding: 4px;">
      <span style="font-size: 18px; font-weight: bold; color: #333;">Phoneme Analysis</span>
    </div>
    <div style="font-size: 14px; color: #888; margin-top: 5px; margin-left: 34px;">Reading time: 7 min</div>
  </a>
</div> -->

## Speech Enhancement

<div style="width: 100%; background-color: #fafafa; border-radius: 8px; padding: 10px; margin-top: 15px; display: flex; flex-direction: column; align-items: flex-start;">
  <a href="{{ site.baseurl }}/blog/speech-and-language-processing/creating-a-mixture" 
     style="text-decoration: none; color: inherit; display: flex; flex-direction: column; width: 100%;">
    <div style="display: flex; align-items: center;">
      <img src="{{ site.baseurl }}/files/blog/speech-and-language-processing-.jpg" alt="Article Icon" style="width: 24px; height: 24px; margin-right: 10px; border-radius: 50%; background-color: #fff; padding: 4px;">
      <span style="font-size: 18px; font-weight: bold; color: #333;">How to Create a Multichannel Mixture of Speech and Noise?</span>
    </div>
    <div style="font-size: 14px; color: #888; margin-top: 5px; margin-left: 34px;">Reading time: 10 min</div>
  </a>
</div>
