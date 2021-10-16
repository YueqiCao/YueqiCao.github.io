---
title: Some Applications of Wasserstein Distances
date: 2019-11-09 09:52:51
tags: 
- Wasserstein Distances
categories: Geometry
---

## OMT I

The original setting for optimal mass transportation (OMT) consists of three objects.

1. Two probability spaces $(X,\mu)$ and $(Y,\nu)$. i.e. $\mu(X)=\nu(Y)=1$;
2. A measurable map $T:X\to Y$ such that $T_*\mu=\nu$. i.e. for any Borel set $B\subset Y$ it holds $\nu(B)=\mu(T^{-1}(B))$.
3. A cost function $c:X\times Y\to \mathbb R_+\cup\{\infty\}$ such that for any $T$ in 2. the map $c_T(x)=c(x,T(x))$ is measurable. The integration $\int_X c(x,T(x))d\mu$ is called the total cost.

<!--more-->

We require that $X$ and $Y$ are probability spaces. However, in practicing many examples do not arise naturally as probability spaces. In those cases we require $\mu(X)=\nu(Y)$ for finite or infinite measures. In the second setting note that we use the **pushforward** of $\mu$ but not the pullback of $\nu$. This has a practical meaning, see [Villani](https://bookstore.ams.org/gsm-58/) for a reference. 

The original problem is raised by Monge that one needs to find a 'transference plan' $T$ to minimize the total cost $\int_X c(x,T(x))d\mu$.

Despite solving Monge's problem, consider the special case where $(X,d)$ is a metric space. $\mu$ and $\nu$ are two measures on $X$ with finite $p$th moments, i.e. $\int_Xd(x,x_0)^pd\mu<\infty,\int_Xd(x,x_0)^pd\nu<\infty$ for any $x_0\in X$. Let $T:X\to X$ range over all measure preserving map so that we can obtain the quantity $(\inf\{\int_Xd(x,T(x))^p\})^{1/p}$ which is called the $p$th Wasserstein distance between $\mu$ and $\nu$, denoted by $W_p(\mu,\nu)$. It can be proved that $W_p$ is a metric on the space of measures with finite $p$th order on $X$.

## Shape Classification

Here is an example that Wasserstein distance is used to classify shapes. See [this paper](https://www.researchgate.net/publication/305887246_Surface-based_shape_classification_using_Wasserstein_distance) for details of methods, and [this paper](https://www.researchgate.net/publication/332180388_A_Geometric_View_of_Optimal_Transportation_and_Generative_Model) for details of proofs.

Let $\mathbb D$ be the unit disk in $\mathbb R^2$ (generally any compact and convex set in $\mathbb R^n$ can be considered), equipped with Lebesgue measure $m$. Let $Y=\{y_1,\cdots,y_k\}$ be a discrete subset in $\mathbb R^2$ with weighted counting measure $\delta=\sum_{i=1}^k b_i\delta_{y_i}$ such that $\delta(Y)=\pi$. In other words, we have two measures on $\mathbb R^2$ where the first is supported on $\mathbb D$ and the second is supported on $Y$. Monge's problem states that a map $f:\mathbb D\to Y$ such that $f_*m=\nu$ is to be find to minimize $\int_{\mathbb D}|x-f(x)|^2dx$, where we use the standard metric on $\mathbb R^2$. Note that $Y$ is discrete. This problem is equivalent to partition $\mathbb D$ into $k$ subsets $D_1\cup\cdots\cup D_k$ such that $m(D_i)=b_i$. Therefore, we can use techniques in [convex geometry](https://www.fmf.uni-lj.si/~lavric/hug&weil.pdf).

Let ${\bf h}=(h_1,\cdots,h_k)\in\mathbb R^k$. Define a piecewise linear convex function $u_{\bf h}(x)=\max\{x\cdot y_i+h_i\}$. Let $G({\bf h})$ be the graph of $u_{\bf h}$. Then $G({\bf h})$ is a piecewise hyperplane. The projection of $G({\bf h})$ to $\mathbb D$ gives a cell decomposition $\mathbb D=\cup_{i=1}^k W_i$, where each $W_i$ corresponds to a piece of plane $\{(x,x\cdot y_i+h_i)|x\in W_i\}$. Assign each $W_i$ to $y_i$. By moving ${\bf h}$ we can find the request assignment with $m(W_i)=b_i$. The fact is that, this is the unique map minimizing the total cost (see [Brenier](https://www.researchgate.net/publication/227632352_Polar_Factorization_and_Monotone_Rearrangement_of_Vector-Valued_Functions), [Aurenhammer](https://www.researchgate.net/publication/220616351_Power_Diagrams_Properties_Algorithms_and_Applications)). Therefore, the problem reduces to find ${\bf h}$ in some suitable space $H_0$. This is done by using Newton's method after defining an objective function $E({\bf h})$ which is twice differentiable and the hessian is given in a closed form.  

For two arbitrary surfaces $M_1,M_2$ in $\mathbb R^3$ (represented by meshes), we use conformal maps to map $M_i$ to unit disks $\mathbb D_i$. For the first disk $\mathbb D_1$ we equip it with Lebesgue measure. For the second disk $\mathbb D_2$ we assign each point (projected from $M_2$) a value so that it is equipped with a weighted counting measure. The Wasserstein distance from $\mathbb D_1$ to $\mathbb D_2$ (in fact. $m$ to $\delta$) measures the difference between $M_1$ and $M_2$.

## OMT II

Consider the following example: $X=\{x_1,\cdots,x_n\}$ and $Y=\{y_1,\cdots,y_n\}$ are finite sets with the same cardinality. Equip $X$ and $Y$ with counting measure. Then a measure preserving map $f:X\to Y$ is exactly a permutation. In many cases it is not adequate to use 'maps' only, since each $x_i$ cannot be 'split' under maps.  If we are permitted to partition each $x_i$ into pieces, then a transference plan is a matrix $\Pi=[\pi_{ij}]$ where $\sum_j \pi_{ij}=1$ for each $i$ and $\sum_{i} \pi_{ij}=1$ for each $j$, i.e. $\Pi$ is a bistochastic matrix. This idea was raised by Kantorovich and the more general setting for OMT is

1. $(X,\mu)$ and $(Y,\nu)$ are probability spaces;
2. $\pi$ is a probability measure on $X\times Y$ such that the maginal distributions are $\mu$ on $X$ and $\nu$ on $Y$ respectively;
3. $c:X\times Y\to \mathbb R_+\cup\{\infty\}$ is a $\pi$ measurable function. The integration $\int_{X\times Y}c(x,y)d\pi$ is called the total cost.

Kantorovich's problem is to find a probability measure $\pi$ so that the total cost is minimized. Note that it is a linear programming problem so we can formulate this in a dual form. The Kantorovich dual problem is 
$$
W_c(\mu,\nu)=\max_{\phi,\psi}\{\int_X\phi(x)d\mu+\int_Y\psi(y)d\nu\}
$$
where $\phi$ and $\psi$ are functions on $X$ and $Y$ respectively and $\phi(x)+\psi(y)\le c(x,y)$. Define $\phi^c(y)=\inf_{x\in X}\{c(x,y)-\phi(x)\}$. Then (1) is equivalent to 
$$
W_c(\mu,\nu)=\max_{\phi}\{\int_X\phi(x)d\mu+\int_Y\phi^c(y)d\nu \}
$$

## WGAN

In [this paper](http://proceedings.mlr.press/v70/arjovsky17a/arjovsky17a.pdf) Wasserstein distance is first introduced to Generative Adversarial Network and the model is called WGAN. A resent [paper](https://www.researchgate.net/publication/332180388_A_Geometric_View_of_Optimal_Transportation_and_Generative_Model) by Gu Xianfeng etc. used geometry to interprete the role of Wasserstein distance in WGAN.

A GAN consists of a generator (G) and a discriminator (D).  (G) generates artificial data and (D) discriminate them from real data. Suppose real data lies in a high dimensional space $\Chi$ and its distribution $\nu$ supports around a low dimensional manifold $\mathcal M$. A local chart $(U,\tau)$ is an open set in $\mathcal M$ together with a map $\tau:U\to Z$  from $U$ to the latent space $Z$. The inverse of $\tau$ is called a parametrization. If $\mu$ is a distribution on $Z$ then a local parametrization pushes forward $\mu$ to be a distribution on $\mathcal M$. i.e. the local parametrization **is** generator (G). Assume the training parameter for (G) is $\theta$ and denote the parametrization by $g_\theta$. (G) generates data on $\mathcal M$ whose distribution is $(g_\theta)_*\mu$. But how to discriminate it from the real distribution $\nu$? The answer is Wasserstein distance $W((g_\theta)_*,\nu)$. More specifically, by Kantorovich dual we need to compute
$$
W_c((g_\theta)_*\mu,\nu)=\max_{\phi}\{\int_Z\phi(g_\theta(z))d\mu+\int_Y\phi^c(y)d\nu\}
$$
Suppose the training parameter for (D) is $\xi$. Then we can rewrite (3) as
$$
W_c((g_\theta)_*\mu,\nu)=\max_{\xi}(\mathbb E_{z\sim \mu}\phi(g_\theta(z))+\mathbb E_{y\sim \nu}\phi^c(y))
$$
Therefore, the discriminator (D) **is** a calculator computing the Wasserstein distance. Above all, we can write down the objective function of a WGAN
$$
\min_{\theta}\max_{\xi}(\mathbb E_{z\sim \mu}\phi(g_\theta(z))+\mathbb E_{y\sim \nu}\phi^c(y))
$$
