---
title: Bayesian Linear Regression
date: 2019-07-21 14:37:02
tags: 
- Linear Regression
- Least Squares
categories: Statistical-Theory
mathjax: true

---

## The Linear Regression Model

A *normal linear regression model* assumes an output variable $Y$, a vector of covariates ${\bf x}=(x_1,\cdots ,x_p)$, and $Y$ is linear deterministic function $\bf \beta^Tx$ with additive Gaussian noise. <!--more-->That is 
$$
Y={\bf \beta^Tx}+\epsilon, \epsilon\sim \mathcal N(0,\sigma^2).
$$
Given $n$ i.i.d. samples $({\bf x_1},y_1),\cdots, ({\bf x_n},y_n)$, the joint probability density of observed data $y_1,\cdots, y_n$ conditional upon $\bf x_1,\cdots,x_n$ and the value of $\bf \beta$ and $\sigma^2$ (or, the **likelihood function**) is
$$
\begin{aligned}
&p(y_1,\cdots,y_n|{\bf x_1,\cdots,x_n},\beta,\sigma^2)=\prod_{i=1}^np(y_i|{\bf x_i},\beta,\sigma^2)\\
&=(2\pi\sigma^2)^{-n/2}\exp\{-\frac{1}{2\sigma^2}\sum_{i=1}^n(y_i-\beta^T{\bf x_i})^2\}.
\end{aligned}
$$
Maximizing the likelihood function is equivalent to minimizing the sum of squared residuals $SSR(\beta)=\sum_{i=1}^n(y_i-\beta^T{\bf x_i})^2$. Let $\bf X=[\bf x_1,\cdots,x_n]^T$ and ${\bf y}=(y_1,\cdots, y_n)^T$. We have
$$
SSR(\beta)=(\bf y-X\beta)^T(y-X\beta)=\|y-X\beta\|_2^2.
$$
The minimizer, also called the ordinary least square (OLS) estimate, is given in the closed form (suppose $\bf X^TX$ is invertible)
$$
\hat{\beta}_{ols}=\bf (X^TX)^{-1}X^Ty.
$$
The closed form can be obtained using [linear algebra](https://vdisk.weibo.com/s/uGmkTKh4CQ2uJ), which is often explained as the geometric meaning of least square.

## Bayesian Linear Regression

### A Semiconjugate Prior for $\beta$  

Suppose $\beta\sim\mathcal N(\beta_0,\Sigma_0)$. The posterior distribution for $\beta$ is 
$$
\begin{aligned}
&p(\beta|{\bf y,X,\sigma^2})\propto p({\bf y}|{\bf X,\beta,\sigma^2})p(\beta)\\
\propto& \exp\{\bf -\frac{1}{2}(-2\beta^TX^Ty/\sigma^2+\beta^TX^TX\beta/\sigma^2-2\beta^T\Sigma_0^{-1}\beta_0+\beta^T\Sigma_0^{-1}\beta)\}\\
=&\exp\{\bf \beta^T(\Sigma_0^{-1}\beta_0+X^Ty/\sigma^2)-\frac{1}{2}\beta^T(\Sigma_0^{-1}+X^TX/\sigma^2)\beta\}.
\end{aligned}
$$
Therefore, the posterior distribution for $\beta$ is Gaussian with 
$$
\begin{aligned}
&\mathbb E[{\bf \beta|y,X,\sigma^2}]=(\Sigma_0^{-1}+{\bf X^TX/\sigma^2})^{-1}(\Sigma_0^{-1}\beta_0+{\bf X^Ty/\sigma^2})\\
&\textrm{Var}[{\bf \beta|y,X,\sigma^2}]=(\Sigma_0^{-1}+{\bf X^TX/\sigma^2})^{-1}.
\end{aligned}
$$
Suppose $\beta_0=0$ and $\Sigma_0=\alpha^{-1}{\bf I}$. The posterior density is simplified as
$$
p(\beta|{\bf y,X,\sigma^2})\propto \exp\{-\frac{1}{2}(\beta^T({\bf \alpha I+X^TX/\sigma^2})\beta-2\beta^T{\bf X^Ty}/\sigma^2)\}.
$$
Maximizing the posterior probability is equivalent to minimizing the error
$$
\frac{1}{\sigma^2}\sum_{i=1}^n(y_i-\beta^T{\bf x_i})^2+\alpha\beta^T\beta,
$$
which leads to the regularized least square problem. 

### A Semiconjugate Prior for $\sigma^2$ 

Let $\gamma=\frac{1}{\sigma^2}$ be the precision. Suppose $\gamma\sim Gamma(\nu_0/2,\nu_o\sigma^2_0/2)$. The posterior probability for $\gamma$ is
$$
\begin{aligned}
&p(\gamma|{\bf y,X,\beta})\propto p(\gamma)p({\bf y}|{\bf X,\beta,\gamma})\\
\propto&(\gamma^{\nu_0/2-1}\exp\{-\gamma\nu_0\sigma^0/2\})\times(\gamma^{n/2}\exp\{-\gamma SSR(\beta)/2\})\\
=&\gamma^{(\nu_0+n)/2-1}\exp\{-\gamma(\nu_0\sigma^2_0+SSR(\beta))/2\}.
\end{aligned}
$$
Hence, the posterior distribution for $\gamma$ is $Gamma((\nu_0+n)/2,(\nu_0\sigma_0^2+SSR(\beta))/2)$. 

### Gibbs Sampler

Given current values $\{\beta^{(s)},(\sigma^2)^{(s)}\}$. We can sample a new value by

1. Updating $\beta$: 
   1. Compute $\mathbb E[\beta|{\bf y,X,(\sigma^2)^{(s)}}]$ and $\textrm{Var}[\beta|{\bf y,X,(\sigma^2)^{(s)}}]$;
   2. Sample $\beta^{(s+1)}$ according to $\mathcal N(\mathbb E,\textrm{Var})$.
2. Updating $\sigma^2$:
   1. Compute $SSR(\beta^{(s+1)})$;
   2. Sample $(\sigma^2)^{(s+1)}$ according to inverse-gamma.

### Zellner's g-Prior

In the setting of prior distribution of $\beta$, let $\beta_0=0$ and $\Sigma_0=k({\bf X^TX})^{-1}$, where $k=g\sigma^2$. We obtain what is called [g-prior](https://en.wikipedia.org/wiki/G-prior). The mean and variance are simplified as 
$$
\begin{aligned}
&\mathbb E[\beta|{\bf y,X,\sigma^2}]=\frac{g}{g+1}\sigma^2{\bf \Phi}\\
&\textrm{Var}[\beta|{\bf y,X,\sigma^2}]=\frac{g}{g+1}{\bf \Phi X^Ty}.
\end{aligned}
$$
where $\bf\Phi=(X^TX)^{-1}$. Suppose the prior distribution for $\sigma^2$ is inverse-gamma. We will show that $p(\sigma^2|{\bf y,X})$ is inverse-gamma. Compared with the above discussion, this simplifies our sampling procedure since the posterior does **NOT** depend on $\beta$. 

Note that 
$$
p({\bf y}|{\bf X,\sigma^2})=\int p({\bf y}|{\bf X,\sigma^2,\beta})p(\beta|{\bf X,\sigma^2}){\rm d}\beta.
$$
Substituting the densities, we obtain
$$
\begin{aligned}
p({\bf y}|{\bf X,\sigma^2,\beta})p(\beta|{\bf X,\sigma^2})&=C \exp\{-\frac{1}{2\sigma^2}({\bf y-X\beta})^T({\bf y-X\beta})-\frac{1}{2g\sigma^2}\beta^T{\bf \Phi^{-1}}\beta\}.
\end{aligned}
$$
where
$$
C=(2\pi\sigma^2)^{-n/2}\times|2\pi g\sigma^2{\Phi}|^{-1/2}.
$$
The terms in the exponent can be rewritten as
$$
-\frac{1}{2\sigma^2}{\bf y^Ty}-\frac{1}{2}(\beta-m)^TV^{-1}(\beta-m)+\frac{1}{2}m^TV^{-1}m.
$$
where
$$
\begin{aligned}
&V=\frac{g}{g+1}\sigma^2{\bf \Phi}\\
&m=\frac{g}{g+1}{\bf \Phi X^Ty}.
\end{aligned}
$$
The integration is
$$
p({\bf y}|{\bf X,\sigma^2})=(2\pi)^{-n/2}(1+g)^{-p/2}(\sigma^2)^{-n/2}\exp\{-\frac{1}{2\sigma^2}SSR_g\},
$$
where
$$
SSR_g=\bf y^T(I-{\it \frac{g}{g+1}}X^T\Phi X)y.
$$
Let $\gamma=1/\sigma^2\sim Gamma(\nu_0/2,\nu_0\sigma^2_0/2)$. Then we have
$$
\begin{aligned}
p(\gamma|{\bf X,y})&\propto p(\gamma)p({\bf y}|{\bf X,\gamma})\\
&\propto \gamma^{(\nu_0+n)/2-1}\exp\{-\gamma(\nu_0\sigma^2_0+SSR_g)/2\}.
\end{aligned}
$$
Therefore, the posterior distribution for $\sigma^2$ is inverse-gamma with parameter $((\nu_0+n)/2,(\nu_0\sigma^2_0+SSR_g)/2)$. 

### Monte Carlo Sampler

Using g-prior, we see that the posterior distribution of $\sigma^2$ does not contain $\beta$. Thus we can use a simple sampling procedure

1. Sample $\sigma^2$ according to inverse-gamma;
2. Sample $\beta\sim\mathcal N(\frac{g}{g+1}\hat{\beta}_{ols},\frac{g}{g+1}\sigma^2{\bf \Phi})$.

## Reference

1. Hoff, Peter D. *A first course in Bayesian statistical methods*. Vol. 580. New York: Springer, 2009.
2. Bishop, Christopher M. *Pattern recognition and machine learning*. springer, 2006.

