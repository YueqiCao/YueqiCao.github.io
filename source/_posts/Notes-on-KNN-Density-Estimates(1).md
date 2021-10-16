---
title: Notes on KNN Density Estimates (1)
date: 2019-07-18 15:29:05
tags: 
- Asymptotic Analysis 
- Nonparametric Estimates
categories: Statistical-Theory
---

This series is a note of [Y. P. Mack and M. Rosenblatt](https://mathscinet.ams.org/mathscinet-getitem?mr=530638)'s work in 1979. 

## Introduction

Suppose we have a **bounded, twice differentiable density** function $f$ on $\mathbb R^p$. Let $X_1,X_2,\cdots,X_n$ be $n$ i.i.d. samples of $f$. Let $x\in\mathbb R^p$ be a fixed point so that $f(x)>0$. We want to estimate $f(x)$ based on $n$ samples. The KNN estimate is given by 
$$
f_n(x)=\frac{1}{n(Z_n)^p}\sum_{j=1}^n\omega(\frac{x-X_j}{Z_n}),
$$
where $Z_n$ is the distance between $x$ and its $k$th nearest neighbor, and $\omega$ is a **bounded integrable** weight function with $\int\omega(u){\rm d}u=1$. 

<!--more-->

Let $\omega(u)=\frac{1}{|B_0(1)|}\chi_{B_0(1)}(u)$, where $B_0(1)=\{x\in\mathbb R^p:\|x\|\le 1\}$ is the solid ball centered at origin with radius 1, and $|B_0(1)|=\frac{\pi^{p/2}}{\Gamma(\frac{p+2}{2})}$ is the volume of unit ball. Under these settings we see that the KNN estimate is 
$$
f_n(x)=\frac{1}{n(Z_n)^p}\cdot\frac{k}{|B_0(1)|}=\frac{k}{n}\cdot\frac{1}{|B_0(Z_n)|}.
$$
If we see $\frac{k}{n}$ as the probability that points lie in a ball around $x$, then it is a naive analogy of $\text{probability}=\int\text{density}\approx\text{density}\times \text{area}$. In the following we always assume that $k=k(n)$ is a function of sample size $n$ and $k(n)\to \infty,k(n)/n\to0$ as $n\to\infty$.

We first investigate several properties of $Z_n$. For simplicity, we call $Z_n$ the KNN distance variable.

## KNN distance variable $Z_n$

### CDF and PDF of $Z_n$ 

For fixed $x\in\mathbb R^p$, note that $Z_n$ is a function of $n$ i.i.d. samples. Let $H(r)$ be the cumulative distribution function (**CDF**) of $Z_n$. Let 
$$
G(r)=\mathbb P(B_x(r))=\int_{B_x(r)}f(u){\rm d}u.
$$
For any $\epsilon>0$, consider the probability $H(r+\epsilon)-H(r)=\mathbb P(r\le Z_n\le r+\epsilon)$. Suppose $\epsilon$ is small enough so that there is **exactly one** point lying in the shell of thickness $\epsilon$ (It happens when multiple points lie in the shell, but they will not contribute to our deduction since higher order of $\epsilon$ vanishes when taking limit). There are $n$ choices of $k$th nearest point, $\binom{n-1}{k-1}$ choices of $k-1$ points lying within the $r$ ball and others are outside the $r+\epsilon$ ball. Therefore, we have
$$
H(r+\epsilon)-H(r)=n(G(r+\epsilon)-G(r))\binom{n-1}{k-1}G(r)^{k-1}(1-G(r+\epsilon))^{n-k}.
$$
Let $h(r)$ be the probability density function (**PDF**) of $Z_n$. By definition, we have
$$
h(r)=\lim\limits_{\epsilon\to0}\frac{H(r+\epsilon)-H(r)}{\epsilon}=n\binom{n-1}{k-1}G(r)^{k-1}(1-G(r))^{n-k}G'(r).
$$
Furthermore, $G'(r)$ can be expressed as an integration of $f$. Note that
$$
\begin{aligned}
G'(r)&=\lim\limits_{\delta\to 0}\frac{1}{\delta}[\int_{B_x(r+\delta)}f(u){\rm d}u-\int_{B_x(r)}f(u){\rm d}u]\\
&=\lim_{\delta\to0}\frac{1}{\delta}\int_r^{r+\delta}\rho^{p-1}{\rm d}\rho\int_{S_x(1)}f(\rho,t){\rm d}\sigma(t)\\
&=\int_{S_x(r)}f(t){\rm d}\sigma(t),
\end{aligned}
$$
where $S_x(r)=\{y\in\mathbb R^p:\|y-x\|=r\}$ is the sphere centered at $x$ with radius $r$, and ${\rm d}\sigma$ is the volume element on the sphere. 

On the other hand, for each $X_i$, $\|X_i-x\|$ is a random variable with CDF $G(r)$ and   PDF $G'(r)$. Note that $Z_n$ is exactly the **$k$th order statistic** from i.i.d. samples $\|X_i-x\|$. The $k$th order statistic gives the same $h(r)$ as we deduced above.

### Moments of $Z_n$ 

In general, for a measurable function $\phi$, we want to compute the expectation $\mathbb{E}\phi(Z_n)$. By definition,
$$
\begin{aligned}
\mathbb E\phi(Z_n)&=\int_0^{\infty}\phi(r)h(r){\rm d}r\\
&=n\binom{n-1}{k-1}\int_0^{\infty}\phi(r)G(r)^{k-1}(1-G(r))^{n-k}{\rm d}G(r).
\end{aligned}
$$
In our situation, we consider a specific function of the type
$$
\phi(r)=\frac{r^{\lambda}}{G(r)^\gamma(1-G(r))^\beta},
$$
where $\lambda,\gamma,\beta$ are nonnegative integers. Note that $G(r)\in[0,1]$. To ensure that the integration exists, we assume that $1-G(r)=O(r^{-\xi})$, where $\xi>0$, as $r\to \infty$.  

Since $G(r)$ is a monotonically increasing function, we can solve $r=G^{-1}(t)$ where $t\in[0,1]$. On the one hand,
$$
\begin{aligned}
G(r)&=\int_{B_x(r)}f(u){\rm d}u\\
&=f(x)|B_x(r)|+\int_{B_x(r)}f(u)-f(x){\rm d}u,\\
\end{aligned}
$$
where
$$
\int_{B_x(r)}|f(u)-f(x|{\rm d}u\le K(r)\int_{B_x(r)}\|u-x\|{\rm d  }u=\frac{K(r)}{n+1}r^{p+1}|S_x(1)|.
$$
Therefore, $t=G(r)=cf(x)r^p+o(r^p)$ as $r\to 0$, where $c=|B_x(1)|$. From the assumption $1-G(r)=O(r^{-\xi})$, we see that $t=1-O(r^{-\xi})$ as $r\to\infty$. We can write $r$ as
$$
r=G^{-1}(t)=(\frac{t}{cf(x)})^{1/p}+\eta(t),
$$
where $\eta(t)=o(t^{1/p})$ as $t\to 0$ and $\eta(t)=O(\frac{1}{(1-t)^\xi})$ as $t\to 1$.

Using the change of variable $t=G(r)$, we see that
$$
\begin{aligned}
\mathbb E\phi(Z_n)&=n\binom{n-1}{k-1}\int_0^1(\frac{t}{cf(x)}+\eta(t))^\lambda t^{k-1-\gamma}(1-t)^{n-k-\beta}{\rm d}t\\

\end{aligned}
$$



----

**Personal Comments**

I was intended to study [Y. P. Mack and M. Rosenblatt](https://mathscinet.ams.org/mathscinet-getitem?mr=530638)'s paper thoroughly to understand the asymptotic behaviors of kNN estimator. Both results and techniques in proofs are important for me. However, I was very upset to find many subtle details I could not get through. The biggest problem appears in equation (12)

> $$
> \mathbb E \phi(R_n)=n\binom{n-1}{k-1}\int_0^1((\frac{t}{cf(x)})^\lambda+o(t^\lambda))t^{k-1-\gamma}(1-t)^{n-k-\beta}{\rm d}t
> $$

The notation $o(t)$ is misleading. It is correct when $t$ is small. However, when $t$ is close to 1, this term tends to infinity. Therefore, the estimation for this expectation is not easy. One cannot simply drop the $o(t)$ integration. But according to the paper (though they did not display the computation), $o(t)$ was simply dropped. 

It was also disappointing that I found there were few papers concerning the asymptotic behaviors about kNN. One could find that the asymptotic moments for kNN distance variable are well-known. But the references were not mentioned. 

There is another paper discussing the asymptotic moments of kNN distance. But it restricts to compact convex area. See [Asymptotic moments of near–neighbour distance distributions](https://royalsocietypublishing.org/doi/abs/10.1098/rspa.2002.1011).

I will keep on tracking about this topic.



