---
title: Digital Audio Signal Processing-Lecture 2 (Notes)
date: 2019-01-15 19:15:03
tags: Lecture Notes (DASP)
categories: DSP
mathjax: true
toc: true
---
Notes of Digital Audio Signal Processing, Lecture 2.
<!--more-->

## Dot product
- $D(\mathbf{u},\mathbf{v})=\sum_{i=1}^3u_iv_i$
- The [correlation](https://en.wikipedia.org/wiki/Correlation_and_dependence#Definition) is related to dot product, see [here](https://qr.ae/TUnqvl).
- norm ($\left\lVert\mathbf{u}\right\rVert = D(\mathbf{u},\mathbf{u})=\sum_{i=1}^3u_i^2$) $\rightarrow$ dot product ($D(\mathbf{u},\mathbf{v})=\sum_{i=1}^3u_iv_i$) $\rightarrow$ Energy $\left\lVert\mathbf{u}\right\rVert ^2$.
- $D(\mathbf{u},\mathbf{u}) = \mathbf{u}^\intercal \mathbf{u}$
- inner product
- Signal in discrete time of lenght $N$ has a dimension of $N$;
- [Orthogonal](https://en.wikipedia.org/wiki/Orthogonality) $\mathbf{s_1}^\intercal \mathbf{s_2} = 0$, meaning, nonzeros in $\mathbf{s_1}$ correspond to zeros in $\mathbf{s_2}$ $\rightarrow$ **Frequency does not overlap ??**

## Matrix
- A matrix is a system.
- [**Hadamard matrix**](https://en.wikipedia.org/wiki/Hadamard_matrix) $\rightarrow$ [Hadamard Transform](https://en.wikipedia.org/wiki/Hadamard_transform) is an example of a generalized class of Fourier transform. 
- [**Rotation matrix**](https://en.wikipedia.org/wiki/Rotation_matrix)
- In Matlab, `u.*v` equals `diag(u)*v` (element-wise multiplication), where `diag(u)` is the **temporal envelope**.
- In Matlab, $B^{-1}C=$`B\C` and $B/C^{-1}=$`B/C`.
- The relationship between **the deconvolution and the inverse of a matrix**
- [**Toeplitz matrix**](https://en.wikipedia.org/wiki/Toeplitz_matrix) and its "upside down" version - [**Hankel matrix**](https://en.wikipedia.org/wiki/Hankel_matrix) $\rightarrow$ filter correlation $\rightarrow$ **Transmission line matrix (Waveguide)**
- [**VanderMonde matrix**](https://en.wikipedia.org/wiki/Vandermonde_matrix) $\rightarrow$ damped sine wave (inversion) $\rightarrow$ noise cancellation
- Matrices might not be inversable just like one might not recover the original signal from its projection onto one axis.
- $(\mathbf{ABC})^\intercal = \mathbf{C}^\intercal\mathbf{B}^\intercal\mathbf{A}^\intercal$
- [Eigenvector $\mathbf{v}$ and eigenvalues $\lambda$ ](https://en.wikipedia.org/wiki/Eigenvalues_and_eigenvectors). "Eigen" origins from German for "proper".
  - $T(\mathbf{v})=\lambda\mathbf{v}$: $T$ is a linear transform and $\mathbf{v}$ and $\lambda$ are its eigenvector and eigenvalue.
  - [The spectrum of a matrix is the set of its eigenvalues](https://en.wikipedia.org/wiki/Spectrum_of_a_matrix) and each eigenvector represents one frequency or one dimension/direction. Check [**Eigendecomposition of a matrix**](https://en.wikipedia.org/wiki/Eigendecomposition_of_a_matrix).



## Functions and Polynomials
- Linear (gain or interpolation), exponential (the feedback loop) and polynomial functions (spline interpolation, harmonic distortion or representing any functions)
- Chebyshev Polynomial and distortion
- Roots of polynomials $p_n(x_i) = 0$
  - `roots` (order limits)
  - $p_n(x) = (x-x_1)p_{n-1}(x) = a_n\prod_{i=1}^n(x-x_i)$ **??**

## Rational
- $f(x) = \frac{Q}{P}$ 
- Filter frequency response is a rational function (for most of cases), e.g., an exception, viscosity loss of pipe $\rightarrow$ $\sqrt{f}$ $\rightarrow$ irrational function

## Complex numbers

### Imaginary
- Matlab considers a number to be complex ($\mathbb{C}$)  
- Complex number is defined because it does not exist in $\mathbb{R}$ or is just not defined before?
- $j, -1, -j, 1$ for $j^n$, where $n=1,2,3,4$.
- Imaginary, a good word, but [imaginary is not real imaginary](https://www.math.toronto.edu/mathnet/answers/imaginary.html)

### Phase and angle
- `atan2`, "2" because it accepts two arguments and `angle` in Matlab uses `atan2`
- phase in(de)crease infinitely but how?

### Conjugate
- [conjugate](http://www.oed.com/view/Entry/39266?rskey=5nAP9w&result=1&isAdvanced=false#eid) meaning the opposite angle
- real coefficients of polynomial $\rightarrow$ roots must be grouped by pairs
- Euler's formula$\rightarrow$
- $e^{j\theta} = \cos\theta+j\sin\theta$ where $e^{j\theta}$ is the [analytic signal](https://en.wikipedia.org/wiki/Analytic_signal), the analytic representation of the real-value function ([analytic continuation](https://en.wikipedia.org/wiki/Analytic_continuation))
- Transfer complex to real after passing a linear system is true but it is not true for a nonliear processing. **WHY?**

### Unity Circle

- For root of unity $z^N=1$, there are $N$ Nth root because it is an Nth-order polynomial $1-z^N=0$.
- Reciprocal of $z$ $\rightarrow$ unit circle (in(out)side) $\rightarrow$ stability ((un)stable)
- polynomial
  - [Complex conjugate root theorem](https://en.wikipedia.org/wiki/Complex_conjugate_root_theorem): real coefficients $\rightarrow$ roots are conjugate pairs.
  - symmetrical coefficients $\rightarrow$ roots are conjugate inverse pairs
  - when, $|z|=1$, $z^*=\dfrac{1}{z}$, roots are pairs of both inverse and conjugate, and are on unit circle.
- For [complex vectors](https://en.wikipedia.org/wiki/Dot_product#Complex_vectors) $\mathbf{u}$ and $\mathbf{v}$,
  - $D(u,v) = \sum_{i=1}^{N}\bar{u}_iv_i=u^{*T}v = u^Hv$, $H$ means transposed and conjugated $\rightarrow$ ```u'``` in Matlab
  - `u.'` only does the transpose
  - $D(u,v)=\overline{D(v,u)}$
  

