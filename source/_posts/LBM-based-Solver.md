---
title: LBM-based Solver
date: 2018-09-17 17:04:05
tags: [LBM, CFD, Palabos, OpenLB, XFlow, PowerFlow, ProLB]
categories: Palabos
toc: true
---

This is simply a list of different Lattice Boltzmann Method-based solvers.

<!--more-->


## [Palabos](http://palabos.org)
- Short for "PArallel LAttice BOltzmann Solver",
- “Palabos” = “παλαβός” in Greek, meaning “Crazy”
- Developed by [FlowKit Ltd. technology company](https://www.flowkit.com/)
- Supported by [Scientific and Parallel Computing Group (SPC)](http://spc.unige.ch/doku.php) at the University of Geneva.
- A fork from OpenLB
- Written in C++ with no external dependencies (only Posix and MPI). It also provides additional programmer interfaces for the Python and Java.

## [OpenLB](http://www.openlb.net/)
- Developed by the [Lattice Boltzmann Research Group](http://www.lbrg.kit.edu/) at Karlsruhe Institute of Technology, which is led by Dr. Mathias J. Krause.
- The [author list](http://www.openlb.net/authors)

## [XFlow CFD](https://www.3ds.com/products-services/simulia/products/xflow/)
- A SIMULIA product.
- Using MRT-CM and Wall-Modeled Large Eddy Simulation (WMLES) for simulation.
- The [co-simulation with Abaqus](https://www.youtube.com/watch?v=dN92l2gp6lc) sounds cool.

## [PowerFlow](https://exa.com/en/product/simulation-tools/powerflow-cfd-simulation)
- A product of [Exa Corporation](https://exa.com/en) which is acquired by Dassault Systèmes on November 17 ([news here](https://exa.com/en/message-our-customers)) and becomes part of SIMULIA, a Dassault Systèmes brand.
- [Demo video and literature](https://exa.com/en/company/cfd-simulation-resources) could be found in the link.
- [Technology](https://exa.com/en/company/exa-lattice-boltzmann-technology) including very large eddy simulation (VLES).

## [ProLB](http://www.prolb-cfd.com/)
- A recently (maybe) built solver, one of whose creators is Prof. Pierre Sagaut.
- Especially for aeroacoustic and aerodynamic simulation of weakly compressible flow.
- The [technology](http://www.prolb-cfd.com/technology/) includes double relaxation time (DRT) for collision, wall-modeled large eddy simulation (WMLES) for turbulence modeling, immersed boundary model (IBM) for boundary conditions.

PS: 
- [Dassault Systèmes](https://www.3ds.com/) , a subsidiary of Dassault Group, is a CAE/PLM software developing company whose subsidiaries including SIMULIA and SolidWorks. [SIMULIA](https://www.3ds.com/products-services/simulia/) products include Abaqus, XFLOW CFD, and now also PowerFlow.
- Just forget me if anything description is wrong.
