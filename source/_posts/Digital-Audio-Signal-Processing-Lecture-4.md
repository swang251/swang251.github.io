---
title: Digital Audio Signal Processing Lecture 4 (Notes)
mathjax: true
toc: true
date: 2019-01-29 17:38:43
tags: Lecture Notes (DASP)
categories: DSP
---
Notes of Digital Audio Signal Processing, Lecture 4.

NOTA: All $f$ in this blog refers to the normalized frequency.
<!--more-->

### Different representation

#### Time-domain representation
  - $\delta_k$: the feature of time, representing time 'k';
  - $x = \sum\limits_{k\in\mathbb{Z}} x[k]\delta_k$ or $x[n] = \sum\limits_{k\in\mathbb{Z}}x[k]\delta[n-k]$

#### Frequency-domain representation (spectrum)
- $p_f[n] = e^{2\pi jfn}$: the feature of frequency, and be used to represent $x[n]$ in terms of frequency $f$.
- $x[n]$ is a linear combination of $p_f[n]$ $\rightarrow$ $x[n] = \int X(f)p_f[n]\text{d}f$, where $X(f)$ is the Fourier representation.

### Heuristic description of Fourier Transform

#### For $x[n] = ae^{j\theta}$
- $x[n]p_{f_0}[n] = ae^{j(2\pi f_0n+\theta)}$ 
  - $\sum\limits_{n\in\mathbb{Z}} a\cos(2\pi f_0n+\theta) = a\cos\theta\delta(f_0)$,
  - $\sum\limits_{n\in\mathbb{Z}} a\sin(2\pi f_0n+\theta) = a\sin\theta\delta(f_0)$,
  - so $$
  \begin{equation}
     \sum\limits_{n\in\mathbb{Z}} ae^{j\theta}p_{f_0}n = ae^{j\theta}\delta(f_0),
  \end{equation}\label{distribution}
  $$
    where $\delta(f_0)$ is a distribution function
  
#### For $x[n] = ae^{j\theta}e^{2\pi f_0n}$
- $x[n]p_{-f}[n] = ae^{j\theta}e^{2\pi j(f_0-f)n}$
  - Looking for a modulated frquency $f_{modulated} = f_0-f$.
  - So we have, $$
  \begin{equation}\sum\limits_{n\in\mathbb{Z}} x[n]p_{-f}[n] = ae^{j\theta}\delta(f_0-f),\end{equation}$$
  meaning there is a contribution of $x[n]$ only when $f_0 = f$.
- Go for, $\sum\limits_{n\in\mathbb{Z}} x[n]p_{-f}[n]$ = $\sum\limits_{n\in\mathbb{Z}} x[n]\overline{p_f[n]} = \mathbf{x}\cdot\mathbf{p_f} = \mathbf{p_f}^H\cdot\mathbf{x}$, assuming $\mathbf{x}$ is a real vector (signal).
  - Meaning **projecting signal $\mathbf{x}$ onto the coordinate $\mathbf{p_f}$**,
  - where it first does the modulation ($e^{-2\pi jfn}$) and then the summation ($\sum$)
  - Properties of the Euclidean Inner Product: $\mathbf{u}\cdot\mathbf{v} = \overline{\mathbf{v}\cdot\mathbf{u}}$
- **Fourier transform and inverse Fourier transform**
  - $X(f)=\sum\limits_{n\in\mathbb{Z}}x[n]e^{-2\pi jfn}$: the "-" sign comes from the conjugate of $\mathbf{p_f}$ during the dot products
  - $x[n]=\int X(f)e^{+2\pi jfn}\text{d}f$: the "+" sign because these is the linear combination of $\mathbf{p_f}
  
### More about Fourier Transform
- Fourier Transform: $X(f) = \int x(t)e^{-2\pi jFt}\text{d}t$.
- Discrete-time Fourier Transform: $X(f) = \sum\limits_{n\in \mathbb{Z}}x[n]e^{-2\pi jfn}$.
- The frequency is real and continuous.
- $X(f) \in \mathbb{C}$ is periodic and complex.
- Though it is easy to prove, but **why does sampling make signal periodic in frequency domain?**
  - $X(f) = X(f+1)$
- Convergence: $|X(f)|$. ([norm](https://en.wikipedia.org/wiki/Norm_(mathematics)))

### Examples
| Time-domain $x[n]$                         | Frequency-domain $X(f)$                             |
| :-------------:                            | :------------------:                                |
| Impulse: $\delta[n]$                       | $1$                                                 |
| Damped exponential: $a^n u[n]$             | $\dfrac{1}{1-ae^{-2\pi jf}}$                        |
| Rectangular function: $r_N[n]=u[n]-u[n-N]$ | $e^{-\pi jf(N-1)}\dfrac{\sin(\pi fN)}{\sin(\pi f)}$ |


- **NOTA:** For the rectangular function, the $\dfrac{\sin(\pi fN)}{\sin(\pi f)}$ in the $X(f)$ is not the sinc function. Instead, $\dfrac{\sin(\pi f)}{\pi f} = \text{sinc}(\pi f)$, the sinc function, which is non-periodic, is the Fourier transform of the rectangular function instead of its DTFT. The sampling makes the $X(f)$ periodic in frequency domain as shown in the table.

### Theorems
- periodic in $f$
- linear
- time-shift (delay): $y[n] = x[n-d] \rightarrow Y(f) = X(f)e^{-2\pi jfd}$
- frequency-shift: $y[n] = x[n]e^{2\pi jf_0n} \rightarrow Y(f) = X(f-f_0)$
- time-reverse: $y[n] = x[-n] \rightarrow Y(f)=X(-f)$
- Frequency multiplication means time convolution and vice versa.
