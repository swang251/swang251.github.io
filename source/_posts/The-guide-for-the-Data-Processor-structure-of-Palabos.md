---
title: The guide for the Data Processor structure of Palabos
date: 2018-08-28 23:49:02
tags: [Palabos, LBM, CFD]
categories: Palabos
toc: true
---
In this article, the execution of data processors and the related functions are briefly summarized, based on the [official documentation](https://palabos.unige.ch/get-started/palabos-documentation/). 

<!--more-->

### First, two data processor wrappers, the function can be called directly by the end users
   - Two Data Processor Wrappers
     - **`applyProcessingFunctional()`**, 
       - the wrapper of `executeDataProcessor()`
       - executed just once, on one or more blocks
     - **`integrateProcessingFunctional()`**,
       - the wrapper of `addInternalProcessor()`
       - added data processors to a block, which becomes part of the block and can be executed as many times as wished. The added processors are implicitly (to the users) called by the function *`executeInternalProcessors`*
   - They accept three main parameters:
     1. `BoxProcessingFunctionalXD_LSTN functional`
     2. `BoxXD domain` 
     3. `MultiBlockLatticeXD lattice`;
     4. A `integrateProcessingFunctional` accepts an additional parameter: `plint level`;
   - *They are based on the **functional**, which defines the operation of the data processor.*
   - where in library
     - multiBlock version */src/multiBlock/multiDataProcessorWrapperXD.h/hh/cpp*.
     - atomicBlock version */src/atomicBlock/dataProcessorWrapperXD.h/hh*.   

### Second, two multi block data processor operators
   - Two operators
     - `excuteDataProcessor()`
     - `addInternalProcessor()`
   - The *functional* is wrapped into a `DataProcessorGeneratorXD` and passed to either the `executeDataProcessor()` or `addInternalProcessor()`
     - The `DataProcessorGeneratorXD` stores a pointer to the `functional` as a private member.
   - The main job is to deal with the multi-block structure and pass the functional into the *atomic block operators*
   - where in library
      - operators: */src/multiBlock/multiBlockOperationsXD.h/cpp*.
      - Data processor generators: */src/atomicBlock/dataProcessingFunctionalXD.h/hh/cpp*.
      - Data processor generator base struct: */src/atomicBlock/dataProcessorXD.h/hh/cpp*.
     
### Third, two atomic block data processor operators
   - The `DataProcessorGeneratorXD generator` is passed from the multi-block operators.
   - The `generator` generates a `processor`: `generator.gererates(objects)` with the `functional` embeded.
   - Two operators
     - `excuteDataProcessor`
       - The processor is finally processed `processor-process()`
     - `addInternalProcessor`
       - The processor is integrated using the function `integrateDataProcessor()` and the processor is pushed to the `vector<processor> processors` in each atomic block through `processors[level].push_back(processor)`;
   - Folders
     -  Operators: */src/atomicBlock/atomicBlockOperationsXD.h/.cpp*
     -  Data Processors: */src/atomicBlock/dataProcessingFunctionalXD.h/.cpp*
     -  Data Processor Base struct: */src/atomicBlock/dataProcessorXD.h/.cpp*

### As a summary
   - The `functional` is the key, where the main algorithm is implemented. 
   - It is first passed to the `applyProcessingFunctional()` as an argument, inside which, it is cloned to the newed `DataProcessorGenerator` that is passed to the `executeDataProcessor()`. 
   - It goes into the atomic version operator and finally cloned in to the `processor` generated from the `generator`.
   - The `processor->process()`  finally calls the `functional->process()`.
   
### In addition: `BoxProcessingFunctionalXD`
   - `BoxProcessingFunctionalXD` has the algorithm implemented in `processGenericBlock()` instead of `process()`
     - `BoxProcessingFunctionalXD` is a base class defined in the same file as many of its subclasses.
   - `BoxProcessorXD :: DataProcessorXD` is designed for `BoxProcessingFunctionalXD`,which overrides the function `process()` 
     - `process()`runs `functional -> processGenericBlock(domain, atomicBlocks)`
   - Inheritance: `ACertainFunctional` ==> `BoxProcessingFunctionalXD_LL` etc.  ==> `BoxProcessingFunctionalXD`
     - *src/atomicBlock/dataProcessingFunctionalXD.h*
   
### In addition: `excuteInternalProcessors()`
   - It is called in 
     1. `MultiBlockLatticeXD::stream()`, 
	  2. `MultiBlockLatticeXD::collideAndStream()` 
	  3. `MultiBlockXD::initialize()`
   - The `MultiBlockXD::executeInternalProcessors(level)` calls the `getComponent(blockId).excuteInternalProcessors(leve)` which is at the atomicBlocks unit. (line511@*/src/multiBlock/multiBlock3D.cpp*)
   - The `AtomicBlockXD::executeInternalProcessors(level, processors)` finally calls the processors -> process(); in (line254@*/src/atomicBlock/atomicBlock3D.cpp*)

----------
There is more to be discussed about the design for sure.





