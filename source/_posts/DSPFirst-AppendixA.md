---
title: DSP First - Appendix A - Complex Numbers
date: 2018-12-18 22:18:05
tags: DSP First
categories: DSP
mathjax: true
toc: true
---

- In this appendix, the basic manipulations of complex numbers are reviewed. There ideas are treated:
  - simple algebraic rules: operations on $z = x+jy$.
  - elimination of trigonometry: Euler's formula for the complex exponential $z = re^{j\theta}=r\cos\theta+jr\sin\theta$.
  - representation by vectors: a way for visualization.
- Symbol: $i$ or $j$
  - Physicists and mathematicians use symbol $i=\sqrt{-1}$.
  - Electrical engineers use symbol $j=\sqrt{-1}$ instead because $i$ is left to the current.
- Algebraic vs. Trigonometric vs. Geometric.

### A.1 Introduction
- The way $j$ is introduced: $z^2=-1$ ==> $z=\pm j$.
- More general, complex numbers are the roots of quadratic equations.

### A.2 Notation for complex numbers
- There are two types complex number representations:
  - Rectangular form (Cartesian form): $z = (x, y) = x + jy = \Re \{ z \}  + j\Im\{z\}$, where $\Re\{\}$ and $\Im\{\}$ represent the real and imaginary parts of the complex number, respectively.
  - Polar form: $z \leftrightarrow r\angle\theta$ where $r$ is the amplitude and $\angle\theta$ is the angle whose principal value belongs to $-180^{\circ}<\theta < 180^{\circ}$
  - Conversion:
    - polar --> rectangular: $z=x + jy$, where
       $$\begin{equation}
	        \begin{cases}
	        x = r\cos\theta,\\
			y = r\sin\theta
			\end{cases}
	   \end{equation}	\label{eq1}$$
	- rectangular --> polar: $z = re^{j\theta}=|z|e^{j\, \text{arg}|z|}$, where
	   $$\begin{equation}
	        \begin{cases}
	        r = \sqrt{x^2+y^2},\\
			\theta = \text{atan}(y, x)
			\end{cases}
	   \end{equation}	\label{eq2}$$

### A.3 Euler's formula
- Euler's formula
$$ \begin{equation} e^{j\theta} = \cos{\theta} + j\sin\theta \end{equation}\label{Euler} $$
- Inverse Euler fomulas
$$ \begin{align}
      \cos\theta &= \frac{e^{j\theta} + e^{-j\theta}}{2}\\
      \sin\theta &= \frac{e^{j\theta} - e^{-j\theta}}{2}
   \end{align}$$

### A.4 Algebraic rules for complex numbers
#### Rectangular form
For $z_1 = x_1 + jy_1$ and $z_2 = x_2+jy_2$, 

- addition and subtraction: $z_1 \pm z_2 = (x_1 \pm x_2) + j(y_1 \pm y_2)$.
- multiplication: $z_1 z_2$ = (x_1x_2-y_1y_2)+j(x_1y_2+x_2y_1)$
- conjugate: $z_1^* = x_1 - jy_1$
- division: $\dfrac{z_1}{z_2} = \dfrac{z_1z_2^*}{z_2z_2^*} = \dfrac{z_1z_2^*}{|z_2|^2} = \dfrac{(x_1x_2+y_1y_2) + j(x_2y_1-x_1y_2)}{x_2^2+y_2^2}$

#### Polar form
For $z_1 = r_1e^{j\theta_1}$ and $z_2 = r_2e^{j\theta_2}$,

- multiplication: $z_1z_2 = (r_1r_2)e^{j(\theta_1+theta_2)}$
- conjugate: $z_1^* = r_1e^{-j\theta_1}$
- division: $\dfrac{z_1}{z_2} = \dfrac{r_1}{r_2}e^{j(\theta_1-\theta_2)}$
- addition and subtraction: transfer to rectangular form and do the addition or subtraction, and then, transfer back to polar form.

#### others
- $\Re\{z\} = \dfrac{z+z^*}{2}$
- $\Im\{z\} = \dfrac{z-z^*}{2j}$
- $|z|^2 = zz^*$

### A.5 Geometric views off complex operations
A geometric view provides a convenient visualization for complex number operations.

### A.6 Powers and Roots
- $z^N = (re^{j\theta})^N = r^Ne^{jN\theta}$
- De Moivre's formula: $(\cos\theta + j\sin\theta)^N = \cos N\theta + j\sin N\theta$ (because $(e^{j\theta})^N = e^{jN\theta}$)
- Roots of unity ($z^N=1$): $z=e^{j2\pi l/N}$ for $l=0,1,2\dots N-1$
- $z^N=c=|c|e^{j\phi}$: $z=re^{j\theta}$, where
  $$\begin{cases}
  r = |c|^{1/N},\\
  \theta = \dfrac{\phi+2\pi l}{N},
  \end{cases}$$
  and $\theta$ is the angular spacing.


<!-- the famous matter-energy equation $\eqref{eq1}$ proposed by Einstein ...-->
