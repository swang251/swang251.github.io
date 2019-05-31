---
title: DSP First - Chapter 4 - Sampling and Aliasing
date: 2018-12-20 09:01:28
tags: DSP First
categories: DSP
mathjax: true
toc: true
---

Sinusoids, or sinusoidal signals, representing the cosine or sine signals/waves, are the most basic signals in the theory of signals and systems. This chapter introduces the basic sinusoid concepts and operations.

<!--more-->

### Review of sine and cosine functions
- Basic [trigonometric functions](https://en.wikipedia.org/wiki/Trigonometric_functions).

#### Properties
- Equivalence: $\sin\theta = \cos(\theta-\pi/2)$ or $\cos\theta=\sin(\theta+\pi/2)$; **the sine function is just a cosine function that is shifted to the right by $\pi/2$**,
- Periodicity: $\cos(\theta + 2\pi k) = \cos\theta$, where $k\in \mathbb{Z}$,
- Evenness of cosine: $\cos(-\theta) = \cos\theta$,
- Oddness of sine: $\sin(-\theta) = -\sin\theta$,
- Zeros of sine: $\sin(\pi k) = 0$, for $k\in\mathbb{Z}$,
- Ones of sine: $\cos(2\pi k) = 1$, for $k\in\mathbb{Z}$,
- Minus ones of cosine: $\cos[2\pi(k+\dfrac{1}{2})]=-1$, for $k\in\mathbb{Z}$,x
- Derivatives: $\dfrac{d \sin\theta}{d \theta} = \cos\theta$ and $\dfrac{d \cos\theta}{d \theta} = -\sin\theta$.

#### Trigonometric identities
- $\sin^2\theta + \cos^2\theta = 1$,
- $\cos^2\theta = \cos^2\theta - \sin^2\theta$,
- $\sin^2\theta = 2\sin\theta\cos\theta$,
- $\sin(\alpha\pm\beta) = \sin\alpha\cos\beta \pm \cos\alpha\sin\beta$,
- $\cos(\alpha\pm\beta) = \cos\alpha\cos\beta \mp \sin\alpha\sin\beta$,
- $\cos^2\theta = \frac{1}{2}(1+\cos 2\theta)$,
- $\sin^2\theta = \frac{1}{2}(1-\cos 2\theta)$.


### Sinusoidal signals
#### The general mathematical formula for a cosine signal is
$$\begin{equation}
   x(t) = A\cos(\omega_0 t + \phi) = A\cos(2\pi f_0 t + \phi),
\end{equation}\label{cos}$$
where 
- $A$ is the *amplitude*,
- $\omega_0$ is the *radian frequency* (rad/sec),
- $\phi$ represents the *radian phase-shift* (rads),
- $f_0 = \omega_0/2\pi$, the *cyclic frequency* (sec$^{-1}$), represents the number of periods (cycles) per second,
- $T_0 = \dfrac{1}{f_0} = \dfrac{2\pi}{\omega_0}$, the *period* (sec), is the one cycle length of the sinusoid in time.

#### Phase shift and time shift
- Having $x_1(t) = x(t-t_1)$, we say $x(t)$ is a time-shifted version of $s(t)$
  - if $t_1 > 0$ (*positive*), shifted to the right = *delayed*,
  - if $t_1 < 0$ (*negative*), shifted to the left  = *advanced*.
- Taking the sinusoid as the form in Eq. $\eqref{cos}$,
  - convert time shift to a phase shift: $x(t-t_1) = A\cos(\omega_0(t-t_1)+\phi) = A\cos(\omega_0t+\phi+\phi_1)$, where $\phi_1 = -\omega_0t_1$ is the phase shift.
  - $t_1 = -\dfrac{\phi}{\omega_0} = -\dfrac{\phi}{2\pi f_0}$,
  - $\phi_1 = -2\pi f_0 t_1 = -2\pi\dfrac{t_1}{T_0}$.
- **Based on the definition** of the time shift and the phase shift, **they have the opposite direction**, e.g., if the time shift is positive (delay), the phase shift would be negative.
- modulo reduction and principal value of the phase.

### Sampling and plotting sinusoids
- Be careful of the use of $n$ and $t$, meaning one can use either $x(nT_s)$ or $x(t)$ but never $x(tT_s)$.

### Complex exponentials and phasors
- Complex exponentials signals provide an alternative representation for the real cosine signal and might make some manipulation or analysis easier.

#### Review of complex numbers
- Real part and imaginary part.
- Cartesian form or polar form.
- Magnitude and argument
- Euler's formula: $e^{j\theta} = \cos\theta + j\sin\theta$

#### Complex exponentials signal
- $\bar{x}(t) = Ae^{j(\omega_0t + \phi)}$
- $x(t) = \Re{\{Ae^{j(\omega_0t+\phi)}\}} = A\cos(\omega_0t+\phi)$

  
#### The rotating phasor interpretation
- The complex exponential signal could be expressed as $\bar{x}(t)=Xe^{j\omega_0t}$, i.e., the product of the *complex amplitude* $X=Ae^{j\phi}$ and the *complex-valued* function $e^{j\omega_0t}$.
- The complex amplitude $X$ is also called the **phasor** (vs. vector) (相量 vs. 向量).
- $\bar{x}(t)=Xe^{j\omega_0t}=Ae^{j\theta(t)}$, where $\theta(t) = \omega_0t + \phi$.
- In the complex plane, $\bar{x}(t)$ is simply a rotating vector at a constant rate $\omega_0$ with initial phase $\phi$ ($t=0$). So *a complex exponential signal* is a **rotating phasor**.
  - $\omega_0 > 0$: rotating counterclockwise,
  - $\omega_0 < 0$: rotating clockwise.
  
#### Inverse Euler formulas
- Applying the inverse Euler's formula, the real cosine signal with radian frequency $\omega_0$ is composed of two conjugated complex exponential signals with frequencies of $\omega_0$ and $-\omega_0$, and also complex amplitudes of $\frac{1}{2}Ae^{j\phi}$ and $-\frac{1}{2}Ae^{j\phi}$, respectively.
  $$x(t) = A\cos(\omega_0t+\phi) = \frac{1}{2}\bar{x}(t) + \frac{1}{2}\bar{x}^*(t) = \Re{\{\bar{x}(t)\}}$$

### Phasor Addition 
- Additions of sinusoids with the same frequency but different amplitudes and phases

#### Addition of complex numbers
- $z_1+z_2= (x_1+x_2)+j(y_1+y_2)$.

#### Phasor addition rule
- *The summation of sinusoids with the same frequency is a sinusoid with the identical frequency with the amplitude and phase of a certain phasor calculated by the summation of the phasors of each sinusoid.*
- Summation of phasors is also a phasor: 
    $$\begin{equation}
	  \sum_{k=1}^N A_ke^{j\phi_k} = Ae^{j\phi}
	  \end{equation} \label{phasor_sum}$$
- Finally, lead us to: $$\sum_{k=1}^N A_k\cos(\omega_0t + \phi_k) = A\cos(\omega_0t + \phi)$$
  which could be proved either by
  - trigonometric identities, or
  - summation of phasors following the steps:
    1. Get the phasors $X_k = A_ke^{j\phi_k}$ of each individual cosine signals,
    2. Add phasors using Eq. $\eqref{phasor_sum}$, employing polar-to-Cartesian-to-polar conversion,
    3. Multiply the resulting phasor $X=Ae^{j\phi}$ with the rotating function $e^{j\omega_0t}$ and get $\bar{x}(t)$,
    4. Take the real part and get $x(t) = \bar{x}(t)$.

### Tuning fork and its physics
- higher-frequency "ting" and the lower-frequency "hum", where the "ting" comes from the *transient*.


