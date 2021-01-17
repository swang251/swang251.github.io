---
title: Specific admittance of the wall for modeling the thermoviscous losses
mathjax: true
toc: true
date: 2021-01-16 21:09:12
tags: [Acoustics]
categories: Acoustics
---

The derivation of the specific admittance of the wall for modeling the thermoviscous losses can be found in Pierce's book, *Acoustics: An Introduction to Its Physical Principles and Applications* (2019, 3rd edition). This article is to note down the derivation with the key steps and equations copied from the book.

<!--more-->

## Derivation
The derivation is explained in Chapter 10.4, *Acoustic Boundary-Layer Theory*, while the entire Chapter 10 is about *Effects of Viscosity and Other Dissipative Processes*.

- > At frequencies of normal interest, any disturbance governed by the linear equations derived in the previous setion can be considered as a superposition of **vorticity**, **entropy**, and **acoustic** *modal wave fields*.
- The linear equations mentioned here refer to the *mass conservation equation*, *Navier-Stokes equation*, and the *Kirchhoff Fourrier equation*. (Eq. 10.2.2)

- The derivation starts from the notation $\psi_n(\boldsymbol{x},t) = \text{Re}\{\hat{\psi}_n e^{-i\omega t} e^{i\boldsymbol{k}\cdot\boldsymbol{x}}\}$, Eq. (10.3.1), where $\psi_n$ can be the plane-wave disturbance of either of the three modal wave fields mentioned above.

- > There are only a small number of $k^2$ for a given $\omega$ for which a nontrivial solution (at least one $\hat{\psi}_n$ not zero) exists. 
- > The resulting relations between $k^2$ and $\omega$ are the *dispersion relations* for the possible modes of propagation.
- Three different modes correspond to three different **dispersion relations**, leading to three different **PDEs**, where the nontrivial solution exists.
  - Vorticity mode: $k^2 = i\omega\rho/\mu$ ($\nabla\times\boldsymbol{v}\neq 0$, $\boldsymbol{k\cdot v}=0$)
    $$\nabla^2\boldsymbol{v}_{vor} = \dfrac{\rho}{\mu}\dfrac{\partial \boldsymbol{v}_{vor}}{\partial t}\qquad \text{(Eq. 10.3.11)}$$
  - Acoustic Mode: Eq. (10.3.7a) ($\boldsymbol{k\times v} = 0$)
    $$\nabla^2 p_{ac} - \dfrac{1}{c^2}\dfrac{\partial^2 p_{ac}}{\partial t^2} + \dfrac{2}{c^4}\delta_{cl}\dfrac{\partial^3 p_{ac}}{\partial t^3} = 0, \qquad \text{(Eq. 10.3.13)}$$
  - Entropy Mode: Eq. (10.3.7b), or $k^2\approx i\omega\rho c_p/\kappa$ ($\boldsymbol{k\times v} = 0$)
    $$\nabla^2s_{ent} = \dfrac{\rho c_p}{\kappa}\dfrac{\partial s_{ent}}{\partial t}\qquad\text{(Eq. 10.3.15)}$$
- > Any superposition of vorticity-, acoustic-, and entropy-mode fields will satisfy the linear equations for a fluid with finite viscosity and thermal conductivity. ... any disturbance satisfying those equations can be represented as such a superposition, ...
$$\boldsymbol{v} = \boldsymbol{v}_{vor}+ \boldsymbol{v}_{ac} + \boldsymbol{v}_{ent}\qquad \text{(Eq. 10.4.1)}$$
- Boundary layer thickness, determined by $1/|k_l|$, where $k_l$ is calculated using the dispersion relations.
  - $l_{vor} = \sqrt{\dfrac{2\mu}{\omega\rho}}$, **N.B., there is a typo in the book**
  - $l_{ent} = \sqrt{\dfrac{2\kappa}{\omega\rho c_p}} = \dfrac{l_{vor}}{\sqrt{\text{Pr}}}$
  - Question: why not use $2\pi/|k_l|$ to define the boundary layer thickness as $k_l$ is the wavenumber.
- The field varies much more rapidly with the $z$ coordinate than with the $x$ and $y$ coordinates ($\partial/\partial z > \partial/\partial x \sim \partial/\partial y$), as the sound wavelength is much larger then $l_{vor}$ and $l_{ent}$, so the $\nabla^2$ is approximated by $\partial^2/\partial z^2$ in Eq. 10.3.11 and Eq. 10.3.15, and leads to
  - $$\dfrac{\partial^2}{\partial z^2}\hat{\psi}(x,y,z) = -\dfrac{2i}{l^2}\hat{\psi}(x,y,z)\qquad\text{(Eq. 10.4.5)}$$
  with the solution 
  $$\hat{\psi}(x,y,z) = \hat{\psi}(x,y,0)e^{-(1-i)z/l}\qquad\text{(Eq. 10.4.6)}$$
  (substitute Eq. (10.4.6) into Eq. (10.4.5) will lead to the $-2i/l^2$ on the LHS) with 
  - $l= l_{vor}$ or $l_{ent}$, and 
  - $\hat{\psi}=\hat{s}_{ent}$ or $\hat{\boldsymbol{v}}_{vor}$.

- The $\partial/\partial z$ is replaced with $-(1-i)/l$ based on Eq. 10.4.6
- Based on the polarization relations $\nabla\cdot\boldsymbol{v}_{vor} =0 $ and $\boldsymbol{v}_{ent} \approx \left(\dfrac{\beta T \kappa}{\rho c^2_p}\right)_o\nabla s_{ent}$, and the fact that $\nabla = \nabla_T + \nabla_\boldsymbol{n}$, the Eq. (10.4.7) can be derived

