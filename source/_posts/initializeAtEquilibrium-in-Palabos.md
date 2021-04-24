---
title: initializeAtEquilibrium() in Palabos
tags: [Palabos, C++]
categories: [Palabos]
mathjax: true
toc: true
date: 2021-04-22 20:32:01
---

I've discussed the structure of the data processor execution in a [previous article](https://swang251.github.io/2018/08/28/The-guide-for-the-Data-Processor-structure-of-Palabos/). Today let's take a look at a certain type of the data processors: **data initializer**.

<!--more-->
There are many data initializers implemented in `src/dataProcessors/dataInitializerWrapperXD.h/hh`. I'll take one of them, `initializeAtEquilibrium()`, as an example here.

## Overloads of `initializeAtEquilibrium()`
- Taking the 2D version as an example, there are four overloads that are categorized into two types.

  1. Two of them accept **constant** `density` and `velocity` and applied constants to all cells.
  ```c++
  template<typename T, template<class U> class Descriptor>
  void initializeAtEquilibrium(BlockLattice2D<T,Descriptor>& lattice, Box2D domain,T density, Array<T,2> velocity, T temperature = (T)1);

  template<typename T, template<class U> class Descriptor>
  void initializeAtEquilibrium(MultiBlockLattice2D<T,Descriptor>& lattice, Box2D domain, T density, Array<T,2> velocity, T temperature = (T)1);
  ``` 
     - It calls `applyProcessingFunctional()`
     - It is based on the functional `IniConstEquilibriumFunctional2D`
  
  2. Two of them accept a **function object** `RhoUFunction` and provides a cell-dependent initialization.
  ```c++
  template<typename T, template<class U> class Descriptor, class RhoUFunction>
  void initializeAtEquilibrium(BlockLattice2D<T,Descriptor>& lattice, Box2D domain, RhoUFunction f)

  template<typename T, template<class U> class Descriptor, class RhoUFunction>
  void initializeAtEquilibrium(MultiBlockLattice2D<T,Descriptor>& lattice, Box2D domain, RhoUFunction f)
  ```
     - It calls `applyIndexed()`, a wrapper of `applyProcessingFunctional()`
     - It is based on the functional `IniCustomEquilibriumFunctional2D`
- For each type, there are two versions, one for `MultiblockLattice2D` and one for `BlockLattice2D`.
- As I've discussed a lot about the general `applyProcessingFunctional` in the previous article, I will focus on the more interesting cell-dependent version initializer.

## Function Object
- For the cell-dependent version, it needs to initialize each cell of the domain with a cell (position)-dependent value. This is achieved by passing a function object `RhoUFunction` into the `initializeAtEquilibrium()` function.
``` c++
// This function is implemented in-place, because it cannot be precompiled due to its generic nature.
template<typename T, template<class U> class Descriptor, class RhoUFunction>
void initializeAtEquilibrium(MultiBlockLattice2D<T,Descriptor>& lattice, Box2D domain, RhoUFunction f)
```
- `RhoUFunction f` is an [function object](https://docs.microsoft.com/en-us/cpp/standard-library/function-objects-in-the-stl?view=msvc-160)
  - > A *function object*, or *functor*, is any type that implements operator(). This operator is referred to as the call operator or sometimes the application operator. The C++ Standard Library uses function objects primarily as sorting criteria for containers and in algorithms.
  - > Function objects provide two main advantages over a straight function call. The first is that a function object can contain state. The second is that a function object is a type and therefore can be used as a template parameter.
- As mentioned above, the function object can be used as a template parameter as it is shown in the above snippet.
- The `RhoUFunction` is a class member of the functional `IniCustomEquilibriumFunctional2D`, is called in side `functional->execute()`.
- A typical functor
```c++
/// A functional, used to create an initial condition for the density and velocity
template<typename T>
class PoiseuilleVelocityAndDensity {
public:
    void operator()(plint iX, plint iY, T& rho, Array<T,2>& u) const {
        // assign values to rho and u.
    }
};
```

## Cell-dependent functional
- `IniCustomEquilibriumFunctional2D` is 
  - declared in *src/dataProcessors/dataInitializerFunctional2D.h*
  - implemented in *src/dataProcessors/dataInitializerGenerics2D.h* (the file name sounds weird though, I guess "generic" means cell-dependent?)
- `IniCustomEquilibriumFunctional2D : OneCellIndexedFunctional2D`
- `OneCellIndexedFunctional2D` has the member function `execute(iX, iY, cell)` which is overridden in the subclass.
  - where: *src/dataProcessors/dataInitializerFunctional2D.h/hh*
- **`execute()` is the place to implement the algorithm**.


## `applyIndexed` a wrapper of `applyProcessingFunctional`
- `applyIndexed` is a wrapper of `applyProcessingFunctional`
- It builds a `GenericIndexedLatticeFunctional2D` that is inherited from  `BoxProcessingFunctional2D_L` 
- `GenericIndexedLatticeFunctional2D` includes the private class member `OneCellIndexedFunctional2D* f`, which is `IniCustomEquilibriumFunctional2D`
- The key idea of `GenericIndexedLatticeFunctional2D` is the overridden `process()` loops through the domain and call the `f->execute()` at each cell.
- where
  - `src/dataProcessors/dataInitializerWrappers2D.hh`

## More about the structure: three cell-related functionals
- One-cell functional
  1. `OneCellFunctional2D`
  2. `OneCellIndexedFunctional2D`
  3. `OneCellIndexedWithRandFunctional2D`
- Generic lattice functional, which takes one-cell functional as a private class member `f`. Such a functional overrides the `process()` so that execute `f->execute()` at each cell of the domain
  1. `GenericLatticeFunctional2D`
  2. `GenericIndexedLatticeFunctional2D`
  3. `GenericIndexedWithRandLatticeFunctional2D`
- Functional Wrapper, that calls `applyProcessingFunctional()` with the functional
  1. `apply()`
  2. `applyIndexed()`
     1. take `GenericIndexedLatticeFunctional2D`
     2. take `GenericIndexedWithRandLatticeFunctional2D`