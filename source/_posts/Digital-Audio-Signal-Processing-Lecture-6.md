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
- **E.g.**, $h[n]=u[n]$ $\leftrightarrow$ $h_i[n]=\delta[n]-delta[n-1]$, where $h*h_i = \delta$
- Infinite impulse response $\longleftrightarrow$ finite impulse response, where the stability needs to be checked when inversion is from finite IR to infinite IR.




### Notable notes

