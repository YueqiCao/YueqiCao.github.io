---
title: Basics about Riemannian Submanifolds
date: 2020-04-25 10:42:38
tags:
- Submanifolds
categories: 
- Geometry

---

## The Second Fundamental Form

Let $(\tilde{M},\tilde{g})$ be a Riemannian manifold and $M\subset \tilde{M}$ be a submanifold. By restricting $\tilde{g}$ on $M$ the submanifold is assigned with a natural Riemannian metric.  At each point $p$ we have the orthogonal decomposition with respect to $\tilde{g}_p$,
$$
T_p\tilde{M}=T_pM\oplus T_p^\perp M
$$
where $T_p^\perp M$, called the normal space at $p$, denotes the orthogonal complement of $T_pM$ in $T_p\tilde{M}$. Let $T^\perp M=\cup_{p\in M}T_p^\perp M$. It can be verified that $T^\perp M$ is a vector bundle on $M$, called the normal bundle. The idea to study Riemannian submanifolds is straightforward: **we differentiate the vector fields along $M$ and look at its tangent components and normal components respectively**.<!--more--> Let $\tilde{\nabla}$ be the metric connection on $\tilde{M}$ and $X\in\Gamma(TM)$ be a tangent vector field on $M$. On the one hand, for any vector fields $X,Y\in \Gamma(TM)$, we have 
$$
\tilde{\nabla}_XY=(\tilde{\nabla}_XY)^\top+(\tilde{\nabla}_XY)^\perp
$$
The first term is nothing but the covariant derivative of $Y$ on $M$. Let $\nabla$ be the metric connection on $M$ with respect to the induced Riemannian metric. Then $(\tilde{\nabla}_XY)^\top=\nabla_XY$. Define 
$$
h(X,Y)=(\tilde{\nabla}_XY)^\perp=\tilde{\nabla}_XY-\nabla_XY
$$
It can be verified that $h$ is a normal-bundle-valued symmetric tensor field on $M$, called **the second fundamental form**. Equation (3) is called **the Gauss formula**.

**Remark.** Given $\xi\in \Gamma(T^\perp M)$, we can define a tensor field $\Pi_\xi(X,Y)=\tilde{g}(h(X,Y),\xi)$. In literature $\Pi$ is also called the second fundamental form. 

On the other hand, for a vector field $\xi\in \Gamma(T^\perp M)$, we have 
$$
\tilde{\nabla}_X\xi=(\tilde{\nabla}_X\xi)^\top+(\tilde{\nabla}_X\xi)^\perp
$$
Define the connection $\nabla^\perp:\Gamma(T^\perp M)\times\Gamma(TM)\to \Gamma(T^\perp M)$ by $(\nabla^\perp)_X\xi=(\tilde{\nabla}_X\xi)^\perp$. It can be verified that $\nabla^\perp$ is a connection on the normal bundle $T^\perp M$ which is compatible with the bundle metric, called **the normal connection**. Define 
$$
A_\xi(X)=-(\tilde{\nabla}_X\xi)^\top
$$
The operator $A_\xi:T_pM\to T_pM$ is called **the shape operator** or **the Weingarten map**. The minus sign is chosen so that the following equation holds
$$
\tilde{g}(A_\xi(X),Y)=\tilde{g}(h(X,Y),\xi)
$$
The equation
$$
\tilde{\nabla}_X\xi=-A_\xi(X)+\nabla^\perp_X\xi
$$
is called **the Weingarten formula**.

