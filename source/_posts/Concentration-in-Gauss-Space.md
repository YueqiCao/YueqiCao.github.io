---
title: Concentration in Gauss Space
date: 2019-07-25 15:54:23
tags: 
- Concentration Inequality
categories: Probability

---

This article aims to solve an exercise in [High-Dimensional Probability](https://www.math.uci.edu/~rvershyn/papers/HDP-book/HDP-book.html#) (Page 112, Exercise 5.2.3).

## Gaussian Isoperimetric Inequality

Let $\mathbb R^n$ equip with the [Gauss measure](https://en.wikipedia.org/wiki/Gaussian_measure) $\gamma_n$:
$$
\gamma_n(E)=\frac{1}{(2\pi)^{n/2}}\int_E\exp\{-\frac{\|x\|^2}{2}\}{\rm d}x
$$
where $E\subseteq \mathbb R^n$ is a Borel set. Then $(\mathbb R^n,\gamma_n)$ is called Gauss space. Gaussian isoperimetric inequality states that, among all the measurable sets with given volume, half spaces have the **smallest perimeter**. Moreover, define the Minkowski sum 
$$
A+B=\{a+b\in\mathbb R^n,a\in A,b\in B\}.
$$
We have the following statement.

<!--more-->

**Theorem.** Let $\epsilon>0$. Among all sets $A\subseteq \mathbb R^n$ with fixed Gauss measure $\gamma_n(A)$, the half spaces minimizes the Gauss measure $\gamma_n(A+B^n(\epsilon))$, where $B^n(\epsilon)$ is a solid ball centered at origin with radius $\epsilon$.

See [here](https://link.springer.com/content/pdf/10.1007/BF01425510.pdf) for a general definition of Gauss space and proof of the above theorem. See [this paper](https://www.jstor.org/stable/29782707?seq=1#page_scan_tab_contents) for a friendly introduction of Gaussian isoperimetric inequality.

## Concentration

We want to prove the following concentration inequality in Gauss spaces.

**Theorem.** Let $X\sim\mathcal N(0,I_n)$ be a Gauss variable. $f:\mathbb R^n\to \mathbb R$ is a Lipschitz function with respect to the standard Euclidean metric. Then $f(X)-\mathbb Ef(X)$ is a sub-gaussian variable. That is,
$$
\mathbb P(|f(X)-\mathbb Ef(X)|>t)\le \exp(-ct^2),\forall t>0,
$$
where $c>0$ is a constant.

First we prove a blow-up lemma using isoperimetric inequality.

**Lemma.** Let $A$ be a subset in Gauss space. If $\gamma_n(A)>1/2$, then for any $t>0$, $\gamma_n(A+B^n(t))\ge1-\frac{1}{2}\exp\{-t^2/2\}$.

**Proof of Lemma.** Let $H=\{x\in\mathbb R^n:x_1\le 0\}$ be the half space. By assumption, $\gamma_n(A)>\gamma_n(H)$. The Gaussian isoperimetric inequality implies 
$$
\gamma_n(A+B^n(t))>\gamma_n(H+B^n(t)).
$$
Note that $H+B^n(t)=\{x\in\mathbb R_n:x_1\le t\}$ is also a half space. Direct computation shows that 
$$
\begin{aligned}
\gamma_n(H+B^n(t))&=\frac{1}{\sqrt{2\pi}}\int_{-\infty}^t\exp\{-\frac{x_1^2}{2}\}{\rm d}x_1\\
&=1-\frac{1}{\sqrt{2\pi}}\int_t^{\infty}\exp\{-\frac{x_1^2}{2}\}{\rm d}x_1\\
&=1-\frac{1}{\sqrt{2\pi}}\int_0^{\infty}\exp\{-\frac{(t+y)^2}{2}\}{\rm d}y\\
&\ge 1-\frac{1}{\sqrt{2\pi}}\int_0^{\infty}\exp\{-\frac{t^2}{2}\}\exp\{-\frac{y^2}{2}\}{\rm d}y\\
&=1-\frac{1}{2}\exp\{-\frac{t^2}{2}\}.
\end{aligned}
$$
Therefore, we have $\gamma_n(A+B^n(t))\ge1-\frac{1}{2}\exp\{-t^2/2\}$. $\blacksquare$ 

This blow-up lemma enables us to prove the main theorem.

**Proof of Main Theorem.** Without loss of generality, we assume $|f(x)-f(y)|\le \|x-y\|$. Let $m$ denote the median of $f(X)$. That is,
$$
\mathbb P(f(X)\le m)\ge 1/2,\mathbb P(f(X)\ge m)\ge 1/2.
$$
Consider the level set $A=f^{-1}((-\infty,m])$. Note that $\mathbb P(f(X)\le m)=\gamma_n(A)\ge 1/2$. By blow-up lemma, $\gamma_n(A+B^n(t))\ge  1-1/2\exp\{-t^2/2\}$. On the other hand, if $x\in A+B^n(t) $, there exists $y\in A$ such that $\|x-y\|\le t$. Therefore, 
$$
f(x)\le \|x-y\|+f(y)=f(y)+t.
$$
This implies $\mathbb P(f(X)\le m+t)\ge \gamma_n(A+B^n(t))$, i.e. $\mathbb P(f(X)-m>t)\le 1/2\exp\{-t^2/2\}$. 

Replace $f$ with $-f$. We can obtain a similar inequality as $\mathbb P(f(X)-m<-t)\le 1/2\exp\{-t^2/2\}$. Hence, 
$$
\mathbb P(|f(X)-m|>t)\le \exp\{-t^2/2\},
$$
which implies $f(X)-m$ is a sub-gaussian variable. Note that $\mathbb E(f(X)-m)=\mathbb E(f(X))-m$. We know that $f(X)-\mathbb Ef(X)$ is a sub-gaussian variable. $\blacksquare$

## Applications

Let us take $f:\mathbb R^n\to\mathbb R$ to be the norm $\|\cdot\|$. Let $X\sim\mathcal N(0,I_n)$ be a Gauss variable. Direct computation shows that
$$
\begin{aligned}
\mathbb Ef(X)&=\mathbb E\|X\|=\frac{1}{(2\pi)^{n/2}}\int \|x\|\exp\{-\frac{\|x\|^2}{2}\}{\rm d}x\\
&=\frac{1}{(2\pi)^{n/2}}\int_0^{\infty}\rho\exp\{-\rho^2/2\}{\rm d}\rho\int_{S^{n-1}(\rho)}{\rm d}\sigma\\
&=\frac{1}{(2\pi)^{n/2}}\times\frac{n\pi^{n/2}}{\Gamma(\frac{n}{2}+1)}\times 2^{(n-1)/2}\Gamma(\frac{n+1}{2})\\
&=\frac{n}{\sqrt{2}}\times\frac{\Gamma(\frac{n+1}{2})}{\Gamma(\frac{n+2}{2})}.
\end{aligned}
$$
By [Stirling's formula]([https://en.wikipedia.org/wiki/Stirling%27s_approximation](https://en.wikipedia.org/wiki/Stirling's_approximation)), the expectation is about $\sqrt{n}$ when $n$ is large. This shows that in high dimensions, the points concentrate in a sphere of radius $\sqrt{n}$. 

