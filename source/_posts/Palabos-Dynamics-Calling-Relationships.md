---
title: Palabos Dynamics Calling Relationships
date: 2018-09-10 15:59:43
tags: [Palabos, LBM, CFD]
categories: Palabos
toc: ture
---

In this article, the calling relationship of dynamics would be shown which helps write your own dynamic classes. The dynamics classes are mainly written in */src/basicDynamics/* and */src/complexDynamics/*. Here we will take `BGKdynamics` and `MRTdynamics` as examples for illustration.

### BGKdynamics
- The calling graph: `BGKdynamics::collide()` <-- `dynamicsTemplates::bgk_ma2_collision()` <-- `dynamicsTemplatesImpl::bgk_ma2_collision()`.
- The declaration and implementation of functions in class `BGKdynamics` are in *src/basicDynamics/isoThermalDynamics.h* and *../isoThermalDynamics.hh*, respectively.
- The structs `dynamicsTemplates` and `dynamicsTemplatesImpl` and the two member functions with the same name `bgk_ma2_collision()` are written in *src/latticeBoltzmann/dynamicsTemplates.h*

### MRTdynamics
- The calling graph: `MRTdynamics::collide()` <-- `mrtTemplates::mrtCollision()` <-- `mrtTemplatesImpl::mrtCollision()`.
- The declaration and implementation of functions in class `MRTdynamics` are in *src/complexDynamics/mrtDynamics.h* and *../mrtDynamics.hh*, respectively.
- The structs `mrtTemplates` and `mrtTemplatesImpl` and the two member functions with the same name `mrtCollision()` are written in *src/latticeBoltzmann/mrtTemplates.h*

### Conclusion
- The kernal function is the `XXXdynamics::collide()` which implements the collision step.
- The `collide()` would call different computations from different `Templates` like `dynamicsTemplates`, `mrtTemplates`, `momentTemplates` and so on.
- The `collide()` is implemented on `cell` level. So for non-local dynamics, a superclass `class NonLocalDynamics2D : public CompositeDynamics<T,Descriptor>` might be used.

To better understand the calling relations, one could use [Doxygen+GraphViz](https://romanegloo.wordpress.com/2012/03/29/generating-a-callgraph-by-using-doxygen-and-graphviz-13/) to plot the call graph or get use of the structure or call graph/hierachy function within IDE.
