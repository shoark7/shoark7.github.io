---
layout: post
title: '[부록] 피보나치 수열 행렬 곱 증명'
date: 2018-11-25
description: 'This post proves Fibonacci sequence with matrix multiplication'
img:  /algorithm/fibonacci-logo.png
categories: [Programming, Knowledge]
tags: [Algorithm, Fibonacci_sequence, Fibonacci]
---


## 들어가며

---

[직전 알고리즘 포스트](/programming/algorithm/피보나치-알고리즘을-해결하는-5가지-방법.html){:target="_blank"}가 피보나치 수열 알고리즘을 해결하는 방법들에 대해 다뤘다. 그 중 4번째 방법이 행렬의 곱셈을 이용한 방법이었는데 그 식에서 아래와 같은 식을 제시했다.


$$
 F_{n}\text{이 } n\text{번째 피보나치 수라고 할 때,} \\
 \\
 \begin{pmatrix}
   F_{n+1} & F_{n} \\
   F_{n} & F_{n-1} 
 \end{pmatrix}
 =
 \begin{pmatrix}
   1 & 1 \\
   1 & 0
 \end{pmatrix}^n
$$

위 식이 0 이상의 정수 _n_ 에 대해 성립해야 행렬 곱셈 풀이가 의미가 있다. 그래서 이번 포스트는 위 식을 증명해보자. 수학적 귀납법을 활용한다.



## 증명

---

피보나치 수열은 다음과 같은 수열이다.

$$
\begin{equation}  \label{x1}
	F_{n+2} = F_{n+1} + F_{n+2} \\
	(n >= 0, F_0 = 1, F_1 = 1)
\end{equation}
$$

이 식을 행렬을 이용해 표현하면 다음과 같이 표현해볼 수 있다.



$$
\begin{align}  \label{x2}
  \begin{bmatrix}
    F_{n+2}
  \end{bmatrix}
  =
  \begin{bmatrix}
    1 & 1
  \end{bmatrix}
  \begin{bmatrix}
    F_{n+1} \\
    F_n
  \end{bmatrix}
  \\
  \begin{bmatrix}
    F_{n+1}
  \end{bmatrix}
  =
  \begin{bmatrix}
    1 & 0
  \end{bmatrix}
  \begin{bmatrix}
    F_{n+1} \\
    F_n
  \end{bmatrix}
\end{align}
$$

이 두 행렬을 결합하면 다음과 같이 된다.

$$
\begin{align}  \label{x3}
	\begin{bmatrix}
		F_{n+2} \\
		F_{n+1}
	\end{bmatrix}
	=
	\begin{bmatrix}
		1 & 1 \\
		1 & 0
	\end{bmatrix}
	\begin{bmatrix}
		F_{n+1} \\
		F_n
	\end{bmatrix}
\end{align}
$$

위 식에 _n_ 대신 _n-1_ 을 대입하고 두 행렬을 다시 결합하면 결국 아래와 같은 일반식을 도출할 수 있다.


$$
\begin{align}  \label{x4}
	\begin{bmatrix}
		F_{n+2} & F_{n+1} \\
		F_{n+1} & F_n
	\end{bmatrix}
	=
	\begin{bmatrix}
		1 & 1 \\
		1 & 0
	\end{bmatrix}
	\begin{bmatrix}
		F_{n+1} & F_n \\
		F_n & F_{n-1}
	\end{bmatrix}
	&& \cdots && \text{이 식을 A라고 하자}
\end{align}
$$


### 수학적 귀납 증명

$$
\begin{array}
	\mathit{1.} \text{ 가설: }
	 \begin{pmatrix}
	   F_{n+1} & F_{n} \\
	   F_{n} & F_{n-1} 
	 \end{pmatrix}
	 =
	 \begin{pmatrix}
	   1 & 1 \\
	   1 & 0
	 \end{pmatrix}^n
	 \text{는 } n\text{ 이 모든 자연수일 때 성립}
	\\	
	\\
	\mathit{2.} \text{ 검증:} \text{ 2.1. 위 식이 } n\text{이 1일 때 성립 & 2.2. 모든 자연수 } n\text{에 대해 성립} \\
	 \mathit{2.1.} \text{ } n \text{이 1일 때} 
	 \begin{pmatrix}
	   F_{2} & F_{1} \\
	   F_{1} & F_{0} 
	 \end{pmatrix}
	 =
	 \begin{pmatrix}
	   1 & 1 \\
	   1 & 0
	 \end{pmatrix}
	 \text{는 참} \\

	 \mathit{2.2.} n \text{에 임의의 자연수} k\text{를 대입: } 
	 \begin{pmatrix}
	   F_{k+1} & F_{k} \\
	   F_{k} & F_{k-1} 
	 \end{pmatrix}
	 =
	 \begin{pmatrix}
	   1 & 1 \\
	   1 & 0
	 \end{pmatrix}^k



\end{array}
$$
