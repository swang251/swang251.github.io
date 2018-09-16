---
title: Selective Filter 2D - Palabos
date: 2018-09-15 23:36:17
tags: [Palabos, LBM, CFD]
categories: Palabos
mathjax: true
mathjax2: true
---

I just implemented the 2D selective filter<sup>1</sup> in Palabos. Because of the non-local calculation when filtering the collision operator, it takes Miguel and me some time to think about a way to implement it in Palabos. 

- We first thought about the `integrateProcessingFunctional` but it might only do the post-collision operation (though we could apply a -1 `level` and call `executeInternalProcessors(-1)` manually). 

- Then Miguel found the *DynamicProcessor* could be a candidate,something in *src/basicDynamics/dynamicsProcessorXD.hh* where there is `ExternalRhoJcollideAndStream2D` for external macroscopic variable cases (*examples/codesByTopic/externalMacroscopicVariables*). 

- I then found the `nonLocalDynamicsXD` written in *src/core/nonLocalDynamicsXD.h/hh*. This doesn't seems to be complete and neither is there a show case. However, you can find something related in `ExecuteNonLocalDynamics3D`, a functional inherited from `BoxProcessingFunctional3D_L` in *src/boundaryCondition/NLD_boundaries3D.h/hh*. 

I finally decide to go to the last direction because I consider `nonLocalDynamicsXD` as a good interface to start with. So, the basic idea here is to keep every variables and function of the dynamics in the `dynamics` class and create each member function a functional for data processor. Likely, I write `SelectiveFilterBGKDynamics2D.nonLocalAction()` and `SelectiveFilterBGKDynamics2D.prepareFNeq()` and two functional inherited from `BoxProcessingFunctional2D_L`. In addition, the dynamics class has two private members for the original and the filtered $f_{neq}$. `applyProcessingFunctional` would be used in the main function.

One important thing I found when writing a new dynamics is about the `serialize` and `unserialize`. I do need write `serializer.addValues()` and `unserializer.readValues()` for each member variables or there would be a problem. I don't get it totally understand it but hopefully, [this article](https://isocpp.org/wiki/faq/serialization) would help, and I will be back with the answer soon.







1. Ricot, Denis, Simon Marié, Pierre Sagaut, and Christophe Bailly. 2009. “Lattice Boltzmann Method with Selective Viscosity Filter.” Journal of Computational Physics 228 (12): 4478–4490.

