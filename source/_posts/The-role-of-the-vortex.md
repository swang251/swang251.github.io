---
title: The role of the vortex - sound generative or dissipative?
mathjax: true
toc: true
date: 2020-09-22 20:20:48
tags: [Acoustics, Aero-acoustics]
categories: Acoustics
---

We know that the vortex is generative based on the vortex sound theory. We also know that the vortex is dissipative at the end of the orifice. Is the vortex acoustic generative or dissipative?

<!--more-->

## Generative Vortices
Let's start with the role of the vorticity in generating the sound.

- The vortex sound equation:
$$\begin{equation}
  \left(\dfrac{D}{Dt}\left(\dfrac{1}{c^2}\dfrac{D}{Dt} \right) - \dfrac{1}{\rho}\nabla\cdot(\rho\nabla) \right)B = \dfrac{1}{\rho}\nabla\cdot(\rho\boldsymbol{\omega}\times \boldsymbol{v})
\end{equation}$$
  - > Lighthill's equation can be recast in a form that emphasizes the prominent role of vorticity in the production of sound by taking the **total enthalpy** as the independent acoustic variable, in place of Lighthill's $c_0^2(\rho-\rho_0)$ -- *Howe, M. (Theory of Vortex Sound)*
  - [Enthalpy](https://en.wikipedia.org/wiki/Enthalpy): "is defined as the sum of the system's internal energy and the product of its pressure and volume. The pressure-volume term expresses the work required to establish the system's physical dimensions, i.e. to make room for it by displacing its environment." *Enthalpy = internal energy + work required to establish the system's physical dimensions.*
  - [Total Enthalpy](https://en.wikipedia.org/wiki/Stagnation_enthalpy): $\displaystyle B = \int\dfrac{dp}{\rho} + \dfrac{1}{2}v^2$
  - It is IMPORTANT to notice the following things:
    1. Originally proposed by Powell, the vortex sound equation is a reformation of the Lighthill's equation, which means it is applied to the **unbounded homentropic flow**.
	2. It is based on the **low Mach number approximation**
	3. The term $\nabla\cdot(\rho_0\boldsymbol{\omega}\times \boldsymbol{v})$ is the **dominant component of the Lighthill quadrupole** $\dfrac{\partial^2(\rho v_iv_j)}{\partial x_i\partial x_j}$


By the way,

- The equations in the wave equation format, i.e., Lighthill's equation and the vortex sound is derived by combining the continuity equation and the momentum equation.
- Crocc's equation is simply the **Crocco's form** of the **momentum equation** with the emphasis on the vorticity.

## Dissipative Vortices
Now, let's see why the vortices are acoustical dissipative as well. 

In general, it is because

> acoustic energy is expended in the generation of vorticity at an edge or corner, and the mean flow convects away the vorticity into regions where it can no longer continue to interact significantly with the acoustic field, and where its kinetic energy is ultimately dissipated as heat.

- Based on Howe, M. (1980), the absorbed acoustic energy is written as 
$$\begin{equation}
\displaystyle\pi_T = \int\rho_0\boldsymbol{\omega}\times\boldsymbol{u'} \text{d}^3\boldsymbol{x} = -\int\varepsilon_{ij}\rho_0v_iv_j \text{d}^3\boldsymbol{x}
\end{equation}$$
   - where $\boldsymbol{u'}$ is the *acoustic* particle velocity, $\boldsymbol{v}$ is the velocity and $\varepsilon_{ij}$ is the *acoustic* rate of the strain tensor

As you might have noticed, the term (1) $\rho_0\boldsymbol{\omega}\times\boldsymbol{u'}$ resembles the term $\rho_0\boldsymbol{\omega}\times\boldsymbol{v}$ in the vortex sound equation, only by replacing $\boldsymbol{v}$ with the acoustic counterpart $\boldsymbol{u}'$. The term (2) $\varepsilon_{ij}\rho_0v_iv_j$ is also simply the product of the low Mach number Lighthill stress tensor $\rho_0v_iv_j$ and the acoustic rate of the strain tensor. 

For both term (1) and (2), their counterparts in the generative case correspond to source term or RHS of the vortex sound equation and the Lighthill's equation, which describe the energy transfering from the fludic field to the acoustic field. Instead, term (1) and (2) is the other way round, the energy goes from the acoustic field to the fluidic field, or in other words, the acoustic energy is dissipated.

Actually, there is another way to understand quickly the dissipative characteristic of the vortex.

The velocity is related to the scalar potention $\phi$ and the stream function $\boldsymbol{A}$
$$
\begin{equation}
\boldsymbol{v} = \nabla\phi + \nabla\times\boldsymbol{A}
\end{equation}
$$
where $\nabla\phi = \boldsymbol{u}$ is the irrotational field and the $\nabla\times\boldsymbol{A}$ is the solenoidal field.

The acoustic field is irrotational as $u' = \nabla\phi'$. The vorticity field is solenoidal as $\boldsymbol{\omega} = \nabla\times \boldsymbol{v} =\nabla\times \nabla\times \boldsymbol{v}$, since $\nabla(\nabla\times f) = \nabla\times(\nabla f) = 0$.

When the kinetic energy is conserved, it simply flows from $\nabla\times\boldsymbol{A}$ (solenoidal/vorticity) to the $\nabla\phi$ (irrotational/acoustic) when the sound is generated and the other way round when the sound is dissipated.



## Reference
- [1] Howe, M. S., 2003, Theory of Vortex Sound, Cambridge University Press.
- [2] Howe, M. S., 1980, “The Dissipation of Sound at an Edge,” Journal of Sound and Vibration, 70(3), pp. 407–411.
- [3] Hirschberg, A., and Rienstra, S. W., 2004, “An Introduction to Aeroacoustics,” Eindhoven university of technology.
- [4] Kühnelt, H., 2016, “Studying the Vortex Sound of Recorder- and Flute-like Instruments by Means of the Lattice Boltzmann Method and Helmholtz Decomposition,” University of Music and Performing Arts Vienna.



