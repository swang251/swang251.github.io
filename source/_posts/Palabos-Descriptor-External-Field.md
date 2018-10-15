---
title: Descriptor and External Field of Palabos
date: 2018-10-15 15:29:31
tags: [Palabos, LBM, CFD]
categories: Palabos
mathjax: true
toc: true
---


For the lattice Boltzmann method, the descriptor has to be defined in advance. Here we briefly discuss the descriptor structure in Palabos. 

<!--more--> 

## Descriptor
In palabos, the descriptors are stored in `/src/latticeBoltzmann/nearestNeighborLatticesXD.h`, where $X=2,3$.

Each descriptor is a **combination** of the lattice schema and the external field, so that must inherit from at least two *`DescriptorBase`* including the basic  *`DdQqDescriptorBase`* defining the lattice-related variables, and a *`EXTERNALVARLISTDescriptorBase`* with external variables or `NoExternalFieldBase` if the problem involves no external variables. (*`DdQqDescriptorBase`* could be `D2Q9DescriptorBase`, and *`EXTERNALVARLISTDescriptorBase`* could be `RhoBarVelocityPiNeqOmegaDescriptorBase2D`).

- In *`DdQqDescriptorBase`*, it defines the `d`, the `q`, the lattice velocity `c[q][d]`, lattice weight `t[q]`, square speed of sound `cs2` and so on by means of `DdQqConstants`. 

- The *`EXTERNALVARLISTDescriptorBaseXD`* is written in `/src/latticeBoltzmann/externalFields.h`. In *`EXTERNALVARLISTDescriptorBaseXD`*, it defines the problem-specific `ExternalField` as `EXTERNALVARLISTDescriptorXD`. Here the `DdQq` of `EXTERNALVARLISTDdQqDescriptor` must correspond to the one in `DdQqDescriptorBase`. Here above `EXTERNALVARLIST-` represents the name list of the external variables, e.g., `EXTERNALVARLIST=RhoBarVelocityPiNeqOmega` and `EXTERNALVARLIST=ForcedRhoBarJ` for `RhoBarVelocityPiNeqOmegaD2Q9Descriptor` and `ForcedRhoBarJD2Q9Descriptor`, respectively.

## Example
- Take the `RhoBarVelocityPiNeqOmegaD2Q9Descriptor` as an example to illustrate the structure, it inherits from `D2Q9DescriptorBase` and `RhoBarVelocityPiNeqOmegaDescriptorBase2D`. 
```
template <typename T> struct RhoBarVelocityPiNeqOmegaD2Q9Descriptor
   : public D2Q9DescriptorBase<T>, 
     public RhoBarVelocityPiNeqOmegaDescriptorBase2D
{
    static const char name[];
};
```
### DdQqDescriptorBase
- The `D2Q9DescriptorBase` is defined as 
```
template <typename T> struct D2Q9DescriptorBase
    : public D2Q9Constants<T>, public DefaultRoundOffPolicy<T>
{
    typedef D2Q9DescriptorBase<T> BaseDescriptor;
    enum { numPop=D2Q9Constants<T>::q };
};
```
- where the lattce-related variables are defined in 
```
template <typename T> struct D2Q9Constants
{
    enum { d = 2, q = 9 };        ///< number of dimensions/distr. functions
    static const T invD;          ///< 1 / (number of dimensions)
    static const int vicinity;    ///< size of neighborhood
    static const int c[q][d];     ///< lattice directions
    static const int cNormSqr[q]; ///< norm-square of the vector c
    static const T t[q];          ///< lattice weights
    static const T cs2;           ///< lattice constant cs2 (in BGK, this is the square-speed-of-sound)
    static const T invCs2;        ///< 1 / cs2
    };
	```
### EXTERNALVARLISTDescriptorBaseXD
- The `RhoBarVelocityPiNeqOmegaDescriptorBase2D` has a component `ExternalField`
```
struct RhoBarVelocityPiNeqOmegaDescriptorBase2D {
    typedef RhoBarVelocityPiNeqOmegaDescriptor2D ExternalField;
};
```
- and the `RhoBarVelocityPiNeqOmegaDescriptor2D` would store
 - the number of scalars,
 - the number of the species,
 - the index each variable starts,
 - the size of each variable (2 for 2d and 3 for 3d tensors),
```
struct RhoBarVelocityPiNeqOmegaDescriptor2D {
    static const int numScalars       = 7;
    static const int numSpecies       = 4;
    static const int rhoBarBeginsAt   = 0;
    static const int sizeOfRhoBar     = 1;
    static const int velocityBeginsAt = 1; 
    static const int sizeOfVelocity   = 2;
    static const int piNeqBeginsAt    = 3;
    static const int sizeOfPiNeq      = 3;
    static const int omegaBeginsAt    = 6;
    static const int sizeOfOmega      = 1;
    static const int sizeOfForce      = 0;
};
```

- meaning `ForcedRhoBarJdescriptor3DRhoBarVelocityPiNeqOmegaDescriptor2D` have 4 species including `rhoBar`, `velocity`, `piNeq` and `omega`, with 1, 2, 3 and 1 as the sizes, respectively. So the scalar number would be $1+2+3+1=7$ in total.

## Setting up the external field
Once the descriptor with an external field is defined, the memory of `external` inside the `cell` is allocated (see `src/core/cell.h`). For initializing or simply setting values to the external field, one would use the data processor, i.e., `setExternalVector` or `setExternalScalar` with the variable start index like `DESCRIPTOR<T>::ExternalField::rhoBarBeginsAt`.

- An example of external force flow would be found in the project `/examples/showCases/womersley/`. Where the external forces is set by an array, i.e., the force is uniformally deployed in the domain.
```
Array<T,NSDESCRIPTOR<T>::d> force(womersleyForce((T)0, amplitude, frequency, parameters),0.);
setExternalVector(lattice,lattice.getBoundingBox(),NSDESCRIPTOR<T>::ExternalField::forceBeginsAt,force); 
```

- For position-dependent external variables, one could use a `MultiScalarFieldXD` or `MultiTensorFieldXD`, initialized from a functional, as the input of `setExternalVector` or `setExternalScalar` and use a functional to initialize the `MultiXXXXFieldXD`. For the setup of the absorbing layers, I use
```
MultiScalarField2D<T> sigma(lattice);
WaveAbsorptionSigmaFunction2D<T> sigmaFunction2D(lattice.getBoundingBox(), numSpongeCells ,bulkValue);
setToFunction(sigma, lattice.getBoundingBox(), sigmaFunction2D);
setExternalScalar(lattice, lattice.getBoundingBox(),
                      DESCRIPTOR<T>::ExternalField::sigmaBeginsAt, sigma );
					  ```
