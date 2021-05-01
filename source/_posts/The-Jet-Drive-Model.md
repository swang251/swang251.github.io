---
title: The Jet-Drive Model
mathjax: true
toc: true
date: 2020-09-30 18:20:20
tags: [Acoustics, Musical Acoustics, Wind Instrument, Flute]
categories: [Acoustics]
---

Modeling the flute exitation is complex. There exiting two main models, i.e., *the jet-drive model* and *the discrete vortex model*. Let's talk about the jet-drive model for now.

<!--more-->

## General Sound Generation Mechanisms
The earliest attemps to study the flute-like instrument sound generation trace back to the work by Helmholtz (1877) and Rayleigh (1877), in their own celebrated books. The details within the instrument is more and more revealed recently thanks to the study by different researchers, like A. Hirschberg, B. Fabre, M. P. Verge, to name a few, even though there are still many puzzles left to be solved.

In general, the air blown out of the player's mouth passes through a flue channel, either a flue canal of a recorder or the one constrained by the player's lip, and forms a jet. The jet starts to oscillate with transverse perturbations contributed either by the acoustic field feed-back, the jet's intrinsic instability or the hydrodynamic direct feedback from the labium. Such an oscillation or perturbation will evolve and grow while convected by the jet from the flue channel exit toward the labium (a sharp edge). The jet will then hit the labium and apply a force on it, and the reacting force from the labium to the fluid acts as the acoustic source that sustains the acoustic oscillation inside the flute.


## The Flute Model
Based on the sound generation mechanisms, there are several key components need to be modeled and the most popular and easiest way to do that is modeling each component separately and lump them together. Such a lumped model is widely applied in different studies as well as synthesis, even though questioned by some researchers (Fabre et al. 2000).

Here is a list of the components to be modeled:

- Jet formation
- Jet receptivity
- Jet instability
- Sound source
- Vortices
- Turbulence


