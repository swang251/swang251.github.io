---
title: DSP First - Chapter 5 - FIR Filters
date: 2018-12-24 13:10:07
tags: DSP First
categories: DSP
mathjax: true
toc: true
---

> A **filter** is a system that is designed to remove some component or modify some characteristic of a signal.

<!--more-->
Several different things are introduced, including:
- *Finite impulse response (FIR)* systems: refered as FIR filters, are systems for which *each output value is the sum of a finite number of weighted values of the input sequence*.
- *Difference equation*: the basis of the input-output structure of the FIR filter as a time-domain computation.
- *Unit impulse response*
- *Convolution*
- *Linearity* and *time invariance*
- *Discrete-time systems*

### Discrete-time systems
> A discrete-time system is a computational process for transforming one sequence into another sequence.
- $x[n]\rightarrow \mathcal{T}\{\cdot\}\rightarrow y[n]=\mathcal{T}\{x[n]\}$, where $x[n]$ is the input signal and $y[n]$ is the output signal, both of which are discrete-time signals.

### The running-average (moving-average) filter
- [Difference equation](https://ccrma.stanford.edu/~jos/fp/Difference_Equation_I.html), e.g., the general, causal, linear and time invariant difference equation:
  $$\begin{equation}
    y[n] = \sum\limits_{k=0}^M b_k x[n-k] - \sum\limits_{l=0}^N a_l y[n-l],
  \end{equation}\label{DE}$$
  where $k$ and $l$ are the "dummy" counting indices for the sum and $n$ denotes the index of the $n^{th}$ sample of the output sequence.
- Causal and noncausal:
  - *Causal filter*: a filter that uses only the present and past values of the **input**.
  - *Noncausal filter*: a filter that uses future values of the **input**.
- Causal running averager or backward averager, similarly, we have the centralized running averager and the forward averager.

### The general FIR filter
- The general causal difference equation
  $$\begin{equation}
    y[n] = \sum\limits_{k=0}^M b_k x[n-k],
  \end{equation}\label{FIR}$$
  where the coefficients $b_k$ are fixed numbers. 
  - $M$, the *order* of the FIR filter
  - $L=M+1$, the number of filter coefficients is the filter *length*
- Eq. $\eqref{FIR}$ could be written as
  $$\begin{equation}
    y[n] = \sum\limits_{l=n-M}^n b_{n-l} x[l],
  \end{equation}\label{FIR_l}$$
  where $l=n-k$ showing the FIR is causal using the input $x[l]$ start from the previous $M$ samples, i.e. $l=n-M$, up to the current one $l=n$
- For finite length input signal, i.e., $x[l]\neq 0$ for $l\in[0, N-1]$ and a $M^{th}$-order FIR filter (of length $M+1$, i.e., involving $M+1$ samples), there would be *transient component* of the output including $M$ samples *running onto* and *running off* session. And the total output length would be $N+M\text{ (order)}=N+L-1$.

### The unit impulse response and convolution
> The impulse response provides a complete characterization of the FIR filter.
- Three new ideas introduced:
  - the unit impulse sequence
  - the unit impulse response
  - the convolution sum
  
#### Unit impulse sequence
- Unit impulse, or mathematically taken as the Kronecker *delta function*
  $$\begin{equation}
   \delta[n]=
      \begin{cases}
      1\quad n=0\\
	  0\quad n\neq 0
      \end{cases}
  \end{equation}\label{deltaFunction}$$
- *Express any sequence interm of delta function*
  $$\begin{equation}
    x[n]=\sum\limits_k x[k]\delta[n-k]
	\end{equation}\lab
	el{x}$$
  - the unit impulse is a sequence
  - $\mathbf{x}$ is a summation of infinite impulse sequences $\mathbf{\delta}_k$

#### Unit impulse response sequence
- The output from a filter is called the **response** to the input.
- **Unit impulse response** $h[n]$ represents the output when the input is the unit impulse $\delta[n]$.
