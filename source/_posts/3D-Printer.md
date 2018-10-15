---
title: 3D Printing and Musical Instruments
date: 2018-10-06 17:29:47
tags: [Research Daily, CAML]
categories: Research Daily
toc: true
---
3D printing is becoming more and more popular in a variety of areas and there are already many application in musical instruments. Here I will briefly talks about the main techniques and some of my preliminary attemps in printing a mouthpiece.

<!--more-->

## 3D Printing Techniques

This article deserves reading, [All 10 Types of 3D Printing Technology in 2018 - All3DP](https://all3dp.com/1/types-of-3d-printers-3d-printing-technology/), inside which it classify the 3D printing techniques into, *material extrusion*, *vat polymerization*, *material jetting*, *binder jetting*, and *powder bed fusion (polymers or metals)*.


### Fused Deposition Modeling (FDM) - Material Extrusion
The model is built layer by layer by the deposited materials which is melt through a nozzle in the extrusion head. The model is normally built from the bottom to the top.

### Stereolithography Apparatus (SLA) - Vat Polymerization
SLA is the earliest commercialized 3D printing technique. The 3D model is fabricated layer by layer from the liquid resin which is selectively solidified or polymerized by the ultraviolet (UV) rays through the lenses and the mirror. The object is normally built from the top to the bottom. A good introductory guide is provided by [Formlab](https://formlabs.com/blog/ultimate-guide-to-stereolithography-sla-3d-printing/).

### Selective Laser Sintering (SLS) - Power Bed Fusion
SLS is similar to SLA. A thin layer of material powder is dispersed on the platform and preheated to the temperature just below the melting point. The the laser as the power source is used to sinter the materials (nylon or polymers). A good introductory guide is provided by [Formlab](https://formlabs.com/blog/what-is-selective-laser-sintering/#origins-sls).

### PolyJet - Material Jetting
PolyJet provide a faster and more accurate 3D printing compared with the techniques mentioned above. The print head deposits hundreds of tiny liquid droplets of the UV curable materials on the platform and the UV light attached to the print head simultaniously cures/solidifies the materials. A brief introduction could be found the [Stratsys website](http://www.stratasys.com/polyjet-technology) or the [introduction video](https://youtu.be/Som3CddHfZE) provided by Solid Concepts.

### Comparisons between them
- [SLA vs. PolyJet](https://www.cadimensions.com/blog/sla-vs-polyjet-need-know/)
- [FDM vs. SLA](https://pinshape.com/blog/fdm-vs-sla-how-does-3d-printer-tech-work/)
- [FDM vs. SLA](https://all3dp.com/fdm-vs-sla/)

## 3D Printed Musical Instruments - the real functional instruments instead of the ones just for fun

### Strings
Two of the 3D printed violins are [3Dvarius](https://www.3d-varius.com/), the first electronic 3D printed violin inspired by Stradivarius and made by SLA, and [HOVALIN](http://www.hovalabs.com/hova-instruments/hovalin), an open source 3D printable acoustic violin made by FDM.

### Brass instruments
[Jerome Wiss](http://jeromewiss.com/en/) use 3D printing for the prototype of his brass instruments.

### Saxophone Mouthpiece
It is tested by Lorenzoni et al. (2013) that PolyJet is the best technique for 3D printing a mouthpiece. [SYOS](https://www.syos.co/en/) is using FDM for making customized mouthpiece. 

Personnaly, I have tried both FDM (Ultimaker 2+/3)and SLA (Form2) in 3D printing a saxophone mouthpiece. SLA provides a better resolution with an easier operation while you have to play with hundreds of parameters to print an acceptable mouthpiece by FDM. Such parameters might include:

- Resolution
- Nozzle sizes
- Layer thickness
- Line width
- Infilling
- Ironing


## Ref.
- [3D printing: future of the music instrument making? - Syos Blog](https://www.syos.co/en/blog/lab/3-d-printing-musical-instruments)
- [TOP 15 3D Printed Music Instruments & Music Applications](https://www.3dnatives.com/en/top-15-3d-printing-music210620174/)
- [常见三种3D打印技术：FDM、SLS、SLA技术原理](http://www.3ddayin.net/fuwu/3Ddayinbaike/23932.html)
- [20张动图秒懂SLA、CLIP、3DP、PolyJet和FDM 3D打印原理](http://www.cnpowdertech.com/2017/kejifazhan_0327/20974.html)
- [How does a Form2 3D printer compare to an Ultimaker2+? What is the failure rate and how much maintenance is needed?-Quora](https://www.quora.com/How-does-a-Form2-3D-printer-compare-to-an-Ultimaker2+-What-is-the-failure-rate-and-how-much-maintenance-is-needed)
- Lorenzoni, Valerio, E. L. Doubrovski, and J. C. Verlinden. 2013. “Embracing the Digital in Instrument Making: Towards a Musician-Tailored Mouthpiece by 3D Printing.” In Proceedings of the Stockholm Music Acoustics Conference 2013, SMAC 2013, Stockholm (Sweden), 30 July-3 August, 2013.