- Assume the surface is oscillating as a rigid body such that every material point on the surface has a verlocity with complext amplitude $\hat{v}_{wall}$,
  $$\hat{\boldsymbol{v}}_{wall} = \hat{\boldsymbol{v}}_{vor} + \hat{\boldsymbol{v}}_{ac} + \hat{\boldsymbol{v}}_{ent} \qquad\text{(Eq. 10.4.8)}$$
- $\nabla_T\cdot(\text{10.4.8})$ + Eq. (10.4.7a) leads to Eq. (10.4.10) which express $\hat{\boldsymbol{v}}_{vor}$ in terms of $\hat{\boldsymbol{v}}_{ac,T}$
  $$\hat{\boldsymbol{v}}_{vor}  = -\dfrac{1+i}{2}l_{vor}\nabla_T\cdot\hat{\boldsymbol{v}}_{ac,T}\qquad\text{Eq.a}$$
- Take the normal component of Eq. 8 $\rightarrow(\text{Eq. 10.4.8}\cdot\boldsymbol{n})$,
  - Applying Eq. a, Eq. 10.4.7c, Eq. 10.3.14, leads to the boundary condition \*\***Eq. 10.4.12**, expressing $\hat{\boldsymbol{v}}_{wall}\cdot\boldsymbol{n}$ only in terms of acoustic variables $\hat{\boldsymbol{v}}_{ac}$ and $\hat{p}_{ac}$
  - It allows an examination of the effects of *viscosity* and *thermal* condition on the reflection of plane waves.
- Rewrite the Euler's equation
  $$\nabla_T\cdot\boldsymbol{v}_{ac,T} = -\dfrac{\sin^2\theta_i}{\rho c^2}\dfrac{\partial p}{\partial t}\qquad\text{(Eq.10.4.17)}$$
- Inserting Eq. 10.4.17 into Eq. 10.4.12 leads to the specific admittance of the surface
  $$\dfrac{1}{Z} = Y = -\dfrac{\hat{\boldsymbol{v}}_{ac}\cdot\boldsymbol{n}_{wall}}{\hat{p}} = \dfrac{1}{2}(1-i)\dfrac{\omega}{\rho c^2}[l_{vor}\sin^2\theta_i + (\gamma-1)l_{ent}]\qquad\text{(10.4.18)}$$


## Different expressions
The definitions of the specific admittance of the wall are different between Chaigne & Kergomard (2016) and Pierce (2019)

- Chaigne & Kergomard (2016): $$Y_p = \dfrac{1}{\rho c}\sqrt{\dfrac{j\omega}{c}}[\sin^2\theta\sqrt{l_v} + \sqrt{l_t}] \qquad (5.141)$$
  where the characteristic lengths $l_v = \dfrac{\mu}{\rho c}$ and $l_t = \dfrac{\kappa}{\rho c C_p}$ in Eq. (5.136), are defined differently with $l_{vor}$ and $l_{ent}$.

- Pierce (2019): $$\dfrac{1}{Z} = \dfrac{1}{2}(1-i)\dfrac{\omega}{\rho c^2}[l_{vor}\sin^2\theta_i+(\gamma-1)l_{ent}]\qquad (10.4.18)$$
- Rewrite Eq. (10.4.18) in terms of variables defined in Chaigne & Kergomard's book
	$$\dfrac{1}{Z} = \dfrac{1}{\rho c}\dfrac{1-i}{1+i}\sqrt{\dfrac{j\omega}{c}}[\sin^2\theta\sqrt{l_v} + \sqrt{l_t}]\qquad Eq. (b)$$
	
- Comparing Eq. (b) and Eq. (5.141), the difference is the term $\dfrac{1-i}{1+i}$ in Eq. (b).
  - If the $1-i$ in Eq. (10.4.18) is $1+i$, then the definitions in two books are identical to each other.
- After tracing back the derivations in Pierce (2019), I found the origin of the $1-i$ comes from the definition of the **phaser**.

- In Kinsler (1999) Fundamentals of acoustics, Ch. 1.5, it is mentioend there are different conventions to represent the time dependence of scillatory functions
  - *the engineering convention*: $\exp(j\omega t)$
  - *the physics convention*: $\exp(-i\omega t)$
- In Chaigne & Kergomard's book, it is defined as $\psi = \hat{\psi}e^{j\omega t}$, while in the Pierce's book, it is defined as $\psi = \hat{\psi}e^{-i\omega t}$. It is this difference that leads to the differences in the definition of the wall losses
- Different conventions are also reflected in the definition of the wave number involving the attenuation coefficient as shown in Eq. (10.5.10) in Pierce's book, which can be used to calculate $\Gamma$ for the transfer matrix of a cylinder.
	$$k = \omega/c + (1+i)\alpha_{walls} \qquad \text{(10.5.10) in Pierce's book}$$
    - If the engineering convention is applied, Eq. 10.5.10 becomes, $k=\omega/c + (1-i)\alpha_{walls}$, which is the one used in some papers, 
	  - Van Walstijn, M. et al. (2005) Wideband measurement of the acoustic impedance of tubular objects
	  - Mason, W.P. (1928) The propagation characteristics of sound tubes and acoustic filters

## References
- https://www.comsol.com/blogs/theory-of-thermoviscous-acoustics-thermal-and-viscous-losses/
- Pierce, A. D., 2019, Acoustics: An Introduction to Its Physical Principles and Applications, Springer International Publishing.
- Chaigne, A., and Kergomard, J., 2016, Acoustics of Musical Instruments, Springer-Verlag, New York.
- Kinsler, L. E., Frey, A. R., Coppens, A. B., and Sanders, J. V., 1999, Fundamentals of Acoustics, Wiley.






