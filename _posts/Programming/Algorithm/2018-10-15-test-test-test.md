---
layout: post
title: 'Test test test'
date: 2018-10-10
description: '와일드카드 패턴과 문자열이 주어질 때 둘이 매칭되는지 확인하는 알고리즘을 짜보자!'
img:  /algorithm/wildcard.png
categories: [Programming, Algorithm]
tags: [Algorithm]
---
MathJax는 몇 가지 요소로 구성되는데:
  * page preprocessor
  * input preprocessor
  * output preprocessor
  * MathJax Hub
  
MathJax는 나머지 요소를 구성하고 연결하는 역할을 하며, input & output preprocessor는 jax라고 부른다.      

$$
\begin{align} \label{x1}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align}
$$


LaTeX 수학 문법


$$ 
\begin{align}
x &= a + b, \label{x3} \\
y &= c + d + e + f, \label{y3}
\end{align}
$$
