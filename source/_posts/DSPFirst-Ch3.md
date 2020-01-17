---
title: DSP First - Chapter 3 - Spectrum Representation
date: 2018-12-19 21:48:39
tags: DSP First
categories: DSP
mathjax: true
toc: true
---

Spectrum, a graphic representation of the frequency components of a signal, is 

> a compact representation of the frequency contents of a signal that can be represented as a sum of sinusoid.

<!--more-->

> The term spectrum is used in many ways—often without precise definition. Our use of the term is clearly defined in terms of sums of sinusoids or complex exponentials.

- In this chapter, instead using Fourier transform, the spectrum is introduced from complex exponentials, illustrated as a clockwise and a counterclockwise rotating phasor.

### The Spectrum of a sum of sinusoids
- Additive linear combination of sinusoids for new signals $x(t)$:
  - represented as real signals: $x(t) = A_0 + \sum\limits_{k=1}^N A_k\cos(2\pi f_k t + \phi_k)$.
  - represented as complex exponentials: $x(t) = X_0 + \sum\limits_{k=1}^N \Re{\{X_k e^{j2\pi f_kt}\}}$, where $X_0=A_0$
- Two-sided spectrum
  - the inverse Euler formula leads the above equation to
    $$\begin{equation}
	x(t)= X_0+ \sum\limits_{k=1}^N\{\dfrac{X_k}{2}e^{j2\pi f_kt}+\dfrac{X_k^*}{2}e^{-j2\pi f_kt}\},
	\label{two-sided}
	\end{equation}$$
	as the real part of a complex number is equal to one-half the sum of that number and its complex conjugate.
  - Eq. $\eqref{two-sided}$ means the sinusoids are decomposed into **two rotating phasors** with frequency $f_k$ and $-f_k$, i.e., $2N+1$ frequency components ("1" corresponds to the $X_0$ which is the zero frequency DC component).
- Frequency-domain representation (spectrum) vs. time-domain representation (waveform).
- The spectrum is represented by the set of $(f_k, a_k)$ pairs, and the signal can be written as a single compact summation
  $$\begin{equation}
	x(t)= \sum\limits_{k=-N}^N a_k e^{j2\pi f_k t},
	\label{signal_summation}
  \end{equation}$$

### Sinusoidal amplitude modulation
The beat note and the amplitude modulation (AM)

#### Multiplication and sum of sinusoids
- Multiplication of sinusoids could be rewritten as a sum of sinusoids.
- Beat notes, an addition of two sinusoids:
  $$x(t) = \cos(2\pi f_1t)+\cos(2\pi f_2t) = 2\cos(2\pi f_{\Delta}t)\cos(2\pi f_c t),$$ 
  with the *center frequency* $f_c=\frac{1}{2}(f_1+f_2)$ and the *deviation frequency* $f_{\Delta}=\frac{1}{2}(f_2-f_1)$
- Envelope and amplitude modulation.

#### Amplitude modulation (AM)
- Amplitude modulation is the process of multiplying a high-frequency sinusoidal signals by a low-frequency signal.
  $$x(t) = v(t)\cos(2\pi f_ct ),$$
  where the $\cos(2\pi f_ct)$ is the carrier signal with the carrier frequency $f_c$ and the $v(t)$ is the modulating signal.
- The primary difference between the AM signal and the beat note signal is that the AM envelope ($v(t)$) is usually set up to have no zero crossings. However, the beat note signal, due to the property of adding sinusoids, the modulation signal is always a $\cos$ function so that brings in zero-crossings.

#### AM spectrum
- As the modulating signal $v(t)= V_0 + V\cos(2\pi f_m t)$, so the resulting spectrum consists of scaled copies of $f=\pm f_c$ because of $V_0$ and two similar subsets $+f_c \pm f_m$ and $-f_c \pm f_m$. Each subsets is a frequency-shifted and scaled version of the two-sided spectrum of $v(t)$.

#### The concept of bandwidth
- For the previous case, the bandwidth equals $BW = (f_c+f_m)-(f_c-f_m)=2f_m$.

> The bandwidth characterization is important in the AM radio broadcast system because each AM radio station is assigned a specific carrier frequency $f_c$ and a bandwidth of 10 kHz centered at the carrier frequency. In this way, many local stations can share the (wide) bandwidth of free space without interfering with each other. This sharing of the free-space communication channel is called *frequency-division multiplexing* (频分复用).

