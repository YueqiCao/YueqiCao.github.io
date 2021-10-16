---
title: Error Estimate under Hausdorff Distance
date: 2021-07-22 15:39:34
tags:
- TDA Stability
categories:
- TDA
- Statistical-Theory
---

This is a useful technique I learned from [Convergence rates for persistence diagram estimation in topological data analysis](https://jmlr.csail.mit.edu/papers/volume16/chazal15a/chazal15a.pdf) when one wants to prove convergence results for some estimator under Hausdorff distance. Typical settings are 

- A metric space $(X,\rho)$;
- A probability measure $\mu$ with support $X_\mu$;
- i.i.d samples $\hat{X}=\{X_1,\cdots,X_n\}$ from $\mu$;

the final essential condition is the $(a,b,r_0)$-standard assumption:

- when $r>r_0$, the ball with radius $r$ has volume $\mu(B(r))> ar^b\wedge 1$.

## Bound on Covering Number

The covering number $Cv(A,r)$ for a metric space $A$ is the minimum number of balls of radius $r$ that cover $A$.

The packing number $Pk(A,r)$ for a metric space $A$ is the maximum number of balls of radius $r$ such that they are mutually disjoint.

We have the following relation

> $Pk(A,r)\le Cv(A,r)\le Pk(A,r/2)$

**proof.** Set $m=Pk(A,r)$. There exists $m$ points from $A$ such that the mutual distance is greater than $2r$. If $Cv(A,r)<m$, then by pigeonhole principle there are at least two points lying in the same ball of radius $2r$ which is a contradiction.

Similarly, let $m'=Pk(A,r/2)$, and let $x_1,\cdots, x_{m'}$ be points realizing the packing number. By definition, for any other point $x$ there exists at least one $x_i$ such that $\rho(x,x_i)\le r$. Therefore, $\cup B(x_i,r)=A$.$\blacksquare$

The $(a,b,r_0)$-standard assumption helps us to bound the packing number and covering number.

> when $r>r_0$, the packing number and covering number are such that
> $Pk(A,r)\le \frac{1}{ar^b}\vee 1$ and $Cv(A,r)\le \frac{2^b}{ar^b}\vee 1$.

**proof.** It suffices to prove for $r<a^{-1/b}$. Let $m=Pk(A,r)$. Choose a packing $B_1,\cdots,B_m$. Since they are disjoint, by assumption we have

$$
\sum_{i=1}^m\mu(B_i)\le 1\implies m\le \frac{1}{ar^b}\vee 1
$$

and for covering numbers we have

$$
Cv(A,r)\le Pk(A,r/2)\le \frac{2^b}{ar^b}\vee 1\quad\blacksquare
$$

## Bound on Hausdorff distance

When the sample size $n$ tends to infinity, our intuition tells us that the Hausdorff distance between samples and $X_\mu$ should converge to zeros. The idea of our proof is to reduce the distance between $X_\mu$ and $\hat{X}$ to the distance between covering set and $\hat{X}$, where in the latter case we are dealing with a fixed finite set. More precisely, let $\mathcal{C}=\{c_1,\cdots,c_p\}$ be the set of points realizing the covering number $Cv(X_\mu,r/2)$. Then

$$
\begin{aligned}
\mathbb{P}(d_H(X,X_\mu)>r)\le & \mathbb{P}(d_H(X,\mathcal{C})+d_H(\mathcal{C},\hat{X})>r)\\
\le & \mathbb{P}(d_H(\mathcal{C},\hat{X})>r/2)\\
\le & \mathbb{P}(\exists i\in\{1,\cdots,p\} \text{ such that } \hat{X}\cap B(c_i)=\emptyset)\\
\le & \sum_{i=1}^p \mathbb{P}(\hat{X}\cap B(c_i)=\emptyset)\\
\le & \frac{4^b}{ar^b}[1-\frac{ar^b}{2^b}]^n\\
\le & \frac{4^b}{ar^b}\exp(-n\frac{a}{2^b}r^b)
\end{aligned}
$$

