---
title: Palabos Immersed Boundary-Lattice Boltzmann Method
mathjax: true
toc: true
date: 2019-06-12 10:31:43
tags: [Palabos, LBM, CFD]
categories: Palabos
---
The immersed boundary method (IBM) is proposed by Peskin in 1972 in his Ph.D. thesis and then is widely used for complex boundaries and moving boundary problems. IBM is applied in the context of lattice Boltzmann method (LBM) for the first time in 2004 by Feng and Michaelides (Feng and Michaelides, J. Comput. Phys, 2004). People also call such combination immersed boundary-lattice Boltzmann method (IB-LBM). In Palabos, different off-lattice methods have been implemented, including the Filippo-Hanel method, the Guo-Zheng-Shi method, the Bouzidi method and also the IBM. 

<!--more-->

In Palabos, there is a demo showing how to use the IBM to solve the moving wall problems (*example/showCases/movingWall*). As one can notice, in Palabosv2.0r0, only 3D IBM is implemented and the corresponding implementaions can be found in 

- *src/offLattice/immersedWalls3D.h*
- *src/offLattice/immersedWalls3D.hh*

Here I will discuss only how the method used in the showCase works.

In the moving wall case, the multi direct-forcing IB-LBM proposed by Inamuro (2012) is used. Two main function are used:

- `instantiateImmersedWallData(vertices, areas, container)` for the wall boundary instantiation,
- `inamuroIteration(parameters)` for the main IBM iteration.

### InstantiateImmersedWallData
`instantiateImmersedWallData` is a function wrapper for the functional `instantiateImmersedWallData3D` where the boundary data is stored in a container block called `ImmersedWallData3D`.

### InamuroIteration
`inamuroIteration` is a function wrapper for the functional `InamuroIteration3D` which implements the IB-LBM algorithm following Inamuro (2012). In Inamuro's paper, there are 5 steps (from Step 0-5) in the iterative procedure and it iterate from Step 1 to Step 4. In Palabos, the iteration is implemented with a slighly different procedure.

- `for (neighboring) {averageJ += W*nextJ;}` corresponds to Eq 2.22 (*Step -1*) and Eq. 2.28 (*Step 3.*) and the $\mathbf{j}_l(\mathbf{X}_k)$ is calculated instead of $\mathbf{u}_l(\mathbf{X}_k)$;
- `for (vertices) {deltaG[i] = area[i]*(wallVelocity-averageJ);}` calculates the $g_l(\mathbf{X}_k)$ in *Step 0* and the last term of the RHS in Eq. 2.29, *Step 4*;
- `for (vertices) {g[i] += deltaG[i];}` (incompressible model), does the Eq. 2.29 in *Step. 4*;
- `for (neighboring) {nextJ += tau*W*deltaG[i];}` corresponds to *Step 1* and *Step 2* for spreading the force for correct the velocity at the Eulerian grid points. We can take it as substituting $\mathbf{g}_l(\mathbf{x})$ in Eq. 2.27 by Eq. 2.26.

In the main function in *movingWall.cpp*, the iteration time depends on `param.ibIter`.

#### N.B.
- The loop for neighboring starts range from -1 to 2. This is because the `plint` in the line `Array<plint,3> intPos ((plint)vertex[0], (plint)vertex[1], (plint)vertex[2])` floors the vertex point to the nearest smaller position.
- Still don't understand how the `tau` in `nextJ += tau*W*deltaG[i]` helps calculate the moment.






