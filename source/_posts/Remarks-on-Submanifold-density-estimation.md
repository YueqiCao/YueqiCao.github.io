---
title: Remarks on 'Submanifold density estimation'
date: 2019-08-08 17:00:43
tags: Nonparametric Estimates
categories: Statistical-Theory

---

There seems to be a gap in [Submanifold density estimation](http://papers.nips.cc/paper/3826-submanifold-density-estimation).

In the deduction of variance, one needs to estimate 

>$\frac{1}{h_m^n}\int_M f(q)\frac{1}{h_m^n}K^2(\frac{u_p(q)}{h_m})dV(q)$

Apply theorem 3.1 to function $K^2$ one obtains
$$
\frac{1}{h^n}\int_M K^2(\frac{u_p(q)}{h})\xi(q)dV(q)\to\xi(p)\int_{\mathbb{R}^n}K^2(\|z\|)d^nz,h\to 0.
$$
It seems $h_m^{2n}$ will cause trouble in estimation. Whatever, they claimed that the integration will converges to $f(p)\int K^2(\|z\|)d^nz$. However, in the expression of variance

> $Var[\frac{1}{h_m^n}K(\frac{u_p(q)}{h_m})]=E[\frac{1}{h_m^{2n}}K^2(\frac{u_p(q)}{h_m})]-(E[\frac{1}{h_m^n}K(\frac{u_p(q)}{h_m})])^2$

the first term will converge to a constant times $f(p)$, while the latter will converge to $f(p)^2$. Thus the variance will not converge to 0.



The idea of proof is straightforward. Since $K$ will be supported in $[0,1]$, one notes that when the bandwidth $h$ is small, the integration will be zero outside the normal coordinate. Therefore, everything goes back to Euclidean space.

<!--more--> 