**Example.** Let $M^{d-1}\subseteq \mathbb{E}^d$ be a hypersurface, $\xi$ be a unit normal vector field on $M$. **The Gauss map** $g:M\to \mathbb{S}^{d-1}$ is defined by $g(p)=\xi_p$. For any $X\in T_pM$, let $\gamma$ be a smooth curve such that $\gamma'(0)=X$. Then
$$
A_\xi X=-(\xi(\gamma)'(0))^\top=-g(\gamma)'(0)=-g_*(X)
$$
that is, $-A_\xi=g_*$ is the differential of Gauss map. It is clear from this example that for hypersurfaces the normal connection is trivial.

Let $e_1,\cdots,e_m$ be a basis of the tangent space and $\xi_1,\cdots,\xi_{d-m}$ be a basis of the normal space. Assume
$$
A_{\xi_\alpha}e_i=\sum_{j=1}^mA_{\alpha i}^je_j
$$
Easy computation shows that
$$
\begin{aligned}
&\Pi_{\xi_\alpha}(e_i,e_j)=A_{\alpha i}^j\\
&h(e_i,e_j)=\sum_{\alpha=1}^{d-m}A_{\alpha i}^j\xi_\alpha
\end{aligned}
$$
Define the mean curvature vector field on $M$ by $H=\frac{1}{m}trace(h)$ where $m$ is the dimension of $M$. By definition $H$ is independent of the choice of basis. Under the above notation we have
$$
H=\frac{1}{m}\sum_{i=1}^m h(e_i,e_i)=\frac{1}{m}\sum_{i=1}^m\sum_{\alpha=1}^{d-m}A_{\alpha i}^i\xi_\alpha=\sum_{\alpha=1}^{d-m}(\frac{1}{m}\text{trace}(A_{\alpha})\xi_{\alpha})=\sum_{\alpha=1}^{d-m}H^\alpha\xi_\alpha
$$
where $H^\xi=\tilde{g}(H,\xi)$ is called the mean curvature along $\xi$. The value $\|H\|=(\sum_\alpha\|H^\alpha\|^2)^{1/2}=\frac{1}{m}(\sum_{\alpha=1}^{d-m}\text{trace}(A_\alpha)^2)^{1/2}$ is called the mean curvature. If $M$ is a hypersurface, $\|H\|=\frac{1}{m}|\text{trace}(A_\alpha)|$. For a surface in 3-dimensional Euclidean space, this coincides with **the absolute mean curvature**. 

## Fundamental Equations

To involve the curvature tensor, we need second order derivative. Thus, we differentiate the Gauss formula and the Weingarten formula. For Gauss formula we have
$$
\begin{aligned}
\tilde{\nabla}_X\tilde{\nabla}_YZ&=\tilde{\nabla}_X\nabla_YZ+\tilde{\nabla}_Xh(Y,Z)\\
&=\nabla_X\nabla_Y+h(X,\nabla_YZ)-A_{h(Y,Z)}(X)+\nabla^\perp_Xh(Y,Z)
\end{aligned}
$$
If we define the curvature tensor to be $\tilde{R}(X,Y)=[\tilde{\nabla}_X,\tilde{\nabla}_Y]-\tilde{\nabla}_{[X,Y]}$, we have
$$
\begin{aligned}
\tilde{R}(X,Y)Z=&R(X,Y)Z+h(X,\nabla_YZ)-h(Y,\nabla_XZ)-h([X,Y],Z)\\
&-A_{h(Y,Z)}(X)+A_{h(X,Z)}(Y)+\nabla^\perp_Xh(Y,Z)-\nabla^\perp_Yh(X,Z)
\end{aligned}
$$
Define the covariant differentiation of $h$ to be
$$
(\nabla_Xh)(Y,Z)=\nabla^\perp_Xh(Y,Z)-h(\nabla_XY,Z)-h(\nabla_XZ,Y)
$$
Then the tangent component of $\tilde{R}(X,Y)Z$ is 
$$
(\tilde{R}(X,Y)Z)^\top=R(X,Y)Z+A_{h(X,Z)}(Y)-A_{h(Y,Z)}(X)
$$
while the normal component is
$$
(\tilde{R}(X,Y)Z)^\perp=(\nabla_Xh)(Y,Z)-(\nabla_Yh)(X,Z)
$$
Equation (12) is called **the Gauss equation** and equation (13) is called **the Codazzi equation**. We can rewrite the Gauss equation as 
$$
\tilde{R}(X,Y,Z,W)=R(X,Y,Z,W)+\langle h(X,Z),h(Y,W)\rangle-\langle h(Y,Z),h(X,W)\rangle
$$
Especially the sectional curvature can be expressed as 
$$
\tilde{K}(X,Y)=K(X,Y)-\langle h(X,X),h(Y,Y)\rangle+\|h(X,Y)\|^2
$$
If the ambient space is Euclidean, then $\overline{R}$ vanishes identically. Let $e_i,e_j$ span a two-plane $\pi_{ij}$, then the sectional curvature of $\pi_{ij}$ is 
$$
K(\pi_{ij})=-\|h(e_i,e_j)\|^2+\langle h(e_i,e_i),h(e_j,e_j)\rangle=\sum_{\alpha=1}^{d-m}(-(A_{\alpha i}^j)^2+A_{\alpha i}^iA_{\alpha j}^j)
$$
From $A_\alpha$ we extract the $2\times 2$ submatrix $A_\alpha|_{\pi_{ij}}$ with $i$th and $j$th row and column. Then 
$$
K(\pi_{ij})=\sum_{\alpha=1}^{d-m}\det(A_\alpha|_{\pi_{ij}})
$$
**Example.** If $M$ is a hypersurface of $\mathbb{E}^d$ with a unit normal vector field $\xi$, the sectional curvature is $K(\pi_{ij})=\det(A_\xi|_{\pi_{ij}})$. If $e_1,\cdots,e_{d-1}$ is a basis that diagonalizes the shape operator with eigenvalues $\lambda_1,\cdots,\lambda_{d-1}$, then $K(\pi_{ij})=\lambda_i\lambda_j$.  The eigenvalues are called **principal curvature** and eigenvectors are called **principal directions**. The determinant of $A_\xi$ is called **the Gauss-Kronecker curvature**.

Similarly we can differentiate the Weingarten formula, which yields
$$
\begin{aligned}
\tilde{\nabla}_X\tilde{\nabla}_Y\xi&=-\tilde{\nabla}_XA_\xi(Y)+\tilde{\nabla}_X\nabla^\perp_Y\xi\\
&=-\nabla_X A_\xi(Y)-h(X,A_\xi(Y))-A_{\nabla^\perp_Y\xi}(X)+\nabla^\perp_X\nabla^\perp_Y\xi
\end{aligned}
$$
Define the curvature tensor on the normal bundle by $R^\perp(X,Y)\xi=[\nabla^\perp_X,\nabla^\perp_Y]\xi-\nabla^\perp_{[X,Y]}\xi$, and define the covariant differentiation of the shape operator by $(\nabla_XA)_\xi(Y)=\nabla_X(A_\xi Y)-A_{\nabla^\perp_X\xi}(Y)-A_\xi(\nabla_XY)$. We obtain that
$$
\begin{aligned}
\tilde{R}(X,Y)\xi=&R^\perp(X,Y)\xi-(\nabla_X A)_\xi(Y)+(\nabla_Y A)_\xi(X)\\
&-h(X,A_\xi(Y))+h(Y,A_\xi(X))
\end{aligned}
$$
The tangent component is 
$$
(\tilde{R}(X,Y)\xi)^\top=-(\nabla_X A)_\xi(Y)+(\nabla_Y A)_\xi(X)
$$
while the normal component is 
$$
(\tilde{R}(X,Y)\xi)^\perp=R^\perp(X,Y)\xi+h(X,A_\xi(Y))-h(Y,A_\xi(X))
$$
Equation (19) is called **the Ricci equation**. Note that equation (18) is equivalent to the Codazzi equation as follows
$$
\begin{aligned}
\langle\tilde{R}(X,Y)\xi,Z\rangle=&\langle-(\nabla_X A)_\xi(Y),Z\rangle+\langle(\nabla_Y A)_\xi(X),Z\rangle\\
=&\langle\nabla_X(A_\xi Y)-A_{\nabla^\perp_X\xi}(Y)-A_\xi(\nabla_XY),Z\rangle\\
&+\langle\nabla_Y(A_\xi X)-A_{\nabla^\perp_Y\xi}(X)-A_\xi(\nabla_YX),Z\rangle\\
=&-\langle\nabla^\perp_X\xi,h(Y,Z)\rangle-\langle\nabla^\perp_Y\xi,h(X,Z)\rangle-\langle h(\nabla_XY,Z),\xi\rangle\\
&-\langle h(\nabla_YX,Z),\xi\rangle+X\langle h(Y,Z),\xi\rangle-\langle h(\nabla_XZ,Y),\xi \rangle\\
&+Y\langle h(X,Z),\xi\rangle-\langle h(\nabla_YZ,X),\xi\rangle\\
=&\langle\nabla_X^\perp h(Y,Z),\xi\rangle+\langle\nabla_Y^\perp h(X,Z),\xi\rangle-\langle h(\nabla_XY,Z),\xi\rangle\\
&-\langle h(\nabla_YX,Z),\xi\rangle-\langle h(\nabla_XZ,Y),\xi \rangle-\langle h(\nabla_YZ,X),\xi\rangle\\
=&\langle(\nabla_X h)(Y,Z)-(\nabla_Y h)(X,Z),\xi\rangle\\
=&\langle\tilde{R}(X,Y)Z,\xi\rangle
\end{aligned}
$$
The three equations (Gauss, Codazzi, Ricci) are called fundamental equations for a submanifold $M\hookrightarrow\tilde{M}$. 

## Examples

### Planar Curves

A planar curve is a 1-dimensional manifold embedded in the 2-plane. Let $\mathbf{t}$ be the tangent vector field and $\mathbf{n}$ be the normal vector field. We have 
$$
A_{\mathbf{n}}\mathbf{t}=-(\overline{D}_{\mathbf{n}}\mathbf{t})^\top=\kappa \mathbf{t}
$$
where $\kappa$ is the curvature. Thus the estimation can be simply given by 
$$
\hat{A}=\frac{\Delta\mathbf{n}\cdot\mathbf{t}}{\Delta p\cdot\mathbf{t}}\approx \kappa
$$

### Space Curves

A space curve is a 1-dimensional manifold embedded in 3-space. Let $\mathbf{t}$ be the tangent vector field, $\mathbf{n}$ be the normal vector field, and $\mathbf{b}$ be the binormal vector field. We have the Frenet formula
$$
\frac{d}{ds}\left(\begin{array}{c}\mathbf{t}\\ \mathbf{n}\\ \mathbf{b}\end{array}\right)=\left(\begin{array}{ccc}0&\kappa&0\\ -\kappa&0&\tau\\ 0&-\tau&0\end{array}\right)\left(\begin{array}{c}\mathbf{t}\\ \mathbf{n}\\ \mathbf{b}\end{array}\right)
$$
where $\kappa$ is curvature and $\tau$ is torsion. Let $\xi=\cos(\theta)\mathbf{n}+\sin(\theta)\mathbf{b}$ be a unit normal vector field. We have
$$
A_\xi\mathbf{t}=\cos(\theta)A_\mathbf{n}\mathbf{t}+\sin(\theta)A_\mathbf{b}\mathbf{t}=\cos(\theta)\kappa\mathbf{t}
$$
Similarly, let $\xi_\perp=-\sin(\theta)\mathbf{n}+\cos(\theta)\mathbf{b}$ be the unit normal vector perpendicular to $\xi$. Then
$$
A_{\xi_\perp}\mathbf{t}=-\sin(\theta)\kappa\mathbf{t}
$$
By definition the mean vector field is $H=\cos(\theta)\kappa\xi-\sin(\theta)\kappa\xi_\perp=\kappa\mathbf{n}$. The mean curvature is $\|H\|=\kappa$.

### Surfaces

A surface is a 2-dimensional manifold embedded in 3-space. The shape operator coincides with the differential of Gauss map (with an additional minus sign). Thus the norm of mean curvature vector $\|H\|$ is in fact the absolute value of mean curvature for surfaces. The sectional curvature is Gaussian curvature for surfaces. 

### Clifford Torus

Let $f:\mathbb{R}^2\to\mathbb{R}^4$ be defined by 
$$
f(\theta,\phi)=\frac{1}{\sqrt{2}}(\cos(\sqrt{2}\theta),\sin(\sqrt{2}\theta),\cos(\sqrt{2}\phi),\sin(\sqrt{2}\phi))
$$
The image of $f$ is $\mathbb{S}^1(\sqrt{1/2})\times\mathbb{S}^1(\sqrt{1/2})$, hence a torus. By computation the tangent vector fields are
$$
\begin{aligned}
& f_\theta = (-\sin(\sqrt{2}\theta),\cos(\sqrt{2}\theta),0,0)\\
& f_\phi = (0,0,-\sin(\sqrt{2}\phi),\cos(\sqrt{2}\phi))
\end{aligned}
$$
The Riemannian metric is given by 
$$
g = d\theta^2+d\phi^2
$$
which is a flat metric, implying the sectional curvature is identically zero. The normal vector fields are given by
$$
\begin{aligned}
& \xi = \frac{1}{\sqrt{2}}(-\cos(\sqrt{2}\theta),-\sin(\sqrt{2}\theta),\cos(\sqrt{2}\phi),\sin(\sqrt{2}\phi))\\
& \nu =\frac{1}{\sqrt{2}}(\cos(\sqrt{2}\theta),\sin(\sqrt{2}\theta),\cos(\sqrt{2}\phi),\sin(\sqrt{2}\phi))
\end{aligned}
$$
By definition the shape operators are given by 
$$
\begin{aligned}
&A_\xi[f_\theta,f_\phi]=[f_\theta,f_\phi]\left[\begin{array}{cc}1&0\\0&-1\end{array}\right]\\
&A_\nu[f_\theta,f_\phi]=[f_\theta,f_\phi]\left[\begin{array}{cc}-1&0\\0&-1\end{array}\right]
\end{aligned}
$$
Therefore, the mean curvature vector field is $H=-\nu$ and the mean curvature is $1$.

### Rotation Group

Let $SO(2)$ be the rotation group which consists of matrices in the form
$$
\left[\begin{array}{cc}\cos(\theta)&-\sin(\theta)\\ \sin(\theta)& \cos(\theta)\end{array}\right]
$$
which can be viewed as a curve in the 4-space. Consider the parametrization
$$
f(\theta)=(\cos(\theta),\sin(\theta),-\sin(\theta),\cos(\theta))
$$
Direct computation shows that the tangent vector field is 
$$
e_\theta=1/\sqrt{2}(-\sin(\theta),\cos(\theta),-\cos(\theta),-\sin(\theta))
$$
and consider the following basis of normal space
$$
\begin{aligned}
& \xi_1=(\cos(\theta),\sin(\theta),0,0)\\
& \xi_2=(0,0,\sin(\theta),-\cos(\theta))\\
& \xi_3=1/\sqrt{2}(-\sin(\theta),\cos(\theta),\cos(\theta),\sin(\theta))
\end{aligned}
$$
Then the shape operators are
$$
A_{\xi_1}e_\theta=-1/\sqrt{2}e_\theta,A_{\xi_2}e_\theta=1/\sqrt{2}e_\theta,A_{\xi_3}e_\theta=0
$$
Hence the mean vector field is $H(\theta)=-1/\sqrt{2}\xi_1+1/\sqrt{2}\xi_2=-1/\sqrt{2}f(\theta)$. 

### Ellipsoid

Let $F:\mathbb{R}^{n+1}\to\mathbb{R}$ be the function 
$$
F(x^1,\cdots,x^{n+1})=\sum_{i=1}^{n+1}(\frac{x^i}{a^i})^2-1
$$
Since $\nabla F(x)\neq 0$ for all $x$ such that $F(x)=0$, the level set $M=F^{-1}(0)$ is a $n$-dimensional submanifold. $\nabla F/\|\nabla F\|$ serves as the unit normal vector field on $M$. The mean curvature is given by the following formula
$$
H=-\frac{1}{n}div(\frac{\nabla F}{\|\nabla F\|})
$$