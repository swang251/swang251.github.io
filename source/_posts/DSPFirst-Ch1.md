---
title: DSP First - Chapter 1 - Introduction
date: 2018-12-18 18:12:37
tags: DSP First
categories: DSP
mathjax: true
toc: true
---

Just got the TA position for the lecture *Digital Audio Signal Processing*. It is a class introducing the basic digital audio signal processing. Even so, I thought it better to prepare more for the lecture. So I decided to review the reference book *DSP FIRST - A multimedia Approach* during the break.

The contents in the book is well-structured and well-explained, and there is nothing tricky inside. All we need to do is to review and use it again and again to make it a solid in our mind. In the blogs, there is nothing else but a list of the key points presented in the book but hopefully, this could help me strengthen my understanding.

<!--more-->
- This is a book about signals and systems.
- A signal is something that carries information and the system is something that operates the signals.
- In the other {% link book https://www.dspguide.com/ch5/1.htm %}: A signal is a description of how one parameter varies with another parameter. For instance, voltage changing over time in an electronic circuit, or brightness varying with distance in an image. A system is any process that produces an output signal in response to an input signal.

#### 1.1 Mathematical representation of signals
- $s(t)$: the continuous signal
- $s[n] = s(nT_s)$: the discrete-time signal, where $T_s$ is the sampling period.
- Same for the image: $p(x,y) \rightarrow p(m\Delta x, n\Delta y) = p[m, n]$

#### 1.2 Mathematical representation of systems
- A system is something that transform signals into new signals or different signal representations: $y(t) = \mathcal{T}\{x(t)\}$ where the system is represented by the operation $\mathcal{T}\{\}$.
- block diagram: a way for the visualization to represent operations and to show the interrelations among the signals.

> A block diagram is a diagram of a system in which the principal parts or functions are represented by blocks connected by lines that show the relationships of the blocks. (from {%link wiki https://en.wikipedia.org/wiki/Block_diagram%})