### Operations on the spectrum
> The correspondence between a time-domain operation and spectrum changes is often referred to as a property of the spectrum representation.

- *Scaling*: leave all frequencies unchanged with scaled amplitude.
- *Adding a constant*: change the complex amplitude at only frequency at 0.
- *Adding signals*: summation of $(f_k, a_k)$ pair.
- *Time-shifting*
  - time-domain: $y(t)=x(t-\tau_d)$, where $\tau_d$ is the delay length.
  - freq-domain: $b_k = a_k e^{-j2\pi f_k \tau_d}$, where $b_k$ is the resulting amplitude.
- *Differentiating* 
  - time-domain: $y(t)=\frac{d}{dt}x(t)$
  - freq-domain: $b_k=(j2\pi f_k)a_k$.
- *Frequency shifting* 
  - time-domain: $y(t)=x(t)e^{j(2\pi f_st+\phi)}$
  - freq-domain: $(f_k, a_k) \rightarrow (f_k+f_s, a_k Ae^{j\phi})$.


### Periodic waveforms
- Periodic Signal $x(t)=x(t+T_0)$, where $T_0$ is the period and $F_0 = 1/T_0$ is the fundamental frequency.
- A Sum of *harmonically related* sinusoids can be used to synthesize a periodic signal.
  $$\begin{equation}
    x(t) = A_0 + \sum\limits_{k=1}^N A_k\cos(2\pi k F_0 t+\phi_k),
  \end{equation}\label{additive synthesis}$$
  where the frequency, $f_k=kF_0$ is the harmonic frequencies and  called the $k^{th}$ harmonic of the $F_0$
- The waveform would be nonperiodic if the frequencies have no harmonic relation to one another.

### Fourier series
- Fourier Synthesis Summation or **Fourier series**
  $$\begin{equation}
    x(t)=\sum\limits_{-\infty}^{\infty} a_k e^{j2\pi f_kt},
  \end{equation}\label{FSS}$$
  where $f_k=k/T_0=kf_0$ and $F_0=1/T_0$.
- Mathematical theory of *Fourier series*: a general theory that shows how to find the coefficients $a_k$ so that any periodic signal can be synthesized with a sum of harmonically related sinusoids, even when the sum may need an infinite umber of terms.
- Two aspects of the Fourier series: 
  - *Fourier analysis*: from $x(t)$ to calculate ${a_k}$.
  - *Fourier synthesis*: from ${a_k}$ to generate $x(t)$.

#### Fourier series: analysis
- Fourier analysis integral
  $$\begin{equation}
     a_k=\dfrac{1}{T_0}\int\limits_0^{T_0}x(t)e^{-j2\pi f_k t} dt,
  \end{equation}\label{FAI}$$
- DC Component
  $$\begin{equation}
     a_0=\dfrac{1}{T_0}\int\limits_0^{T_0}x(t) dt,
  \end{equation}\label{DC}$$
  
- Only one period of $x(t)$ is required.
- Two representations
  - $x(t)$, time-domain representation.
  - $a_k$, frequency-domain representation or the spectrum representation.

#### Examples
- The square wave (1st edition)
- the triangle wave (1st edition), which is the integral of the square wave
- Full-wave rectified sine wave (FWRS), $x(t)=|\sin(2\pi t/T_1)|$, where the fundamental period $T_0 = \frac{1}{2}T_1$.

### Time-frequency spectrum (Spectrogram)

### Frequency modulation: chirp signals
- $x(t)=\Re{Ae^{j\psi(t)}}=A\cos(\psi(t))$, where $\psi(t)$ is the angle function.
- **Instantaneous frequency** $\omega_i(t) = \dfrac{d}{dt}\psi(t) \; \text{rad/s}$ and $f_i(t) = \dfrac{1}{2\pi}\dfrac{d}{dt}\psi(t) \; \text{Hz}$
- Quadratic angle function
  - $\psi(t)=2\pi\mu t^2 + 2\pi f_0 t + \phi$.
  - $f_i(t)=2\mu t + f_0$ $\rightarrow$ *linear Frequency modulation* or *chirp*
