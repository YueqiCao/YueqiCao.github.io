---
title: List of Convergence Rates in TDA
date: 2021-10-16 17:40:01
tags:
- TDA Stability
categories: TDA
---

## Frechet means for distributions of persistence diagrams

Consider the measure $\rho = 1/m \sum_{i=1}^m \delta_{Z_i}$ on the space of persistence diagrams. The population Frechet mean is defined by 

$$
Y = \arg\min_Z \int_{\mathcal{D}} d(X,Z)^2 {\rm d}\rho(X)
$$

Let $X_1,\cdots, X_n$ be iid samples from $\rho$. Let $\rho_n = 1/n\sum_{i=1}^n \delta_{X_i}$. The empirical Frechet mean is defined by

$$
Y_n = \arg\min_Z \int_{\mathcal{D}} d(X,Z)^2 {\rm d}\rho_n(X)
$$

> There exists a $Y_n$ such that with probability greater than $1-\delta$
> $$
> d(Y,Y_n)^2\le \frac{m^2F(Y)}{n}\log(\frac{m}{\delta})
> $$
> for $n\ge 8m\log(m/\delta)$ and the right hand side is less than $r^2$ where $r$ characterizes the separation between the local minima of $F$.

## Convergence rates for persistence diagrams estimation in topological data analysis

Let $(M,\rho)$ be a metric space and $\mu$ is a measure on it with support $M_\mu$. Further, assume that $\mu$ satisfies the $(a,b)$-standard assumption: for any $x$ in $M_\mu$ and $r>0$, $\mu(B(x,r))\ge \min(ar^b,1)$ (usually $b=d$ if in $\mathbb{R}^d$). Let $\mathbb{X}=\{X_1,\cdots,X_n\}$ be iid samples from $\mu$. Then we have 

> $\mathbb{E}[d_\infty(\text{Dgm}(M_\mu),\text{Dgm}(\mathbb{X}))]\le C(\frac{\log n}{n})^{1/b}$
> where $C$ is a constant depending on $a$ and $b$. 

Essentially the result comes from the stability theorem of persistence diagrams and convergence for random sets with respect to Hausdorff distance. In fact, we have 

> for any $\epsilon>0$, $\mathbb{P}[d_H(M_\mu,\mathbb{X})]\le \frac{2^b}{a\epsilon^b}\exp(-na\epsilon^b)\wedge 1$

## Subsampling methods for persistent homology

Let $(M,\rho,\mu)$ be the metric measure space satisfying the $(a,b)$-standard assumption. Let $S_1,\cdots,S_n$ be $n$ iid samples of size $m$ from $\mu$. Define the empirical average landscape by 

$$
\hat(\lambda) = \frac{1}{n}\sum_{i=1}^n\lambda_{S_i}
$$

The empirical average landscape is supposed to converge to the population average landscape which is 

$$
\mathbb{E}_{(\mu^{\otimes m})_*}[\lambda]
$$

The bias part is controlled by the following

> Let $r_m = 2(\frac{\log m}{am})^{1/b}$. If $\mu$ satisfies the $(a,b,r_0)$ assumption, then
> $\|\lambda_{M_\mu}-\mathbb{E}[\lambda]\|_\infty\le r_0+r_m 1_{(r_0,\infty)}(r_m)+C(a,b)\frac{r_m}{(\log m)^2}$

The variance part is controlled by 

> $\mathbb{E}\|\hat{\lambda}-\mathbb{E}[\lambda]\|_\infty\le O(1/\sqrt{n})$

## Estimation and quantization of expected persistence diagrams

Let $\Omega=\{(x,y)|y>x\}$ be the open half-plane, and $\partial\Omega=\{(x,x)|x\in\mathbb{R}\}$ be the boundary of $\Omega$. Let $\mathcal{M}^p$ be the space of Radon measures supported on $\Omega$ that have finite total $p$-persistence, i.e. $\int \|x-\partial\Omega\|^p {\rm d}\mu(x)<\infty$. Define the distance between two measures $\mu$ and $\nu$ by 

$$
\textrm{OT}_p = \inf_{\pi}\left(\int_{\bar{\Omega}\times\bar{\Omega}}\|x-y\|^p {\rm d}\pi(x,y)\right) 
$$

where $\pi$ ranges all measures supported on $\bar{\Omega}\times\bar{\Omega}$ whose first marginal coincides with $\mu$ and second marginal coincides with $\nu$. Let $P$ be a probability distribution supported on $(\mathcal{M}^p,\textrm{OT}_p)$. Let $\mathbf{E}(P)$ be the measure defined by, for $A\subset \Omega$ compact, 

$$
\mathbb{E}(P)[A] = \mathbb{E}_P[\mu(A)]
$$

$\mathbf{E}(P)$ is called the expected persistence diagram. If $P$ is a distribution supported on the space of persistence diagrams, it is proved under mild assumptions, $\mathbb{E}(P)$ admits a density with respect to the Lebesgue measure on $\Omega$.

Given iid samples $\mu_1,\cdots,\mu_n\sim P$, the empirical expected persistence diagram is defined by $\bar{\mu}_n=\frac{1}{n}\sum \mu_i$. We have $\bar{\mu}_n\rightarrow\mathbf{E}(P)$ under $\textrm{OT}_p$ almost surely. Specifically,

$$
\mathbb{E}[\textrm{OT}_p^p(\bar{\mu}_n, \mathbf{E}(P))] = O(\frac{1}{n^{1/2}}+\frac{a_p(n)}{n^{p-q}})
$$

where $1\le p<\infty$, $0\le q< p$, and $P$ is a distribution with 'some' restrictions. 

