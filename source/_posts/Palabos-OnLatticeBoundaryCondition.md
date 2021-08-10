---
title: Palabos-OnLatticeBoundaryCondition
tags:
  - Palabos
  - Design Patterns
categories:
  - Palabos
mathjax: true
toc: true
date: 2021-05-01 15:56:19
---
The boundary conditions implemented in Palabos can be generally divided in two categories

1. `OnLatticeBoundaryCondition`, mainly implemented in **src/boundaryCondition/**

2. `OffLatticeModel`, mainly implemented in **src/offLattice/**

This article mainly focuses on the `OnLatticeBoundaryCondition`.

![Class Diagram](/images/Palabos-OnLatticeBoundaryCondition/OnLatticeBoundaryCondition.png)
<!--more-->

## Basic structure
- Here follows some key points of the structure:
  1. `OnLatticeBoundaryCondition2D` is the base class, and is the one that is "visible" to users. It provides the functions to be called directly by users like 
      - `setVelocityConditionOnBlockBoundaries()`
	  - `setPressureConditionOnBlockBoundaries()`
  2. The instantiator `BoundaryConditionInstantiator2D` inherits from `OnLatticeBoundaryCondition2D`
      - The instantiator to me is a glue that binds the implementation to the user interface.
      - The instantiator helps hide the detailed boundary implementation from the user. It provides specific boundary setup corresponding to different boundary positions in the domain.
	  - It integrates the boundary condition to the main simulation setup by setting a composite dynamics using `setCompositeDynamics()`, and may (not) integrate a boundary functional through `integrateProcessingFunctional()`
      - The instantiator `BoundaryConditionInstantiator2D` takes a **Boundary Manager** as one of its template parameters, and such a Boundary Manager is in charge of actual boundary operations.
  3. `creatXXXBoundaryCondition2D()` is a factory funtion that returns an instance of `BoundaryConditionInstantiator2D`. One may find examples stored in `/src/boundaryCondition/boundaryCondition2D` like
      - `createLocalBoundaryCondition2D()`
      - `createDynamicsBasedLocalBoundaryCondition2D()`
      - `createEquilibriumBoundaryCondition2D()`
      - `createInterpBoundaryCondition2D()`
	
	  or others like `createZouHeBoundaryCondition2D()` saved separately in `/src/boundaryCondition/zouHeBoundary2D.h`
  4. The **Boundary Manager** is the core of boundary condition implementation. 
      - The boundary instantiator makes use of the boundary manager by taking it as a template parameter.
      - There are two different ways of implementing the boundary condition:
	    - create a composite dynamics
	    - create a processor (boundary functional)
	  - The boundary condition normally has both a **dynamics** class (`XXXBoundaryDynamics`) and a **processor** class (`XXXBoundaryFunctional2D`)
	  
## Take `zouHeBoundary2D` as an example

1. The factory functions are in `/src/boundaryCondition/zouHeBoundary2D.h` named
   - `createZouHeBoundaryCondition2D()`
   - `createDynamicsBasedZouHeBoundaryCondition2D()`
2. Each factory function returns a instance of `BoundaryConditionInstantiator2D` with different *Boundary Managers*
   - `WrappedZouHeBoundaryManager2D`
   - `ZouHeBoundaryManager2D`
3. Each Boundary Manager has a series of functions named `getVelocityBoundaryDynamics()`, `getVelocityBoundaryFunctional()` and so on. Take the velocity boundary condition as an example, it returns (or not) either
   - `ZouHeVelocityDynamics`, or 
   - `WrappedLocalBoundaryFunctional2D`
4. No matter how, they all leads to the `ZouHeClosure` function saved in `/src/boundaryCondition/zouHeDynamics.hh`, where the core of the algorithm sits.