## The Jet Formation
- The flow passes from the player's mouth or the organ's foot through the lip or flue channel. A jet is formed when the flow comes out of the channel.
- The jet speed is determined by the pressure difference $\Delta p_{jet} = p_f - p_w$ across the flue channel and its profile depends on the geometry of the channel, where $p_m$ is the foot pressure and $p_w$ is the pressure at the window. 
- Sometimes people call $p_f$ the cavity pressure $p_c$ and $p_w$ can be called as mouth pressure $p_m$ (the mouth represents the window of the instrument instead of the player's mouth).
- unsteady Bernoulli equation
  $$\rho_0 l_c \dfrac{dU_j}{dt} + \dfrac{1}{2}\rho_0U_j^2 = p_f - p_w$$
- The jet flow is a function of $y$, written as $U(y)$.
- The volume flow rate is noted as $Q_j$
- Part of the air will goes into the instrument $Q_{in}$ and the rest goes out $Q_{out}$.
  - The $Q_{in}$ sees the impedance (or admittance) of the pipe $Z_p$
  - The $Q_{out}$ sees the window impedance $Z_w$ which includes the radiation impedance as well as the end correction near the window.
  
## The Jet Profile
- THE PROFILE OF the jet $U(y)$ depends on the upstream setup as well as the geometry of the channel. The most popular velocity profile is the Bickley velocity profile, defined as 
  $$U(y) = U_0\, \text{sech} ^2 (y/b)$$
  - where half width of the profile $b = 2h/5$ is a Poseuille flow is assumed at the flue exit and $h$ is the flue channel height, and $U_0\sim U_j$ is the centerline velocity that is assimilated to the jet velocity $U_j$.

## The Jet Oscillation
- The jet starts to oscillate due to the disturbation by the acoustic transverse velocity as a result of the acoustic feedback.
- The jet receptivity:
- The receptivity is modeled by a parameter $\eta(t)$ defined as the jet lateral displacement when the jet arrives at the labium.
- The contribution to $\eta$ mainly comes from the acoustic perturbation and the hydrodynamic feedback (Verge (1997)). Fletcher proposed a model to describe the receptivity and instability as 
  $$\eta = \dfrac{V_{ac}}{i\omega}(1-\cosh(\mu x))e^{-i\omega(t-x/c_p)}$$
  which is then modified by Verge
  $$\eta = \dfrac{V_{ac}}{i\omega}(1-\cosh(\alpha W))e^{-i\omega W/u}$$
  where $\mu$ and $u$ is a function of the Strouhal number (Verge et al. 1997)
- A simpler model is proposed by de la Cuadra in his thesis (2006)
  $$\eta(t,x) = e^{\alpha_i x}\eta_0(t-x/c_p)$$
  with 
  $$\dfrac{\eta_0}{h} = \dfrac{v_{ac}(t)}{U_j}$$
  - $\alpha_i = \beta/h$: the empirical coefficient corresponding to the jet amplification
  - $c_p = \gamma U_j$: the empirical coefficient corresponding to the phase velocity of a perturbation along the jet.
  - $\beta \sim 0.5$: jet spatial amplification
  - $\gamma \sim 0.4$: the relative convection velocity


## The Jet-Drive Model
- Coltman (1968, 1976) is the first one who proposed the jet drive model. 
- The fluctuating part of the inward and outward flow $Q_{in}'$ and $Q_{out}'$ are complementary to each other ($Q_{in}' = -Q_{out}'$). (They are more commonly noted as $Q_1$ and $Q_2$).
- Assuming the air to be incompressible in between the two flow injection points of $Q_{in}'$ and $Q_{out}'$, and apply the third Newton's law to the air mass, we get
  $$\Delta p = -\dfrac{\rho \delta_d}{S_w}\dfrac{dQ_{in}'}{dt} = -\dfrac{\rho \delta_d}{S_w}\dfrac{dQ_{in}}{dt}$$
  - $S_w$ is the window area
  - $\delta_d$ is the effective acoustical "distance" between the two sources, calculated as $\delta_d = 4\pi\sqrt{2hW}$ as proposed by Verge (1994), where $h$ is the distance from the source to the tip of the labium.
- $Q_{in}$ depends on the jet profile as well as the jet lateral displacement $\eta(t)$
  $$\displaystyle Q_{in}(t) = H_m\int_{-\infty}^{y_{off}-\eta(t)}U(y)dy$$
  - where $y_{off}$ is the offset between the channel exit and the labium tip in $y$ axis
  - $H_w$ the window width

## The Jet-Resonator Interaction
This might be the trickest part of the model and its slightly different from paper to paper.

- In general, the jet-resonator interaction is based on the $\Delta p$ from the jet-drive model and the admittance $Y$ of the resonator, while $Y$ includes the pipe admittance as well as the end correction around the embouchure.

- In Auvray (2012, 2014)'s papers,
  - $\Delta p = p^+ - p^-$ where $p^+$ and $p^-$ corresponds to the pressure at the inward and outward sides of the source, and they share the same (acoustic) velocity $v_{ac}$.
  - $Y = v_{ac} / \Delta p$
  - It is not clear about the definition of $v_{ac}$ in this paper as it is also used as the transverse velocity to calculate the $\eta_0$. But it seems like they are the same thing in Auvray's paper (2012) which is a little difficult to understand.
  - In de La Cuadra's thesis, v_{ac} is simply the acoustic velocity at the entrance of the pipe, corresponding to $Q_p/S$ in Verge's paper.
- In Verge (1997)'s papers,
  - $P_p$ and $P_m$ might correspond to $p^+$ and $p^-$ in Auvray's papeers, are the pressure at the entrance of the pipe and the pressure at the mouth/exit of the flue channel, respectively.
  - The pressure relationship is built as
  $$p_p - p_m = -\dfrac{\rho_0\delta_{in}}{S_m}\dfrac{dQ_{in}}{dt} + \Delta p$$
  - $\Delta p = p_p - p_m + \dfrac{\rho_0\delta_{in}}{S_m}\dfrac{dQ_{in}}{dt} \neq p_p - p_m$
  - $Q_p(0) = Q_{in}(0)$
  - $Q_{in}$ flow entering the $\delta_{in}$ part of the mouth end correction, $Q_{1}$ flow entering the pipe at the labium.
  - It should be safe to announce $Q_p = Q_{in} = Q_1$ based on the mass conservation.
  - $v_{ac}$, the transverse acoustic velocity is defined as $v_m'$ in Verge's paper 
  $$v_m' = \dfrac{2}{\pi}\dfrac{Q_p}{S_m} - \dfrac{0.38Q_1'}{S_m},$$
  where $Q_1' = Q_1 - \frac{1}{2}bHU_0$


## The Jet-Related Sound Source

- 
