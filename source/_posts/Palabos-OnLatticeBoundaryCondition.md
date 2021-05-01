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