The first inequality comes from the triangle inequality. The second line comes from the fact that any point in $X_\mu$ is in the ball of radius $r/2$ centered at covering set. The third line comes from the definition of Hausdorff distance. Note that for any sample point the distance to $\mathcal{C}$ is less than $r/2$. However, for a covering point the distance to $\hat{X}$ can be larger than $r/2$. The fourth line is a relaxation of the third line. The fifth line substitutes the bound on covering number and standard assumption.

Then we have 

$$
\begin{aligned}
\mathbb{E}[d_H(\hat{X},X_\mu)]=&{}\int_{r>0}\mathbb{P}(d_H(\hat{X},X_\mu))\ {\rm d}r\\
\le&{} r_0 + \int_{r>r_0}\mathbb{P}(d_H(\hat{X},X_\mu))\ {\rm d}r
\end{aligned}
$$

Let $r_n=2(\frac{\log n}{an})^{1/b}$ (the choice of $r_n$ depends on the term inside the exponential). Then 

$$
\begin{aligned}
\mathbb{E}[d_H(\hat{X},X_\mu)]= r_0+r_n1_{(r_0,\infty)}+\int_{r>r_n}\mathbb{P}(d_H(\hat{X},X_\mu))\ {\rm d}r
\end{aligned}
$$

It suffices to bound the integral. Use the transformation of variable $t=nar^b/2^b$. The integral becomes

$$
\begin{aligned}
   \int_{r>r_n}\frac{4^b}{ar^b}\exp(-n\frac{a}{2^b}r^b)\,{\rm d}r &\le \int_{r>\log n} \frac{2^bn}{t}\exp(-t)\, {\rm d}(\frac{2t^{1/b}}{(na)^{1/b}})\\
   & = \frac{2^{b+1}n^{1-1/b}}{a^{1/b}b}\int_{r>\log n}t^{1/b-2}\exp(-t)\,{\rm d}t\\
    & =  \frac{2^{b+1}n^{1-1/b}}{a^{1/b}b}(\log n)^{1/b-2}\exp(-t)|^{\log n}_\infty\\
    & = \frac{2^{b+1}}{a^{1/b}b}(\frac{\log n}{an})^{1/b}\frac{1}{(\log n)^2}
\end{aligned}
$$

If $r_0=0$, then we see that 

$$
\begin{aligned}
\mathbb{E}[d_H(\hat{X},X_\mu)]=O((\log n/n)^{1/b}) 
\end{aligned}
$$

Moreover, we see that 

$$
\begin{aligned}
   \mathbb{P}(d_H(\hat{X},X_\mu)\le r_n) = 1-\mathbb{P}(d_H(\hat{X},X_\mu)>r_n)\ge 1-O((\log n)^{1/b-2}/n^{1/b}) 
\end{aligned}
$$

thus with high probability, 

$$
d_H(\hat{X},X_\mu)\le r_n
$$

or 

$$
\lim_{n\to \infty}\mathbb{P}(d_H(\hat{X},X_\mu)\le r_n)=1
$$

## Bound on Bottleneck Distance

As an application we can prove the convergence rate for persistence diagrams. Suppose we are sampling points from a measure $\mu$ with support $X_\mu$. The support $X_\mu$ has a true persistence diagram $D(X_\mu)$. From the sampling points we have an empirical persistence diagram $D(\hat{X})$. We ask if $D(\hat{X})$ is a good estimator of $D(X_\mu)$. By the [stability theorem](http://yueqicao.top/2019/10/02/Stability-Theorems-in-Topological-Data-Analysis-3/), 

$$
d_B(D(X_\mu),D(\hat{X}))\le d_H(X_\mu,\hat{X})
$$

therefore we find that with high probability,

$$
d_B(D(X_\mu),D(\hat{X}))\le r_n
$$

Thus we can approximate the true persistence diagram by sampling. As the sample size tends to infinity, the empirical persistence diagram will approximate the true diagram with rate at least $O(r_n)$. However, since the computational cost for persistence homology is not economic, in practice we cannot have persistence diagram from large samples. In this case, we need bootstrap method to first approximate the persistence diagram for the large sample. See [Subsampling methods fro persistent homology](http://proceedings.mlr.press/v37/chazal15.pdf).





