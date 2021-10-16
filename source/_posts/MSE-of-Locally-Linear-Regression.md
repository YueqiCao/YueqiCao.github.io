---
title: MSE of Locally Linear Regression
date: 2019-07-30 17:32:01
tags:
- Linear Regression
- Least Squares
- Nonparametric Estimates
categories: Statistical-Theory

---

## Backgrounds

Locally linear regression (also called locally weighted least squares) is an important method in nonparametric regression. Its understanding is intuitive. Suppose one has a general model
$$
y=g(x)+\epsilon(x),
$$
where $g$ is a any smooth function, and $\epsilon(x)$ is a variable with zero mean and finite variance. Let $X_1,X_2,\cdots,X_n$ be i.i.d. samples with bounded density $f$, and $Y_1,Y_2,\cdots, Y_n$ be the corresponding responses (assume $X_i$'s are scalars '). By Taylor expansion, we have
$$
Y_i-g(x)\approx \beta(X_i-x)+\epsilon(x).
$$
<!--more-->

To emphasize the local information around $x$, we introduce the kernel function $K_h(u)=K(u/h)/h$, where $\int K(u){\rm d}u=1$ and $h>0$ is called the bandwidth.  And consider the following optimization
$$
\arg\min_{g,\beta}\sum_{i=1}^n(Y_i-g-\beta(X_i-x))^2K_h(X_i-x).
$$
We introduce the following notations
$$
\begin{gather}
{\bf Y}=[Y_1,Y_2,\cdots,Y_n]^T,\\
{\bf X}=\left[\begin{array}{cc}1&X_1-x\\1&X_2-x\\ \cdots&\cdots\\ 1&X_n-x\end{array}\right],\\
{\bf W}={\rm diag}\{K_h(X_1-x),\cdots,K_h(X_n-x)\},\\
e_1=[1,0]^T,\\
e_2=[0,1]^T.
\end{gather}
$$
Then the optimization has a closed solution
$$
\begin{gather}
\hat{g}(x)=e_1^T({\bf X^TWX})^{-1}{\bf X^TWY},\\
\hat{\beta}=e_2^T({\bf X^TWX})^{-1}{\bf X^TWY}.
\end{gather}
$$
For the present we analyze the conditional bias and variance of $\hat{g}(x)$. Note that by assumptions we have $\mathbb E[Y|X]=g(X)$,$\mathbb E[(Y-g(X))^2|X]=\sigma^2(X)$. Let $g({\bf X})=[g(X_1),g(X_2),\cdots,g(X_n)]^T$. We have the following decomposition
$$
\begin{aligned}
\hat{g}(x)-g(x)=&e_1^T({\bf X^TWX})^{-1}{\bf X^TW}({\bf Y}-g({\bf X}))\\
&+e_1^T({\bf X^TWX})^{-1}{\bf X^TW}g({\bf X})-g(x).
\end{aligned}
$$
Taking expectations on both sizes, we have
$$
\begin{aligned}
\mathbb E[(\hat{g}(x)-g(x))^2|{\bf X}]=&\mathbb E[(e_1^T({\bf X^TWX})^{-1}{\bf X^TW}({\bf Y}-g({\bf X})))^2|{\bf X}]\\
&+(e_1^T({\bf X^TWX})^{-1}{\bf X^TW}g({\bf X})-g(x))^2.
\end{aligned}
$$

The first term is variance and the second term is square of bias.

## Variance

Let ${\bf \Sigma}={\rm diag}\{\sigma^2(X_1),\cdots,\sigma^2(X_n)\}$. Variance can be simplified as
$$
e_1^T({\bf X^TWX})^{-1}{\bf X^TW\Sigma WX}({\bf X^TWX})^{-1}e_1.
$$
Denote $\sum_{i=1}^n K_h(X_i-x)(X_i-x)^j$ by $S_j$ for $j=0,1,2$. Then we have 
$$
{\bf X^TWX}=\left[\begin{array}{cc}S_0&S_1\\S_1&S_2\end{array}\right].
$$
Note that
$$
\mathbb E[S_j/nh^j|{\bf X}]=\int K(u)u^jf(x+hu){\rm d}u=\mu_jf(x)+o(1),
$$
where $\mu_j=\int K(u)u^j{\rm d}u<\infty$. Furthermore,
$$
\begin{aligned}
{\rm Var}[S_j/nh^j|{\bf X}]&\le\frac{1}{n}\mathbb E[K_h(X_i-x)^2((X_i-x)/h)^{2j}|{\bf X}]\\
&\le \frac{1}{nh}\int K(u)^2u^{2j}f(x+hu){\rm d}u.
\end{aligned}
$$
Therefore, $\rm Var\to 0$ as $nh\to \infty$. By Chebyshev's inequality, we can write 
$$
S_j/nh^j=\mu_jf(x)+o_{\mathbb P}(1),
$$
where $o_{\mathbb P}(1)$ denotes an infinitesimal in probability. Let ${\bf H}={\rm diag}\{1,h\}$. Then 
$$
\frac{1}{n}{\bf H^{-1}X^TWXH^{-1}}=f(x)\left[\begin{array}{cc}1&0\\0&\mu_2\end{array}\right]+o_{\mathbb P}(1),
$$
where we assume that $\mu_j=0$ for odd $j$. 

