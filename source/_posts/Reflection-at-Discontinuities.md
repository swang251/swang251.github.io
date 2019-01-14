---
title: Reflection at Discontinuities
date: 2018-10-21 23:58:25
tags: [Acoustics]
categories: Acoustics
mathjax: true
---
I got suddenly confused about how the reflection coefficient is computed, and it took me a whole night to figure out my mistake.

<!--more-->

Consider such a case, when a wave is propagating, there is an abrupt discontinuity, which separates two different medium $M1$ and $M2$ to the left and right of the discontinuity point, respectively. The two medium has two different characteristic impedance $Z_1$ and $Z_2$. (It could also be the same media with different cross-section areas in a tube).

The pressure in $M1$ is decomposed into a right-going wave $p_1^+$ and a left-going wave $p_1^-$, which correspond to incident and reflection, respectively. So the right- and left-going volume flow rate are $\dfrac{p_1^+}{Z_1}$ and $-\dfrac{p_1^-}{Z_1}$. (the "$-$" sign means the left-going traveling direction) 

Assuming the continuity of the pressure and the conservation of the volume flow at the boundary, we have:
$$\begin{equation}
   p_1^+ + p_1^- = p_2^+ + p_2^-
   \end{equation} \label{1} $$
and 
$$\begin{equation}
   \dfrac{p_1^+ - p_1^-}{Z_1} = \dfrac{p_2^+ - p_2^-}{Z_2} 
   \end{equation} \label{2}$$

**From here the problem comes.** I try to compute the reflection coefficient from the above two equations, but of course, I can't get anything. **This is because** the reflection coefficient is not related to $Z_2$. Instead, it relates to the load impedance $Z_{load}$, e.g., the input impedance of the system to the right of the discontinuity point. So we will replace the eq. $\eqref{1}$ and eq. $\eqref{2}$ by 
$$\begin{equation}
   p_1^+ + p_1^- = p_2
   \end{equation} \label{3}$$
and
$$\begin{equation}
   \dfrac{p_1^+ - p_1^-}{Z_1} = \dfrac{p_2}{Z_{load}} 
   \end{equation} \label{4}$$.
This way, we get the reflection coefficient
$$\begin{equation}
   R = \dfrac{Z_{load}-Z_1}{Z_{load}+Z_1} 
   \end{equation} \label{5}$$

**Wait!** But why I always see the reflection coefficient with two different characteristic impedances? 
**The answer is,** to calculate the reflection coefficient based on characteristic impedance, it is assumed that $p_2^-=0$, indicating an infinite length of $M2$ with no reflection or right-going wave. This way the input impedance of $M2$ is simply its characteristic impedance $Z_2$. Then we get
$$\begin{equation}
   R = \dfrac{Z_2-Z_1}{Z_2+Z_1}
   \end{equation} \label{6}$$
