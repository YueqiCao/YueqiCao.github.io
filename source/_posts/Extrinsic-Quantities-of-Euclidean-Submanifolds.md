---
title: Extrinsic Quantities of Euclidean Submanifolds
date: 2020-05-16 16:36:28
tags:
- Submanifolds
categories:
- Geometry

---

Consider an $m$-dimensional compact Riemannian submanifold $\mathcal{M}$ of a Euclidean space $\mathbb{R}^n$ with $m<n$. There are two aspects to investigate the geometry and topology about the submanifold. On the one hand, one can look at the intrinsic quantities defined on $\mathcal{M}$, say Riemannian metric tensor, geodesics, Jacobian fields and sectional curvature. This has often been done in [Lie Group Learning](https://arxiv.org/pdf/1909.12057.pdf), [Information Geometry](http://math.ucr.edu/home/baez/information/) and so on. On the other hand, extrinsic quantities related to the embedding of the submanifold into the Euclidean space, which often include normal vectors (or spaces), the second fundamental form and mean curvature etc. , are also useful and important. For data scientists who always confront with the situation where the underlying manifold is unknown and only random samples are available, to look extrinsically is the only choice. Here we list some extrinsic quantities and show their influences on the geometry and topology of the submanifold.

## Reach and Medial Axis

Let $\mathcal{NM}$ be the normal bundle of $\mathcal{M}$. Consider the map given by
$$
\begin{aligned}
E:\mathcal{NM}&\to \mathbb{R}^n\\
(x,\xi)&\mapsto x+\xi
\end{aligned}
$$
A tubular neighborhood $\mathcal{M}^\tau$ is the diffeomorphic image under $E$ of some open subset $V\subseteq \mathcal{NM}$ of the form
$$
V=\{(x,\xi)\in\mathcal{NM}:\|\xi\|<\tau(x)\}
$$
where $\tau:\mathcal{M}\to \mathbb{R}$ is some positive function. That is, $\mathcal{M}^\tau=E(V)$. It is a fact that every embedded submanifold of $\mathbb{R}^n$ has a tubular neighborhood (See [Theorem 6.17 of Lee](https://www.amazon.com/Introduction-Smooth-Manifolds-Graduate-Mathematics/dp/1441999817). Moreover, if $\mathcal{M}$ is compact, $\tau$ can be chosen to be a constant. The projection $\pi^\tau:\mathcal{M}^\tau\to\mathcal{M}$ sends a point $y\in\mathcal{M}^\tau$ to the closest point $\pi^\tau(y)\in\mathcal{M}$. The [reach](https://arxiv.org/pdf/1705.00989.pdf) $\tau_{\mathcal{M}}$ of $\mathcal{M}$ is the supreme radius for which the tubular neighborhood can be defined. 

In computational geometry, the [medial axis](http://people.cs.uchicago.edu/~niyogi/papersps/NiySmaWeiHom.pdf) is a commonly used notion which is defined as the closure of the set 
$$
G=\{x\in\mathbb{R}^n|\exists p\neq q\in\mathcal{M}\text{ s.t. }d(x,\mathcal{M})=\|x-p\|=\|x-q\|\}
$$
For any $p\in\mathcal{M}$, the local feature size $\sigma(p)$ is the distance of $p$ to $\bar{G}$. By definition we have
$$
\tau_{\mathcal{M}}=\inf_{p\in\mathcal{M}}\sigma(p)
$$

## The Second Fundamental Form

Fix a point $x\in\mathcal{M}$. Let $\Pi:T_x\mathcal{M}\times T_x\mathcal{M}\to T_x^\perp\mathcal{M}$ be the second fundamental form at $x$. For any unit normal $\xi\in T_x^\perp\mathcal{M}$, let $A_\xi$ be the shape operator such that 
$$
\langle\Pi(u,v),\xi\rangle=\langle A_\xi(u),v\rangle
$$
Let $\lambda_\xi$ be the largest eigenvalue of $A_\xi$. It turns out that the operator norm of the shape operator and thus the second fundamental form can be uniformly bounded by the reciprocal of reach. 

> For all $x\in\mathcal{M}$ and all $\xi\in T_x^\perp\mathcal{M}$, we have $\lambda_\xi\le 1/\tau_{\mathcal{M}}$. Therefore, $\|A_\xi\|_{op}\le1/\tau_{\mathcal{M}}$. If we define $\|\Pi\|=\sup_{\|u\|=\|v\|=1}\|\Pi(u,v)\|$, then $\|\Pi\|\le 1/\tau_{\mathcal{M}}$.

Suppose there exists $x$ and $\xi\in T_x^\perp\mathcal{M}$ such that $\lambda_\xi>1/\tau_\mathcal{M}$. There exists some $t<\tau_{\mathcal{M}}$ such that $\lambda_\xi>1/t>1/\tau_{\mathcal{M}}$. Note that 
$$
\lambda_\xi=\sup_{\|u\|=1}\langle\Pi(u,u),\xi\rangle
$$
Let $\gamma(s)$ be a geodesic parametrized by the arc length with $\gamma(0)=x$ and $\dot{\gamma}(0)=u$. Then $\Pi(u,u)=\ddot{\gamma}(0)$. Consider the point $q=x+t\xi$. By assumption, $x$ is the closest point to $q$ in $\mathcal{M}$. Thus 
$$
f(s):=\|\gamma(s)-q\|^2\ge f(0)=t^2
$$
Direct computation shows that
$$
\begin{aligned}
&\dot{f}(s)=2\langle\dot{\gamma}(s),\gamma(s)-q\rangle\\
&\ddot{f}(s)=2(\langle\ddot{\gamma}(s),\gamma(s)-q\rangle+1)
\end{aligned}
$$
Note that $\dot{f}(0)=0$ and $\ddot{f}(0)=2(-t\langle\Pi(u,u),\xi\rangle+1)<0$. By continuity, there exists $s_0$ such that $f(s_0)<f(0)$, which contradicts to our assumption.

Since $\|\Pi(u,v)\|=\sup_{\|\xi\|=1}\langle\Pi(u,v),\xi\rangle=\sup_{\|\xi\|=1}\langle A_\xi(u),v\rangle$ and for any $\xi$ the operator norm $\|A_\xi\|_{op}$ is uniformly bounded, we see that $\|\Pi\|\le1/\tau_{\mathcal{M}}$.

## Local Parametrizations

### Exponential Map

The second fundamental form is closely related to the injective radius, as proved by [Bishop and Alexander](https://arxiv.org/pdf/math/0511570.pdf): If $\|\Pi\|\le C$, then $inj_\mathcal{M}\ge\pi/C$. Thus the exponential map can be defined on the ball of radius $\pi/C$ in $T_x\mathcal{M}$ for all $x$. Fix $x\in\mathcal{M}$, if we transform $\mathcal{M}$ isometrically in $\mathbb{R}^n$ so that $x$ is the origin and the first $m$ standard basis $\{e_1,\cdots,e_m\}$ spans the tangent space $T_x\mathcal{M}$. Consider the coordinate components of the exponential map
$$
\exp(u^1,\cdots,u^m)=(r^1(u^1,\cdots,u^m),\cdots,r^n(u^1,\cdots,u^m))
$$
We can express the derivatives of component functions using the geometrical terms defined on $\mathcal{M}$. Firstly, since the tangent map of $\exp$ at origin is the identity, we have 
$$
d\exp_0(e_i)=(\partial_ir^1(0),\cdots,\partial_ir^n(0))=e_i
$$
We obtain that $\partial_ir^j(0)=\delta^j_i$ for $i,j=1,\cdots,m$ and $\partial_ir^\alpha(0)=0$ for $\alpha=m+1,\cdots,n$. 

For the second derivatives, let $u=\sum_{i=1}^m u^ie_i$ and $\gamma(s)=\exp(su)$. we have
$$
\ddot{\gamma}(0)=(\sum_{i,j}\partial_{i}\partial_jr^1(0)u^iu^j,\cdots,\sum_{i,j}\partial_i\partial_jr^n(0)u^iu^j)=\Pi(u,u)
$$
Thus, $\partial_i\partial_jr^k(0)=0$ for $i,j,k=1,\cdots,m$. Let $\Pi_\alpha(u,v)=\langle\Pi(u,v),e_\alpha\rangle=\langle A_{e_\alpha}(u),v\rangle$. We see that $[\partial_i\partial_jr^\alpha(0)=\langle A_{e_\alpha}e_i,e_j\rangle]_{i,j}$ is the matrix representation for shape operator $A_{e_\alpha}$ for $\alpha=m+1,\cdots,n$. 

By Weingarten formula, we have
$$
\dddot{\gamma}=-A_{\Pi(\dot{\gamma},\dot{\gamma})}(\dot{\gamma})+\nabla_{\dot{\gamma}}^\perp\Pi(\dot{\gamma},\dot{\gamma})
$$
If we define $\nabla\Pi(u,v,w)=\nabla_w^\perp\Pi(u,v)-\Pi(\nabla_wu,v)-\Pi(u,\nabla_wv)$. Then we have
$$
\dddot{\gamma}(0)=-A_{\Pi(u,u)}(u)+(\nabla\Pi)(u,u,u)
$$
Comparing the components on both sides we obtain that
$$
\begin{aligned}
&\partial_i\partial_j\partial_kr^l(0)=-\langle A_{\Pi(e_i,e_j)}(e_k),e_l\rangle\\
&\partial_i\partial_j\partial_kr^\alpha(0)=\langle(\nabla_{e_i}\Pi)(e_j,e_k),e_l\rangle
\end{aligned}
$$
for $i,j,k,l=1,\cdots,m$ and $\alpha=m+1,\cdots,n$. We have also deduced the following tailor expansion for the exponential map
$$
\exp_x(u)=x+u+\frac{1}{2}\Pi(u,u)-\frac{1}{6}A_{\Pi(u,u)}(u)+\frac{1}{6}(\nabla_u\Pi)(u,u)+O(\|u\|^4)
$$
Let $y=\exp_x(su)$ where $\|u\|=1$. We can compare the Euclidean distance $\|y-x\|$ and the Riemannian distance $s=d_\mathcal{M}(x,y)$. In fact, we have 
$$
\|y-x\|^2=s^2+\frac{1}{4}\|\Pi(u,u)\|^2s^4-\frac{1}{3}\langle A_{\Pi(u,u)}(u),u\rangle s^4+o(s^4)
$$
Therefore, 
$$
\|y-x\|=s-\frac{1}{24}\|\Pi(u,u)\|^2s^3+o(s^3)
$$

### Graph Parametrization

Consider a parametrized surface $r(u,v)=(x(u,v),y(u,v),z(u,v))$. Without loss of generality assume that $\left[\begin{array}{cc}x_u& y_u\\ x_v&y_v\end{array}\right]$ is non-singular at $p$. Then by implicit function theorem there will be an open neighborhood near $p$ such that $u=u(x,y),v=v(x,y)$. Then $r(x,y)=(x,y,z(x,y))$ is the graph of function $z=z(x,y)$. 

Generally for any submanifold there exists local parametrization such that it is just the graph of some functions. Furthermore, if we place $p$ at the origin and let $T_p\mathcal{M}$ coincide with the $m$-coordinate space, assume that the parametrization is given by
$$
(u^1,\cdots,u^m)\mapsto(u^1,\cdots,u^m,f^1(u^1,\cdots,u^m),\cdots,f^{n-m}(u^1,\cdots,u^m))
$$
Then by assumption $\partial_if^j(0)=0$ for $i,j=1,\cdots,m$. The normal vector field can be explicitly given by 
$$
\xi^\alpha=(-\partial_1f^\alpha,\cdots,-\partial_mf^\alpha,0,\cdots,\overset{\alpha}{1},\cdots,0)
$$
Thus the matrix representation of the shape operator $A_{e_\alpha}$ is $[\partial_i\xi^\alpha\cdot e_j]_{i,j}=Hess(f^\alpha)$. Note that $Hess(f^\alpha)$ also plays the role as the second fundamental form of the hypersurface
$$
(u^1,\cdots,u^m,f^\alpha(u^1,\cdots,u^m))\subseteq \mathbb{R}^{m+1}
$$
Although the asymptotic of graph parametrization and the exponential map parametrization has a lot in common, they are actually different. For the graph parametrization, the inverse is simply given by the projection onto the tangent space, while for the exponential map this cannot be the case.