Let $\nu_j=\int K(u)^2u^j{\rm d}u$. By a similar argument we have 
$$
\frac{1}{n}{\bf H^{-1}X^TW\Sigma WXH^{-1}}=f(x)\sigma^2(x)\left[\begin{array}{cc}\nu_0&0\\0&\nu_2\end{array}\right]+o_{\mathbb P}(1).
$$
Now we can obtain that
$$
\begin{aligned}
&e_1^T({\bf X^TWX})^{-1}{\bf X^TW\Sigma WX}({\bf X^TWX})^{-1}e_1\\
=&\frac{1}{nh}e_1^T{\bf H^{-1}}({\bf H^{-1}X^TWXH^{-1}}/n)^{-1}(\frac{h}{n}{\bf H^{-1}X^TW\Sigma WXH^{-1}})\\
&({\bf H^{-1}X^TWXH^{-1}}/n)^{-1}{\bf H^{-1}}e_1\\
=&\frac{1}{nh}\left(\left(e_1^T\left[\begin{array}{cc}1&0\\0&\mu_2\end{array}\right]^{-1}\left[\begin{array}{cc}\nu_1&0\\0&\nu_2\end{array}\right]\left[\begin{array}{cc}1&0\\0&\mu_2\end{array}\right]^{-1}e_1\right)\frac{\sigma^2(x)}{f(x)}+o_{\mathbb P}(1)\right)\\
=&\frac{1}{nh}(\frac{\nu_0\sigma^2(x)}{f(x)}+o_{\mathbb P}(1)).
\end{aligned}
$$

## Bias

Consider the Taylor expansion for $g$,
$$
g(X_i)=g(x)+g'(x)(X_i-x)+\frac{1}{2}g''(x)(X_i-x)^2+\frac{1}{6}g'''(\bar{X}_i)(X_i-x)^3.
$$
Write $r(X_i)=g(X_i)-g(x)-g'(x)(X_i-x)$. Then we have
$$
g({\bf X})=g(x){\bf X}e_1+g'(x){\bf X}e_2+r({\bf X}).
$$
Therefore, the bias term is 
$$
\begin{aligned}
&e_1^T({\bf X^TWX})^{-1}{\bf X^TW}g({\bf X})-g(x)\\
=&g(x)e_1^T({\bf X^TWX})^{-1}{\bf X^TWX}e_1+g'(x)e_1^T({\bf X^TWX})^{-1}{\bf X^TWX}e_2\\
&+e_1^T({\bf X^TWX})^{-1}{\bf X^TW}r({\bf X})-g(x)\\
=&e_1^T({\bf X^TWX})^{-1}{\bf X^TW}r({\bf X}).
\end{aligned}
$$
For the second order term we have the following estimation
$$
\frac{g''(x)}{2nh^2}{\bf H^{-1}X^TW}[(X_1-x)^2,\cdots,(X_n-x)^2]^T=\left(\begin{array}{c}\frac{1}{2}\mu_2f(x)g''(x)\\0\end{array}\right)+o_{\mathbb P}(1).
$$
For the third order term, we assume that $g'''(\bar{X}_i)$ are bounded. The matrix norm is bounded by
$$
\begin{aligned}
&\|\frac{1}{nh^2}{\bf H^{-1}X^TW}[(X_1-x)^3g(\bar{X}_1),\cdots,(X_n-x)^3g(\bar{X}_n)]^T\|\\
\le & C\max\{\frac{1}{nh^2}\sum_{i=1}^n K_h(X_i-x)|X_i-x|^3,\frac{1}{nh^2}S_4\}.
\end{aligned}
$$
By a similar argument as above, the bound is $o_{\mathbb P}(1)$ when $n\to\infty$. Therefore, the bias is
$$
\begin{aligned}
&e_1^T({\bf X^TWX})^{-1}{\bf X^TW}r({\bf X})\\
=&h^2e_1^T{\bf H^{-1}}(\frac{1}{n}{\bf H^{-1}X^TWXH^{-1}})^{-1}\frac{1}{nh^2}{\bf H^{-1}X^TW}r({\bf X})\\
=&\frac{h^2}{2}\left(g''(x)e_1^T\left[\begin{array}{cc}1&0\\0&\mu_2\end{array}\right]^{-1}\left[\begin{array}{cc}\mu_2\\\mu_3\end{array}\right]+o_{\mathbb P}(1)\right)\\
=&\frac{h^2}{2}(g''(x)\mu_2+o_{\mathbb P}(1))
\end{aligned}
$$
Note that if $g$ is a linear function then we will **NOT** have bias.

## Derivative Estimation

Finally we consider the conditional bias and variance for $\hat{\beta}$. The main difference is that ${\bf H}^{-1}e_2=e_2/h$. Therefore we will have order $O(1/{nh^3})$ in variance, and $O(h)$ in bias.  

## References

The whole procedure can be generalized to multivariate case, where $X$ is a vector and $K(\cdot)$ is a multivariate kernel. The details are displayed in [D. Ruppert and M.P. Wand](https://projecteuclid.org/download/pdf_1/euclid.aos/1176325632)'s paper.

Also in this paper, they considered locally polynomial regression for univariate case. Conditional bias and variance are deduced for derivatives in any order. They also explained why one can not drop *condition* in asymptotic analysis for locally linear regression.

A nice introduction to LLR (and other topics in nonparametric estimates) can be found in the [lecture notes](https://ocw.mit.edu/courses/economics/14-385-nonlinear-econometric-analysis-fall-2007/lecture-notes/). This article mainly follows [local linear regression](https://ocw.mit.edu/courses/economics/14-385-nonlinear-econometric-analysis-fall-2007/lecture-notes/local_lin_reg.pdf).  