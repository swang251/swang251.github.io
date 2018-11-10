---
title: Calculating Fluctuation in Paraview
date: 2018-11-08 16:32:21
tags: [Paraview]
categories: Paraview
mathjax: true
---

This is to show the way to calculate variable (e.g. pressure) fluctuation in Paraview. 

<!--more-->

To calculate the $\tilde{p} = p - \bar{p}$ in Paraview, where $\bar{p}$ is the time average.

- Open the data (.vtk files) as object `p` and saying it contains the variable `pressure`.
- Calculate the time average using the filter *Temporal Statistics* (Filters -> Temporal -> Temporal Statistices) and the output is the object `TemporalStatistics1`.
- Selecte the `p` and the `TemporalStatistics1`, and apply the filter *Append Attributes*. The output is `AppendAttributes1`.
- Use a *Calculator* to subtract pressure_average from pressure.

![Fig. 1 - The pipeline for calculating the fluctuation](/images/20181108/paraview_fluctuation.png)

### Reference 
Paraview Forum Discussion:  https://public.kitware.com/pipermail/paraview/2012-May/024845.html


