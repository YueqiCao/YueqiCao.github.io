---
title: Curvature of Warped Products
date: 2019-09-03 10:27:20
tags:
- Warped Products
categories: Geometry

---

## Curvature of Coupled Planes

Consider the product of two planes $\mathbb R^2\times\mathbb R^2$, with the following Riemannian metric
$$
ds^2=dx^2+dy^2+e^{2f(x,y)}(du^2+dv^2),
$$
where $f(x,y)$ is a smooth function. We compute the sectional/Ricci/scalar curvature of the 'coupled' planes using orthonormal frames. Basics about moving frames are referred to [Loring W. Tu](https://link.springer.com/book/10.1007/978-3-319-55084-8).    

<!--more-->

Consider the following orthonormal bases
$$
e_1=\partial_x,e_2=\partial_y,e_3=e^{-f}\partial_u,e_4=e^{-f}\partial_v.
$$
The dual 1-forms are 
$$
\theta^1=dx,\theta^2=dy,\theta^3=e^{f}du,\theta^4=e^fdv.
$$
There exists a unique skew-symmetric matrix of 1-forms $[\omega^i_j]$ such that
$$
d\theta^i+\omega^i_j\wedge\theta^j=0.
$$
The $\omega^i_j$'s are called the connection 1-forms, and the above equation is called *the first structure equation*. Suppose $\omega^i_j=a^i_jdx+b^i_jdy+c^i_jdu+d^i_jdv$. Substituting into the first structure equation, we solve all the connection 1-forms
$$
\begin{aligned}
&\omega^1_2=\omega^3_4=0,\\
&\omega^1_3=-e^ff_xdu,\omega^1_4=-e^ff_xdv,\\
&\omega^2_3=-e^ff_ydu,\omega^2_4=-e^ff_ydv.
\end{aligned}
$$
The curvature 2-forms are defined by *the second structure equation*
$$
\Omega^i_j=d\omega^i_j+\omega^i_k\wedge\omega^k_j.
$$
Therefore, we write out all the curvature forms
$$
\begin{aligned}
&\Omega^1_2=0,\\
&\Omega^1_3=-e^f(f_{xx}+f_x^2)dx\wedge du-e^f(f_{xy}+f_xf_y)dy\wedge du,\\
&\Omega^1_4=-e^f(f_{xx}+f_x^2)dx\wedge dv-e^f(f_{xy}+f_xf_y)dy\wedge dv,\\
&\Omega^2_3=-e^f(f_{xy}+f_xf_y)dx\wedge du-e^f(f_{yy}+f_y^2)dy\wedge du,\\
&\Omega^2_4=-e^f(f_{xy}+f_xf_y)dx\wedge dv-e^f(f_{yy}+f_y^2)dy\wedge dv,\\
&\Omega^3_4=-e^{2f}(f_x^2+f_y^2)du\wedge dv.
\end{aligned}
$$
By the definition of sectional curvature, for any plane spanned by $e_i,e_j$,
$$
K_{ij}=\langle R(e_i,e_j)e_j,e_i\rangle=\Omega_j^i(e_i,e_j).
$$
Hence, we can compute all the sectional curvature using curvature forms,
$$
\begin{aligned}
&K_{12}=0,\\
&K_{13}=K_{14}=-(f_{xx}+f_x^2),\\
&K_{23}=K_{24}=-(f_{yy}+f_y^2),\\
&K_{34}=-(f_x^2+f_y^2).
\end{aligned}
$$
Ricci curvature is the sum of sectional curvatures, thus,
$$
\begin{aligned}
&Ric_{11}=K_{12}+K_{13}+K_{14}=-2(f_{xx}+f_x^2),\\
&Ric_{22}=K_{12}+K_{23}+K_{24}=-2(f_{yy}+f_y^2),\\
&Ric_{33}=K_{13}+K_{23}+K_{34}=-(f_{xx}+f_{yy}+2f_x^2+2f_y^2),\\
&Ric_{44}=K_{14}+K_{24}+K_{34}=-(f_{xx}+f_{yy}+2f_x^2+2f_y^2),\\
\end{aligned}
$$
Scalar curvature is the sum of Ricci curvature, thus,
$$
S=Ric_{11}+Ric_{22}+Ric_{33}+Ric_{44}.
$$


## Curvature of 4 Dimensional Warped Product Spaces

More generally, let $M$ and $N$ be two Riemannian manifolds with metric $g_M$ and $g_N$, respectively. Consider the product space $M\times N$ with the following metric
$$
g=g_M+e^{2f}g_N,
$$
where $f$ is a smooth function on $M$. This is called the **warped products** of $M$ and $N$, and often denoted by $M\times_{e^f}N$ (see [John Lee, Example 2.24](https://max.book118.com/html/2019/0228/6024223150002012.shtm)).  Let $\theta^1,\theta^2$ be the orthonormal coframe on $M$ and $\omega^1_2$ be the corresponding connection form. Similarly, let $\theta^3,\theta^4,\omega^3_4$ be the orthonormal coframe and connection form on $N$. For the product space $M\times N$, we have the orthonormal coframe
$$
\bar{\theta^1}=\theta^1,\bar{\theta^2}=\theta^2,\bar{\theta^3}=e^f\theta^3,\bar{\theta^4}=e^f\theta^4.
$$
Assume that the connection 1-form for $M\times N$ is
$$
\bar{\omega^i_j}=a^i_j\bar{\theta_1}+b_j^i\bar{\theta_2}+c^i_j\bar{\theta_3}+d^i_j\bar{\theta_4}.
$$
Substituting the connection 1-forms into the first structure equation, we have
$$
\begin{aligned}
&\bar{\omega^1_2}=\omega^1_2,\\
&\bar{\omega^1_3}=-e^{-f}\frac{de^f}{\theta^1}\bar{\theta^3},\\
&\bar{\omega^1_4}=-e^{-f}\frac{de^f}{\theta^1}\bar{\theta^4},\\
&\bar{\omega^2_3}=-e^{-f}\frac{de^f}{\theta^2}\bar{\theta^3},\\
&\bar{\omega^2_4}=-e^{-f}\frac{de^f}{\theta^2}\bar{\theta^4},\\
&\bar{\omega^3_4}=\omega^3_4.
\end{aligned}
$$
Since $de^f$ is a 1-form on $M$, it can be written as a linear combination of $\theta^1$ and $\theta^2$. Let $de^f/\theta^1$ and $de^f/\theta^2$ be the coefficients. Similarly, let $\omega^1_2=a\theta^1+b\theta^2$, by structure equation, $d\theta^1=-\omega^1_2\wedge\theta^2=-a\theta^1\wedge\theta^2$, $d\theta^2=-\omega^2_1\wedge\theta^1=-b\theta^1\wedge\theta^2$. We can write 
$$
\begin{aligned}
&\omega^1_2=-\frac{d\theta^1}{\theta^1\wedge\theta^2}\theta^1-\frac{d\theta^2}{\theta^1\wedge\theta^2}\theta^2,\\
&\omega^3_4=-\frac{d\theta^3}{\theta^3\wedge\theta^4}\theta^3-\frac{d\theta^4}{\theta^3\wedge\theta^4}\theta^4.
\end{aligned}
$$
With these notations, we can list all the curvature 2-forms 
$$
\begin{aligned}
&\bar{\Omega^1_2}=d\omega^1_2=\Omega^1_2,\\
&\bar{\Omega^1_3}=(\frac{de^f}{\theta^2}\frac{d\theta^1}{\theta^1\wedge\theta^2}-\frac{d^2e^f}{(\theta^1)^2})\theta^1\wedge\theta^3+(\frac{de^f}{\theta^2}\frac{d\theta^2}{\theta^1\wedge\theta^2}-\frac{d^2e^f}{\theta^1\theta^2})\theta^2\wedge\theta^3,\\
&\bar{\Omega^1_4}=(\frac{de^f}{\theta^2}\frac{d\theta^1}{\theta^1\wedge\theta^2}-\frac{d^2e^f}{(\theta^1)^2})\theta^1\wedge\theta^4+(\frac{de^f}{\theta^2}\frac{d\theta^2}{\theta^1\wedge\theta^2}-\frac{d^2e^f}{\theta^1\theta^2})\theta^2\wedge\theta^4,\\
&\bar{\Omega^2_3}=(-\frac{de^f}{\theta^1}\frac{d\theta^1}{\theta^1\wedge\theta^2}-\frac{d^2e^f}{\theta^2\theta^1})\theta^1\wedge\theta^3+(-\frac{de^f}{\theta^1}\frac{d\theta^2}{\theta^1\wedge\theta^2}-\frac{d^2e^f}{(\theta^2)^2})\theta^2\wedge\theta^3,\\
&\bar{\Omega^2_4}=(-\frac{de^f}{\theta^1}\frac{d\theta^1}{\theta^1\wedge\theta^2}-\frac{d^2e^f}{\theta^2\theta^1})\theta^1\wedge\theta^4+(-\frac{de^f}{\theta^1}\frac{d\theta^2}{\theta^1\wedge\theta^2}-\frac{d^2e^f}{(\theta^2)^2})\theta^2\wedge\theta^4,\\
&\bar{\Omega^3_4}=\Omega^3_4-((\frac{de^f}{\theta^1})^2+(\frac{de^f}{\theta^2})^2)\theta^3\wedge\theta^4.
\end{aligned}
$$
Hence, the sectional curvatures are 
$$
\begin{aligned}
&\bar{K}_{12}=K_{12},\\
&\bar{K}_{13}=\bar{K}_{14}=e^{-f}(\frac{de^f}{\theta^2}\frac{d\theta^1}{\theta^1\wedge\theta^2}-\frac{d^2e^f}{(\theta^1)^2}),\\
&\bar{K}_{23}=\bar{K}_{24}=e^{-f}(-\frac{de^f}{\theta^1}\frac{d\theta^2}{\theta^1\wedge\theta^2}-\frac{d^2e^f}{(\theta^2)^2}),\\
&\bar{K}_{34}=e^{-2f}(K_{34}-(\frac{de^f}{\theta^1})^2-(\frac{de^f}{\theta^2})^2).
\end{aligned}
$$


## More Examples

Let $\mathbb S^2$ be the unit sphere in $\mathbb R^3$. Using stereographic projection, the *round metric* in local coordinate $(x,y)$ is 
$$
g_{\mathbb S^2}=\frac{4}{(1+x^2+y^2)^2}(dx^2+dy^2).
$$
Let $\theta^1=2/(1+x^2+y^2)dx$ and $\theta^2=2/(1+x^2+y^2)dy$ be the orthonormal coframe. We compute that the connection 1-form is $\omega^1_2=-y\theta^1+x\theta^2$. Therefore, 
$$
\frac{d\theta^1}{\theta^1\wedge\theta^2}=y,\frac{d\theta^2}{\theta^1\wedge\theta^2}=-x.
$$
Denote $(1+x^2+y^2)/2$ by $J$. Then,
$$
\begin{aligned}
&\frac{de^f}{\theta^1}=\frac{e^ff_xdx+e^ff_ydy}{\theta^1}=e^ff_xJ,\\
&\frac{d^2e^f}{(\theta^1)^2}=\frac{d(e^ff_xJ)}{\theta^1}=e^f(f_x)^2J^2+e^ff_{xx}J^2+xe^ff_xJ,\\
&\frac{d^2e^f}{\theta^1\theta^2}=\frac{d(e^ff_xJ)}{\theta^2}=e^ff_xf_yJ^2+e^ff_{xy}J^2+ye^ff_xJ,\\
\end{aligned}
$$
Similarly, we have
$$
\begin{aligned}
&\frac{de^f}{\theta^2}=\frac{e^ff_xdx+e^ff_ydy}{\theta^2}=e^ff_yJ,\\
&\frac{d^2e^f}{(\theta^2)^2}=\frac{d(e^ff_xJ)}{\theta^2}=e^f(f_y)^2J^2+e^ff_{yy}J^2+ye^ff_yJ,\\
&\frac{d^2e^f}{\theta^2\theta^1}=\frac{d(e^ff_xJ)}{\theta^1}=e^ff_xf_yJ^2+e^ff_{xy}J^2+xe^ff_yJ,\\
\end{aligned}
$$
Note that $\frac{d^2e^f}{\theta^1\theta^2}\neq\frac{d^2e^f}{\theta^2\theta^1}$. 

Let $\mathbb H^2$ be the upper plane with *hyperbolic metric*  
$$
g_{\mathbb H^2}=\frac{1}{v^2}(du^2+dv^2).
$$
Under this metric $\mathbb H^2$ will be a Riemannian manifold with constant curvature $-1$. Consider the warped product $\mathbb S^2\times_f \mathbb H^2$. The sectional curvatures are 
$$
\begin{aligned}&\bar{K}_{12}=1,\\&\bar{K}_{13}=\bar{K}_{14}=yf_yJ-(f_x)^2J^2-f_{xx}J^2-xf_xJ,\\&\bar{K}_{23}=\bar{K}_{24}=xf_xJ-(f_y)^2J^2-f_{yy}J^2-yf_yJ,\\&\bar{K}_{34}=e^{-2f}(-1-e^{2f}(f_x)^2J^2-e^{2f}(f_y)^2J^2).\end{aligned}
$$
