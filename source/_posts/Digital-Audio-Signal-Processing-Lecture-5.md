---
title: Digital Audio Signal Processing Lecture 5 (Notes)
mathjax: true
toc: true
date: 2019-02-05 18:00:52
tags: Lecture Notes (DASP)
categories: DSP
---
Notes of Digital Audio Signal Processing, Lecture 5.
<!--more-->

### Convolution and multiplication
  - $Z(f)=X(f)Y(f)\leftrightarrow z=x*y$ 
  - $Z(f)=X(f)*Y(f)\leftrightarrow z=xy$
  - Application in Source-Filter model

### [Parseval's theorem](https://en.wikipedia.org/wiki/Parseval%27s_theorem)
$$\sum\limits_{n=-\infty}^\infty x^2[n]= \dfrac{1}{2\pi}\int_{-\pi}^{\pi}|X(e^{j\hat{\omega}})|^2\text{d}\hat{\omega}=\int_{-\frac{1}{2}}^{\frac{1}{2}}|X(f)|^2\text{d}f,$$
where the $|X(f)|^2$ is called the power spectral **density** which is with respect to frequency.

- To prove:
  - Given signal and its DTFT $x\leftrightarrow X$
  - For the time reversed version of $x$, $y[n] = x[-n] \leftrightarrow Y(f)=\overline{X}(f)$
  - For signal $z$ whose DTFT is defined as $Z(f)=X(f)Y(f) = X(f)\overline{X}(f)$. $z=x*y$
  - In time domain: $z[n]=\sum\limits_{k\in\mathbb{Z}}x[k]y[n-k] = \sum\limits_{k\in\mathbb{Z}}x[k]x[k-n]$, where $\sum\limits_{k\in\mathbb{Z}}x[k]x[k-n]$ is the [autocorrelation](https://en.wikipedia.org/wiki/Autocorrelation). When $n=0$, $$\begin{equation}z[0]=\sum_\limits{k\in\mathbb{Z}}x^2[k]\label{Parseval1}\end{equation}$$. 
  - Taking the inverse DTFT: $z[n] = \int_{-\frac{1}{2}}^{\frac{1}{2}}Z(f)e^{2\pi jfn}\text{d}f = \int_{-\tfrac{1}{2}}^{\tfrac{1}{2}}X(f)Y(f)e^{2\pi jfn}\text{d}f$. When $n=0$, $$\begin{equation}z[0]=\int_{-\frac{1}{2}}^{\frac{1}{2}}|X(f)|^2\text{d}f\label{Parseval2}\end{equation}$$.
  - Eq. $\eqref{Parseval1}$ = Eq. $\eqref{Parseval2}$.


### Symmetry properties of signal and related spectral properties.

- Even: $x_e[n]=x_e[-n]$
- Odd: $x_o[n]=-x_o[-n]$
- properties:
  - $x_e\bot x_o$, ($\sum x[n]y[n]=0$, dot product equals zero)
  - $\text{odd}\times\text{even} = \text{even}$
- For any signal, it could be decomposed as into an even signal and an odd signal, meaning, $x[n] = x_e[n]+x_o[n]$, where $x_e[n] = \frac{x[n]+x[-n]}{2}$ and $x_o[n] = \frac{x[n]-x[-n]}{2}$
- Apply it into Fourier transform 
$$ \begin{align}
      X(f) &= \sum\limits_{n\in\mathbb{Z}}x[n]e^{-2\pi jfn}\\
	       &= \sum\limits_{n\in\mathbb{Z}}(x_e[n]+x_o[n])(\cos 2\pi fn - j \sin2\pi fn)\\
		   &= \sum\limits_{n\in\mathbb{Z}}(x_e[n]\cos2\pi fn - jx_o[n]\sin2\pi fn),\\
   \end{align}$$
   where **the $\Re{\{X(f)\}}$ is even and the $\Im{\{X(f)\}}$ is odd. **
   - So a real spectrum means the even signal and a pure imaginary spectrum corresponds to a odd signal.

### Frequency shift and modulation
- $z=xp_{f_0}$ ($z[n]=x[n]e^{2\pi jf_0n}$)
- Its Fourier transform: $Z(f) = X*P_{f_0}=X(f-f_0)$, where $P_{f_0}(f)=\delta(f-f_0)=\delta_{f_0}(f)$
- **Periodic in one domain** means **evenly spaced in the other domain**.
- [Dirac comb](https://en.wikipedia.org/wiki/Dirac_comb)

### Derivative of a Spectrum
- $$
  \begin{align}
      \dfrac{\text{d} X(f)}{\text{d} f} 
	     &= \frac{\text{d} \sum\limits_{n\in\mathbb{Z}}x[n]e^{-2\pi jfn}}{\text{d} f}\\
	     &= -2\pi j \sum\limits_{n\in\mathbb{Z}}nx[n]e^{-2\pi jfn}
  \end{align}$$
- Application: **gain**
  - $x[n] \rightarrow y[n] = g[n]x[n]$, where $g[n] = a+bn$ is a gain, linearly evolves over time.
  - $y[n]=ax[n]+b(nx[n])$  $\leftrightarrow$ $Y(f) = aX(f)+\frac{bj}{2\pi}\frac{\text{d} X(f)}{\text{d}f}$.
  - **gain in time** $\leftrightarrow$ **derivative in spectrum**
  - **Further explanation?**
  
### Time scaling
- $y(t)=x(\alpha t)$ $\leftrightarrow$ $Y = \frac{1}{\alpha}X(\frac{f}{\alpha})$

### Discrete-time system
- A system: $y=\mathcal{T}\{x\}$ or $y[n] = \mathcal{T}\{x\}[n]$
- Like delay ($y[n]=x[n-n_0]$), square ($y[n]=x^2[n]$), moving max, threshold and so on.
- **Distortion - Chebyshev polynomials?**
- **Noise reduction need distortion?**

#### classes
- memoryless: only the current time (no past, no future samples);
- linear: additivity and scalability
- time invariance: the system propcessing doesn't depends on when you apply it ($y[n-{n_0}]=\mathcal{T}\{x[n-{n_0}]\}$)
- Stability: $\lVert x\rVert < B_x$ $\leftrightarrow$ $\lVert y\rVert < B_y$.
  - delay: stable
  - amplifier: stable
  - accumulator: dependsf
  
### Linear Time-Invariant system $\leftrightarrow$ filter
- A filter is a LTI system.
- $x[n] = \sum\limits_{k\in\mathbb{Z}}x[k]\delta[n-k]$
  $$\begin{align}
    y[n] &= \mathcal{T}\{x\}[n] \\
	     &= \mathcal{T}\{\sum\limits_{k\in\mathbb{Z}}x[k]\delta_k[n]\}\\
		 &= \sum\limits_{k\in\mathbb{Z}}\mathcal{T}\{x[k]\delta_k[n]\}\\
		 &= \sum\limits_{k\in\mathbb{Z}}\{x[k]\mathcal{T}\{\delta_k[n]\}\} \quad \text{applying linearities}\\
		 &= \sum\limits_{k\in\mathbb{Z}}x[k]h_k[n],
    \end{align}
  $$
  where $h_k=\mathcal{T}\{\delta_k\}$ is the **impulse reponse**.
- $y=x*h$
- $Y=XH$, where $H$ is the Fourier transform of $h$ and is the frequency response.
- [Toeplitz matrix and convolution](https://en.wikipedia.org/wiki/Toeplitz_matrix#Discrete_convolution)
- For convoluion: $N_y = N_x+N_h-1$
- Properties:
  - Stability: depends on $h$, meaning the bound of $\sum\limits_{k\in\mathbb{Z}}|h[n-k]|$
  - causality: $h[n-k]=0$ for $k\leq n$.
  - memoryless: $h[k]=0$ when $k\neq 0$

### Notable notes
- Energy: the accumulated version of the power $x^2[n]$
