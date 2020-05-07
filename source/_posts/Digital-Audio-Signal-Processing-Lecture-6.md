---
title: Digital Audio Signal Processing Lecture 6 (Notes)
mathjax: true
toc: true
date: 2019-02-12 19:33:47
tags: Lecture Notes (DASP)
categories: DSP
---
Notes of Digital Audio Signal Processing, Lecture 6.
<!--more-->

### Inverse System
- $y=\mathcal{T}\{x\}$ and $x = \mathcal{T_i}\{y\}$, where $\mathcal{TT_i} = \mathcal{T_iT} = \mathbf{I}$
- $h*h_i = h_i*h = \delta$
- **E.g.**, michrophone with a flare that is a high-pass system, needs an inverse system to get rid of the HP effect.
- **E.g.**, $h[n]=u[n]$ (accumulator) $\leftrightarrow$ $h_i[n]=\delta[n]-\delta[n-1]$, where $h*h_i = \delta$
- Infinite impulse response $\longleftrightarrow$ finite impulse response, where the stability needs to be checked when inversion is from finite IR to infinite IR.
- $power \propto amplitude^2$ 
  - Power dB = $10\log_{10}(\dfrac{p}{p_0}) = 20\log_{10}(\dfrac{a}{a_0})$
  - Amplitude dB = $5\log_{10}(\dfrac{p}{p_0}) = 10\log_{10}(\dfrac{a}{a_0})$
  
### Frequency Response of LTI System
- $p_{f_0}[n] = e^{2\pi jf_0 n}$ is the eigenvector of a filter
- Eigenvalue & eigenvector of LTI system
   - $$
   \begin{align}
      y[n] &= h*p_{f_0} = \sum\limits_{k\in \mathbb{Z}}h[k]p_{f_0}[n-k] \\
	       &= \sum\limits_{k\in \mathbb{Z}}h[k]e^{2\pi jf_0 (n-k)} \\
		   &= e^{2\pi jf_0 n}\sum\limits_{k\in \mathbb{Z}}h[k]e^{-2\pi jf_0k} \\
		   &= p_{f_0}[n]H(f_0)
   \end{align}$$
   - where $p_{f_0}$ is the eigenvector and $H(f_0)$ is the eigenvalue. 




### Notable notes

