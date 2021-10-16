---
title: Two Applications of the Weingarten Map
date: 2020-07-11 15:32:28
tags:
- Submanifolds
categories:
- Geometry
---

If $\mathcal{M}$ is an Euclidean submanifold, many intrinsic quantities can be expressed using information from the ambient Euclidean space. Here are two examples where the Weingarten map plays an important role: first is the Riemannian hessian of a smooth map, and second is the Ricci curvature tensor. Assume that $f:\mathcal{M}\to\mathbb{R}$ is a smooth function and $\widehat{f}:\mathbb{R}^d\to\mathbb{R}$ is a smooth extension of $f$. In data science, it is much more convenient to compute the gradient or hessian of $\widehat{f}$ than those of $f$. [Absil etc.](https://link.springer.com/chapter/10.1007/978-3-642-40020-9_39) presented the relations and applied them in Riemannian optimization. On the other hand, Ricci curvature is also a hot topic in manifold learning. An old paper of [Hicks](https://www.jstor.org/stable/2034680) proves that there is a simple relation between Ricci map and Weingarten map if the manifold is a hypersurface. Many problems concerning Ricci curvature thus descend to the estimation of the Weingarten map.

### Riemannian Hessian

Let $\mathcal{M}$ be an $m$-dimensional submanifold in the $d$-dimensional Euclidean space $\mathbb{R}^d$. Let $\pi_x:\mathbb{R}^d\to T_x\mathcal{M}$ be the orthogonal projection to the tangent space $T_x\mathcal{M}$. It turns out that the gradient of $f$ is nothing but the projection of gradient of $\widehat{f}$. Denote $\partial\widehat{f}$ to be the usual gradient for $\widehat{f}$ and $\text{grad}(f)$ to be the Riemannian gradient for $f$. Then we have

> $\text{grad}(f)_x=\pi_x(\partial\widehat{f}_x)$ 

To check this equality, note that for any tangent vector $v\in T_x\mathcal{M}$ and smooth curve $\gamma$ in $\mathcal{M}$ with $\gamma(0)=x$ and $\gamma'(0)=v$ we have 
$$
\langle v,\text{grad}(f)_x\rangle=v(f)=\frac{\rm d}{\rm dt}|_0f(\gamma(t))=\frac{\rm d}{\rm dt}|_0\widehat{f}(\gamma(t))=\langle v,\pi_x(\partial\widehat{f}_x)\rangle
$$
Let $\nabla$ be the Riemannian connection on $\mathcal{M}$. For any vector fields $X$ and $Y$, by definition, 
$$
\nabla_XY=\pi(\partial_XY)
$$
Define the Riemannian hessian of $f$ at $x$ by
$$
\text{Hess}f_x(v)=\nabla_v\text{grad}(f)
$$
It is easy to check that
$$
\langle\text{Hess}f_x(v),w\rangle=v(w(f))-\langle\nabla_vw,\text{grad}(f)\rangle=\langle\text{Hess}f_x(w),v\rangle
$$
Thus, $\text{Hess}f_x:T_x\mathcal{M}\to T_x\mathcal{M}$ is a self-adjoint operator. However, the original definition is difficult to use in practice. Further computation shows that
$$
\text{Hess}f_x(v)=\pi_x\partial_v(\pi\partial\widehat{f})=\pi_x((\partial_v\pi)\partial\widehat{f}_x+\partial^2\widehat{f}_x(v))
$$
where we have used the product rule. If we understand $\pi$ as matrices then $\partial_v\pi$ contains elements which are derivatives of those in $\pi$. From the result we see that Riemannian hessian of $f$ differs from the projection of usual hessian of $\widehat{f}$ by a term involving the covariant derivative of $\pi$. Let $\pi^\perp:\mathbb{R}^d\to T^\perp_x\mathcal{M}$ be the projection operator to the normal space at $x$. Using the identity $\text{id}=\pi+\pi^\perp$, we have 
$$
\pi_x\partial_v\pi=-\pi_x\partial_v\pi^\perp
$$
In addition, since $\pi\pi^\perp=0$, we have
$$
0=\pi_x\partial_v(\pi\pi^\perp)=\pi_x(\partial_v\pi^\perp)_x+\pi_x(\partial_v\pi)_x\pi^\perp_x
$$
which implies $\pi_x(\partial_v\pi^\perp)_x\pi_x=0$ and $\pi_x(\partial_v\pi)\partial\widehat{f}_x=-\pi_x(\partial_v\pi^\perp)_x\pi_x^\perp\partial\widehat{f}_x$.

Recall that the Weingarten map at $x$ for $\xi\in T^\perp_x\mathcal{M}$ is defined by $A_{x,\xi}(v)=-\pi_x\partial_v\tilde{\xi}$ where $v\in T_x\mathcal{M}$ and $\tilde{\xi}$ is any extension of $\xi$. The identity implies that
$$
A_{x,\xi}(v)=-\pi_x\partial_v(\pi^\perp\tilde{\xi})=-\pi_x(\partial_v\pi^\perp)_x\xi-\pi_x\pi_x^\perp\partial_v\tilde{\xi}=-\pi_x(\partial_v\pi^\perp)_x\xi
$$
Utilizing the above results we have
$$
\text{Hess}f_x(v)=\pi_x\partial^2\widehat{f}_x(v)+A_{x,\pi_x^\perp\partial\widehat{f}_x}(v)
$$

### Ricci Map

Suppose $\mathcal{M}$ is a **hypersurface** in Euclidean space. i.e. $\mathcal{M}$ is of codimension $1$. Let $\xi$ be a local unit normal vector field. The second fundamental form can be simplified as 
$$
h(X,Y)=\partial_XY-\nabla_XY=\langle\partial_XY,\xi\rangle\xi=\langle Y,A_\xi(X)\rangle\xi
$$
where we have used the identity $X\langle Y,\xi\rangle=\langle\partial_XY,\xi\rangle+\langle Y,\partial_X\xi\rangle$ and the definition of Weingarten map. Recall that for Euclidean submanifolds Gauss equation reads
$$
0=\tilde{R}(X,Y)Z=R(X,Y)Z-A_{h(Y,Z)}X+A_{h(X,Z)}Y
$$
Substituting the expression of the second fundamental form into above, we have
$$
R(X,Y)Z=\langle A_\xi(Y),Z\rangle A_\xi(X)-\langle A_\xi(X),Z\rangle A_\xi(Y)
$$
Let $Z_1,\cdots,Z_m$ be an orthonormal base of principal vectors of $A_\xi$. i.e. $A_\xi(Z_i)=k_iZ_i$ where $k_i$'s are principal curvatures. Let $H=\sum k_i$ be the mean curvature and define $Ric:T_x\mathcal{M}\to T_x\mathcal{M}$ by $Ric(X)=\sum_{i=1}^m R(X,Z_i)Z_i$, called **Ricci map**. Then we have
$$
\begin{aligned}
Ric(X)&=\sum_{i=1}^mR(X,Z_i)Z_i\\
&=\sum_{i=1}^m\langle A_\xi(Z_i),Z_i\rangle A_\xi(X)-\langle A_\xi(X),Z_i\rangle A_\xi(Z_i)\\
&=\sum_{i=1}^m\langle k_iZ_i,Z_i\rangle A_\xi(X)-\langle A_\xi(X),Z_i\rangle k_iZ_i\\
&=H A_\xi(X)-\sum_{i=1}^m\langle A_\xi(X),A_\xi(Z_i)\rangle Z_i\\
&=H A_\xi(X)-\sum_{i=1}^m\langle A_\xi^2(X),Z_i\rangle Z_i\\
&=H A_\xi(X)-A_\xi^2(X)
\end{aligned}
$$
Therefore we have proved the following identity relating the Ricci map with Weingarten map
$$
A_\xi^2-HA_\xi+Ric=0
$$
An obvious corollary is that every principal vector is also a Ricci vector. i.e. $Ric$ has the same eigenvectors as $A_\xi$.

**Example.** Let $\mathcal{M}$ be a surface in the three space. The characteristic equation for Weingarten map is $A^2-HA+KI=0$ where $K$ is Gauss curvature. Comparing both equations we have $Ric=KI$.

