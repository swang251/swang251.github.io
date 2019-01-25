---
title: Digital Audio Signal Processing-Lecture 3 (Notes)
mathjax: true
toc: true
date: 2019-01-22 17:15:58
tags: Lecture Notes (DASP)
categories: DSP
---
Notes of Digital Audio Signal Processing, Lecture 3.
<!--more-->

- From now on, the hat, $\hat{}$, represents the normalized version.

###  Notable Notes
- von Coler et al. 2018, Parametric Synthesis of Glissando Note Transitions - A User Study in a Real-Time Application, DAFx-18.
- signal: a mathematical function that carries information, could be pressure, control parameters and so on.
- Lagrange polynomial used in spatial sampling, non-integer delay as an interpolating filter.
- A delay system is a system.
- ADSR is a synthesizer.
- $s[n] = \sum\limits_{k\in \mathbb{Z}}s[k]\delta[n-k]$
- **Dirac delta function**
  - There are many ways to define Dirac delta function, see [Wolfram MathWorld](http://mathworld.wolfram.com/DeltaFunction.html)
  - See more [here](http://tutorial.math.lamar.edu/Classes/DE/DiracDeltaFunction.aspx)
  - integral, kind of dot product.
- **Block by Block (buffer)** in applications equals **vectorization**
- **Sampling** makes the spectrum periodic
  - For two frequency, $\hat{f_0}$ and $\hat{f_0}+r$
    - Discrete-time domain: $\cos(2\pi\hat{f_0}n) = \cos(2\pi(\hat{f_0}+r)n)$, because $2\pi r n$ is an integer multiple of $2\pi$, so it is periodic inthe frequency domain.
    - Continuous-time domain: $\cos(2\pi f_0 t) \neq \cos(2\pi (f_0+rf_0)t)$
  - From $x(t)=x(t+T_0)$ to $x[n] = x[n+N_0]$, it only works when $\hat{f_0}N_0 = k $ and $k=0,1,\dots, N_0$
- impulse (time-domain) $\rightarrow$ 1 (frequency-domain) $\rightarrow$ alias filter (works as a bandlimited filter) $\rightarrow$ rectangular (frequency-domain) $\rightarrow$ ADC $\rightarrow$ sinc function (time-domain)
- The basis of Fourier transform is simply rotating vectors in the 2D plane ($e^{2\pi j\hat{f_0}n}$)

### Discrete-time sequences
#### Impulse
  $$\begin{equation}
  \delta[n] = 
    \begin{cases}
	  1, \quad n=0,\\
	  0, \quad n\neq0
	\end{cases}
  \end{equation}$$
  
- Delayed impulse: $\delta_{n_0}[n]=\delta[n-n_0]$
- Impulse response

#### Unit step sequence
  $$\begin{equation}
  u[n] = 
    \begin{cases}
	  1, \quad n\leq0,\\
	  0, \quad n<0
	\end{cases}
  \end{equation}$$

- $u[n]=u[n-1]+\delta[n]=\sum\limits_{k=0}^\infty\delta[n-k]$
- works as a switch (control)
- used to check the stability

#### Rectangular sequence
$$\begin{equation}
r[n]=u[n]-u[n-N],\end{equation}$$
where $N$ is the length of the rectangular

- $r[n] = \delta[n]$ when $N=1$ $\rightarrow$ $$\delta[n]=u[n]-u[n-1],$$ which is also explained as a finite-difference scheme, representing the slope the signal is we divide both sides by the sampling time $ T_s$
- used to design waveforms like a square wave (a linear combination of rectangular sequence)

#### Damped Exponentials
  $$\begin{equation}
  x[n] = 
    \begin{cases}
	  Aa^n, \quad n\leq0,\\
	  0, \quad n<0
	\end{cases}
  \end{equation}$$
  
- $0<a<1$, damped signal, $-1<a<0$, damped osillating signal.
- [**RC circuit**](https://en.wikipedia.org/wiki/RC_circuit) and [RC filter](https://en.wikipedia.org/wiki/Low-pass_filter#RC_filter), working as a low pass filter, check [here](https://www.electronics-tutorials.ws/filter/filter_2.html).
- The frequency response of $a^nu[n]$ is $\dfrac{1}{1-ae^{-j\hat{\omega}}}$, where $\hat{\omega}$ is the normalized radian frequency.
- recursive

#### Sinusoids sequence
$$\begin{equation}x[n] = A_0\cos(2\pi \hat{f_0}n+\phi_0),\end{equation}$$
where $\hat{f_0}$ is the normalized frequency and $\phi_0$ is the initial phase.

- recursive computaion of $sin$ functions

#### Complex exponential sequence
$$P_{f_0}[n]=e^{2\pi j \hat{f_0}n}$$
and
$$z[n] = A_0e^{j\phi_0}e^{j2\pi\hat{f_0}n}=z[n-1]e^{2\pi j \hat{f_0}},$$
where the phasor $\hat{A}=Ae^{j\phi_0}$ is the complex amplitude.

#### Damped sinusoids
$$x[n] = A_0e^{-\alpha n}\cos(2\pi\hat{f_0}n+\phi_0)$$
and 
$$z[n] = \hat{A_0}e^{-\alpha+2\pi j\hat{f_0}n},$$
where $e^{-\alpha}$ represents the damping.

### The link between phase shift and time delay
Comparing:
$$x(t) \rightarrow x(t-d)$$
and
$$sin(2\pi f_0t+\phi_0) \rightarrow sin(2\pi f_0 (t-d)+\phi_0),$$
where the phase shift $-2\pi f_0 d$ is frequency dependent.

### Others
#### spatial wave
$$p(t,r) = A_0\cos(2\pi f_0(t-\frac{r}{c}))$$
- the link between the spatial domain and the phase domain
- wavenumber is the spatial frequency of the wave $k = \dfrac{2\pi f_0}{c}=\dfrac{2\pi}{\lambda}$ (radians or circle per unit distance), BTW, **wavenumber is not dimensionless** but Helmholtz number $ka$ is.
- Compared to frequency $\omega = \dfrac{2\pi}{T}$, where $T$ and $\lambda$ are the length of the period in time and space, respectively.

#### Phasor
- phasor $\leftrightarrow$ vector
#### Linear chirp
$$phi[n] = \phi_0 + 2\pi(\hat{f_0}+\frac{\beta(n+1)}{2})n$$
instead of simply $\phi[n] = \phi_0+2\pi f[n]n$, where $f[n] = \hat{f_0}+\beta n$

- this is to maintain the phase continuity.
