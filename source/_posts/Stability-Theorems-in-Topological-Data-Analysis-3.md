---
title: Stability Theorems in Topological Data Analysis (3)
date: 2019-10-02 11:37:47
tags:
- TDA Stability
categories: TDA

---

Perhaps the most important case in TDA is point cloud data, i.e. finite metric spaces. The collection of all compact metric spaces makes up a metric space under [Gromov-Hausdorff metric]([https://en.wikipedia.org/wiki/Gromov%E2%80%93Hausdorff_convergence](https://en.wikipedia.org/wiki/Gromov–Hausdorff_convergence)). If we construct Rips filtrations for point clouds,  we obtain a map between metric spaces by sending each point cloud to its persistence diagram. It is natural to ask which properties will this map have. From the work of [F. Memoli etc.](http://fodava.gatech.edu/files/reports/FODAVA-09-24.pdf), it is in fact a **Lipschitz** map. Therefore, the bottleneck distance between two persistence diagrams is bounded by the Gromov-Hausdorff distance between two point clouds. This stability shows that one can use TDA to classify different point clouds, which is a major object in shape analysis.

Let $(Z,d_Z)$ be a (compact) metric space and $X,Y$ be subsets in $Z$. The Hausdorff distance between $X$ and $Y$ is defined as
$$
d_H^Z(X,Y)=\max\{\max_{x\in X}\min_{y\in Y}d_Z(x,y),\max_{y\in Y}\min_{x\in X}d_Z(x,y)\}.
$$
The intuition is follows: For each $x\in X$, we can compute the distance between $x$ and $Y$, which is $\min_{y\in Y}d_Z(x,y)$. Then we take the largest value as the distance from $X$ to $Y$. The distance is the so called one-sided Hausdorff distance. Symmetrically, we compute the distance from $Y$ to $X$. The maximum is the so called (two-sided) Hausdorff distance.

<!--more-->

If $(X,d_X)$ and $(Y,d_Y)$ are different metric spaces, we cannot compare the distance between $X$ and $Y$ unless they are subspaces of another space $(Z,d_Z)$. Therefore, we try to embed $(X,d_X)$ and $(Y,d_Y)$ into a larger space so that they can be compared using Hausdorff distance. This motivates the following definition of Gromov-Hausdorff distance    
$$
d_{GH}((X,d_X),(Y,d_Y))=\inf_{X,Y\hookrightarrow Z}d_H^Z(X,Y).
$$
Let $\mathcal{X}=\{(X,d_X):X\text{ is compact metric space}\}$. Define an equivalence relation on $\mathcal{X}$: $(X,d_X)\sim(Y,d_Y)$ if they are isometric. The quotient space is still denoted by $\mathcal{X}$. Then $(\mathcal{X},d_{GH})$ is a complete metric space (see [this book](https://www.amazon.com/Course-Metric-Geometry-Dmitri-Burago/dp/0821821296) for reference). Furthermore, the infimum is in fact a minimum, that is, we can always find $Z$ for compact spaces.

Given a finite metric space $(X,d_X)$ and a parameter $\alpha>0$, the Rips complex $R_\alpha(X,d_X)$ is an abstract simplicial complex with vertex set $X$. A $k$-simplex is in $R_\alpha(X,d_X)$ if and only if the diameter is no more than $2\alpha$. (**Caveat.** The factor 2 makes a difference in the main theorem. Note that it is a classical issue that there is no universal parametrization on Rips complex.) When $\alpha$ ranges from $0$ to $\infty$, the nested family is called Rips filtration, denoted by $\mathcal{R}(X,d_X)$.

Moreover, if $X$ is a finite subset of $(\mathbb{R}^n,l^\infty)$, there is another construction called $\check{C}ech$ complex which is the nerve of $l^\infty$ balls, denoted by $C_\alpha(X,l^\infty)$. It happens that the two constructions are the same.

-----

**Lemma**. For any finite set $X$ in $(\mathbb{R}^n,l^\infty)$ and $\alpha>0$, $C_\alpha(X,l^\infty)=R_\alpha(X,l^\infty)$.

**proof**. If $\{x_1,\cdots,x_k\}$ is in $C_\alpha$, then there is $\bar{x}$ such that  $|x_i-\bar{x}|_\infty\le \alpha$. By triangle inequality $|x_i-x_j|_\infty\le 2\alpha$. $\{x_1,\cdots,x_k\}$ is in $R_\alpha$. On the other hand, if $|x_i-x_j|_\infty\le 2\alpha$, for each coordinate $l$ we take $\bar{x}^{(l)}=1/2(x^{(l)}_{\max}+x^{(l)}_{\min})$. It is easy to verify $|x_i-\bar{x}|_\infty\le \alpha$. $\{x_1,\cdots,x_k\}$ is in $C_\alpha$.

------

Another useful lemma can be found in the [book](https://www.amazon.com/Course-Metric-Geometry-Dmitri-Burago/dp/0821821296) which says that any finite metric space of cardinality $n$ can be isometrically embedded into $(\mathbb{R}^n,l^\infty)$. The proof is also straightforward. Put the distances in the coordinates in $\mathbb{R}^n$. One also finds a comprehensive introduction to embedding of finite metric spaces [here](https://sites.cs.ucsb.edu/~suri/cs235/MatousekMetric.pdf).

Now we can state and prove the stability theorem.

------

**Theorem**. For any finite metric spaces $(X,d_X)$ and $(Y,d_Y)$, for any $k\in \mathbb{N}$, 
$$
d^\infty_B(D_k\mathcal{R}(X,d_X),D_k\mathcal{R}(Y,d_Y))\le d_{GH}((X,d_X),(Y,d_Y)).
$$
**proof**. Let $\epsilon=d_{GH}((X,d_X),(Y,d_Y))$. By definition, there is a compact metric space $(Z,d_Z)$ and inclusions $\gamma_X:X\to Z$ and $\gamma_Y:Y\to Z$ such that $d_H^Z(X,Y)\le \epsilon$. Since $\gamma_X(X)\cup\gamma_Y(Y)$ is finite, they can be isometrically embedded into $(\mathbb{R}^n,l^\infty)$ for some $n$. Denote the embedding by $\gamma$. Let $\delta_X$ be the distance function to $\gamma(\gamma_X(X))$. That is,  
$$
\delta_X(z)=\min_{x\in X}|z-\gamma(\gamma_X(x))|_\infty.
$$
Similarly, let $\delta_Y$ be the distance function to $\gamma(\gamma_Y(Y))$. Note that
$$
|\delta_X(z)-\delta_Y(z)|\le d_H^\infty(\gamma(\gamma_X(X)),\gamma(\gamma_Y(Y)))=\epsilon.
$$
(*I have doubt in this inequality. The closest point in $X$ and $Y$ may not correspond in Hausdorff distance*).

----

*update.* This inequality is true. Note that $\delta_X(z)=d(z,X)$. For any point $y\in Y$ it holds $d(z,X)\le d(z,y)+d(y,X)$. Since $\inf_y(d(z,y)+d(y,X))\le \inf_yd(z,y)+\sup_yd(y,X)$, we obtain $d(z,X)-d(z,Y)\le H(X,Y)$. The other side is similar.

---



Since $\delta_X$ and $\delta_Y$ are $\epsilon$-close, by the theorem of [Edelsbrunner etc.](https://link.springer.com/article/10.1007%2Fs00454-006-1276-5), the persistence diagrams of $\delta_X$ and $\delta_Y$ are $\epsilon$-close.

However, the level set $\delta_X([0,\alpha])$ is nothing but the union of $\alpha$-balls in $(\mathbb{R}^n,l^\infty)$. By persistence nerve theorem the sublevel filtration of $\delta_X$ and the $\check{C}ech$ filtration of $\gamma(\gamma_X(X))$ yield same persistence diagrams. From the above lemma, $C_\alpha(\gamma(\gamma_X(X)),l^\infty)=R_\alpha(\gamma(\gamma_X(X)),l^\infty)=R_\alpha(\gamma_X(X),d_Z)=R_\alpha(X,d_X)$. Therefore, the persistence diagram of $\delta_X$ is exactly the persistence diagram $D\mathcal{R}(X,d_X)$. Apply the same argument to $Y$. Hence the inequality holds.

------

