---
title: Digital Audio Signal Processing Lecture 1 (Notes)
mathjax: true
toc: true
date: 2019-01-15 20:13:15
tags: Lecture Notes (DASP)
categories: DSP
---
Notes of Digital Audio Signal Processing, Lecture 1.
<!--more-->

## Introduction
- Tools and concepts used in the course: quantitative, math, symbolic
- Symbolic representation

## Symbolic Representation
- numbers: $i,j,k,l,m,n$ (interger), $x,y,z,t$ (coordinate).
- Interger: count object: $\mathbb{Z,V}$
- Real: $\mathbb{R}$ + rational $x=\dfrac{p}{q}$

## Properties Links
- $\subset$ (includes), $\in$ (belong to)
- $s_i$, where $i\in[0,1\cdots]$
- $m=\dfrac{1}{N}\sum\limits_{i=0}^{N-1}s_i$ 

## Sequence and Series
### Sequence
- **Definition**: ordered set of values (mathmatical objects).
- Arithmetic sequence
  - $$
u_n=
\begin{cases}
 a,\quad n=0, \\
 u_{n-1}+b,\quad n>0.
\end{cases}
$$
  - or $u_n=a+nb$.
- Geometric sequence
  - $$
u_n=
\begin{cases}
 a,\quad n=0, \\
 u_{n-1}\cdot b,\quad n>0.
\end{cases}
$$
  - or $u_n=a\cdot b^n$.
- Harmonic sequence
  - $u_k[n]=a_k\cos(2\pi f_k n +\phi_k)$
  
### Series
- **Definition**: $S_n=\sum\limits_{i=0}^n u_i$
- Arithmetic series
$$
\begin{align}
S_n&= \sum\limits_{i=0}^n (b+ia) \\
&= \sum\limits_{i=0}^n b \sum\limits_{i=0}^n ia \\
&= (n+1)b + a\dfrac{n(n+1)}{2} \\
&= (n+1)\cdot(b+\dfrac{an}{2}).
\end{align}
$$
- Geometric series
$$S_n=\sum\limits_{i=0}^n ba^i=b\cdot\sum\limits_{i=0}^n a^i = b\left(\dfrac{1-a^{n+1}}{1-a}\right)$$, when $n\rightarrow \infty$
  - $|a|<1 \rightarrow S_n=b\dfrac{1}{1-a}$
  - $|a|>1 \rightarrow S_n=\pm\infty$
- Fourier series
$S_K[n]=\sum\limits_{k=0}^Ku_k[n]=\sum\limits_{k=0}^K a_k\cos(2\pi f_k n+\phi_k)$

### Vectors & Matrices

