---
title: The guide for the Data Processor structure of Palabos
date: 2018-08-28 23:49:02
tags: [Palabos, LBM, CFD]
categories: Palabos
toc: ture
---

In this article, the running and calling sequences of the data processors related functions is briefly summarized, based on the [official documentation](http://www.palabos.org/documentation/userguide/data-processors.html). Mainly six 'layers' are mentioned here.

### First, two kinds of data processors are used:
   - **applyProcessingFunctional**, the wrapper for `excuteDataProcessor`: is executed just once, on one or more blocks
   - **integrateProcessingFunctional**, the wrapper for `addInternalProcessor`:  is added to a block and is part of the block and can be executed as many times as wished, blabla. The added processors are implicitly (to the users) called by the function *executeInternalProcessors*


### Second
   - The function `integrateProcessingFunctional` and `applyProcessingFunctional` are defined and implemented in */src/multiBlock/multiDataProcessorWrapper2D.h/hh*.
   - The */src/atomicBlock/dataProcessorWrapperXD.h/hh* stores the atomic Block version.
   - The function `applyProcessingFunctional` has three main parameters: 1) `BoxProcessingFunctionalXD_LSTN functional`, 2) `BoxXD domain` and, 3) `MultiBlockLatticeXD lattice`;
   - The function `integrateProcessingFunctional` has an additional parameter: `plint level`;

### Third
   - `applyProcessingFunctional` calls `excuteDataProcessor(BoxProcessorGeneratorXD(functional, domain), lattice);`
   - `integrateProcessingFunctional` calls `addInternalProcessor(BoxProcessorGeneratorXD(functional, domain), lattice, level);`
   - So the `BoxProcessorGeneratorXD` has no difference for the two wrapper functions.
   
### Fourth
   - the `excuteDataProcessor` and `addInternalProcessor` are defined and implemented in */src/multiBlock/multiBlockOperationsXD.h/.cpp*
   - Both functions has the parameter `DataProcessorGeneratorXD const& generator`
   - one of the overriden of the functions is the kernel one.
   - The kernel  `excuteDataProcessor`  and `addInternalProcessor` finally calls the corresponding atomicBlock versions which is defined and implemented in */src/atomicBlock/atomicBlockOperationsXD.h/.cpp*

### Fifth, in the atomicBlock versions
   - */src/atomicBlock/atomicBlockOperationsXD.h/.cpp*
   - the kernel `excuteDataProcessor` calls the `processor -> process()` where `processor` is a `DataProcessorXD` defined in */src/atomicBlock/dataProcessingFunctionalXD.h/.cpp*
   - the kernel `addInternalProcessor` calls the `actor.integrateDataProcessor`, where the `actor` is an `AtomicBlockXD` written in */src/atomicBlock/atomicBlockXD.h/.cpp*, inside which the `integrateDataProcessor` runs `processors[level].push_back(processor)`;

### Sixth
   - `DataProcessorXD`  <== `BoxProcessorXD` who overrides the function `process()` runing `functional -> processGenericBlock(domain, atomicBlocks)` where `BoxProcessingFunctionalXD* functional` is written in the file */src/atomicBlock/dataProcessingFunctionalXD.cpp*
   - **BoxProcessingFunctionalXD** is a base class defined in the same file which **has many subclasses for different purposes**.
   - The `processGenericBlock` calls the `process` function in the tons of subclasses functionals of the class `BoxProcessingFunctionalXD`, like `NTensorFieldBoxProcessingFunctional3D` or `BoxProcessingFunctionalXD_LL`
   - The `process()` would be finally overriden by the subclasses of `BoxProcessingFunctionalXD_LL` or so, and implemented. likely in `class TurbulentLatticeToPassiveAdvDiff3X : public BoxProcessingFunctionalXD_LL` in */src/multiPhysics/advectionDiffusion3D.h/.hh*
   - `SpecialFunctional` ==> `BoxProcessingFunctionalXD_LL` etc.  ==> `BoxProcessingFunctionalXD`

### In addition, about `excuteInternalProcessors()`
   - It is called in 1) `MultiBlockLatticeXD::stream()`, 2) `MultiBlockLatticeXD::collideAndStream()` and 3) `MultiBlockXD::initialize()`
   - The `MultiBlockXD::executeInternalProcessors(level)` calls the `getComponent(blockId).excuteInternalProcessors(leve)` which is at the atomicBlocks unit. (line511@*/arc/multiBlock/multiBlock3D.cpp*)
   - The `AtomicBlockXD::executeInternalProcessors(level, processors)` finally calls the processors -> process(); in (line254@*/src/atomicBlock/atomicBlock3D.cpp*)
   

### An example
*/examples/showCases/boussinesqThermal2d/rayleighBenard2D.cpp*

- line 171:

```
applyProcessingFunctional (
            new IniTemperatureRayleighBenardProcessor2D<T,NSDESCRIPTOR,ADESCRIPTOR>(parameters), 
            adLattice.getBoundingBox(),  adLattice );
```

where the `Struct IniTemperatureRayleighBenardProcessor2D : public BoxProcessingFunctional2D_L<T,adDescriptor>` is a functional

- line 293: 

```
integrateProcessingFunctional (new BoussinesqThermalProcessor2D<>(), nslattice.getBoundingBox(), nslattice, adLattice, processorlevel );
```
where the `class BoussinesqThermalProcessor2D : BoxProcessingFunctional2D_LL` is a functional defined and implemented in */src/multiPhysics/boussinesqThermalProcessor2D.h/.hh*.



**NOTA:** the code used here is Palabos version 2.0






