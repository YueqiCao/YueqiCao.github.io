---
title: Forman-Ricci Curvature on Complexes
date: 2020-02-16 11:35:34
tags:
- Forman Curvature
categories: Geometry

---

## Bochner-Weitzenb$\bf\ddot{o}$ck Formula on Riemannian Manifolds

Let $(M,g)$ be an $n$-dimensional Riemannian manifold, and $\nabla$ be the Levi-Civita connection. Recall that for a smooth function (or 0-form) $f\in C^\infty(M)=\mathcal A^0(M)$, the *Laplacian of smooth functions* is defined as 
$$
\Delta_0(f)=\text{tr}\nabla^2(f)=\text{div}(\text{grad}(f))
$$
The definition $\Delta_0=\text{tr}\nabla^2$ can be generalized to arbitrary $p$-forms and is called the *connection Laplacian*. Suppose in addition $M$ is oriented. Let $d:\mathcal A^p(M)\to\mathcal A^{p+1}(M)$ be the differential operator. We can define the adjoint operator $d^{\*}$ of $d$ using the *Hodge star operator*. i.e. $d^{\*}:\mathcal A^{p+1}(M)\to\mathcal A^p(M)$ is the operator satisfying $\langle d\alpha,\beta\rangle=\langle\alpha,d^{\*}\beta\rangle=\int_Md\alpha\wedge {\*}\beta$ for $\alpha\in\mathcal A^p(M)$ and $\beta\in\mathcal A^{p+1}$. The *Hodge Laplacian* is defined by 
$$
\Delta=dd^*+d^*d
$$
By direct computation, we can see that $\Delta=-\Delta_0$ on $C^\infty(M)=\mathcal A^0(M)$. However, it is much more complicated in higher dimensions.<!--more--> The *Bochner-Weitzenb$\ddot{o}$ck formula* tells that, on $\mathcal A^p(M)$ for $p>0$, a term involving curvature tensor should be added. More precisely, we have 
$$
\Delta=-\Delta_0+\sum_{i,j}\omega^i\wedge i_{E_j}R_{E_iE_j}
$$
where $E_1,\cdots,E_n$ is a local orthonormal frame and $w^1,\cdots,\omega^n$ is the corresponding coframe. $i_{E_j}$ is the interior multiplication and $R_{E_iE_j}=\nabla_{[E_i,E_j]}-[\nabla_{E_i},\nabla_{E_j}]$ is the curvature tensor. For 1-forms the following equation is commonly presented in textbooks.
$$
\frac{1}{2}\Delta_0|\omega|^2=|\nabla\omega|^2-\langle\Delta\omega,\omega\rangle+\text{Ric}(\omega_*,\omega_*)
$$
Using this formula one is able to prove the following Bochner's theorem

> Let $M$ be a compact, oriented Riemannian manifold, whose Ricci curvature tensor is nonnegative and positive at one point. Then $H^1(M;\mathbb R)$=0.

From Hodge theorem it suffices to prove that every harmonic 1-form is zero. Let $\omega$ be a harmonic 1-form. Integrate equation (4) on both sides and note that on any compact manifold we have $\int_M \Delta_0(f)dv=0$. We have 
$$
\nabla\omega=0 \text{ and } \text{Ric}(\omega_*,\omega_*)=0
$$
For any vector field $X$ we have $X|\omega|^2=2\langle\nabla_X\omega,\omega\rangle=0$. Hence $|\omega|$ is constant. If $\omega\neq 0$ at one point then $\omega\neq 0$ on $M$. But $\text{Ric}$ is positive at one point which means at this point $\text{Ric}(\omega_\*,\omega_\*)>0$, which is a contradiction.

This 'standard' proof is not the same as Bochner's original proof. In fact, Bochner defined Laplacian in the following way. Since $\nabla:\Gamma(\bigwedge^\*(M))\to\Gamma(\bigwedge^\*(M)\otimes T^\*M)$ is a linear map between inner product spaces, it admits an adjoint $\nabla^\*$. The [*Bochner Laplacian*](https://en.wikipedia.org/wiki/Laplace_operators_in_differential_geometry) is defined by $\Delta_B=\nabla^\*\nabla$, which is also called *rough Laplacian* in literature (see [Berger](https://www.springer.com/gp/book/9783540653172)). It is easy to see that $\Delta_B$ is nonnegative definite and $\text{Ker}(\Delta_B)=\text{Ker}(\nabla)$ whose elements are parallel forms. By computation one verifies that $\Delta_B=-\Delta_0$. Therefore,
$$
\Delta=\Delta_B+\text{Curv}(R)
$$
If $\text{Curv}(R)$ is nonnegative, then $\text{Ker}(\Delta)=\text{Ker}(\Delta_B)\cap\text{Ker}(\text{Curv}(R))$. But parallel forms are completely determined at one point. Therefore, if $\text{Curv}(R)$ is positive at one point, the harmonic forms will be identically zero. 

## Forman's Discretization of Ricci Curvature

Bochner's proof is carefully studied by [Robin Forman](https://link.springer.com/article/10.1007%2Fs00454-002-0743-x) so as to place a combinatorial analogy in discrete cases. In 2003, a series of combinatorial invariants for quasiconvex CW complexes were proposed, named 'curvature' by Forman. In the simplest case, suppose $M$ is a simplicial complex. For each nonnegative integer $p$, define the $p$th curvature function by 
$$
\mathcal F_p(\alpha)=\#\{(p+1)\text{-cofaces}\}+\#\{(p-1)\text{-faces}\}-\#\{\text{parallel neighbors}\}
$$
where parallel neighbors of $\alpha$ are $p$-simplices sharing either a $(p+1)$-coface or $(p-1)$-face but not both. For $p=1$, $\mathcal F_1$ is called Ricci curvature by Forman, denoted by $\text{Ric}$. Using this analogy Forman could prove several Bochner-type theorems. For example, one has the following

> Let $M$ be a connected weighted quasiconvex CW complex with nonnegative Ricci curvature. Suppose, in addition, there exists a vertex $v$ such that $\text{Ric}(e)>0$ for each coface $e$ of $v$. Then $H_1(M,\mathbb R)=0$.

Forman's idea comes from a simple observation. Though the classical Bochner-Weitzenb$\rm\ddot{o}$ck formula looks rather abstruse, with many abstract operators on Riemannian manifolds involved, but from the simplest perspective, one has
$$
\text{Laplacian}=\text{nonnegative definite operator}+\text{curvature}
$$

For a simplicial complex $M$ the discrete Laplacian is well defined. i.e. Let $\partial_p:C_p(M;\mathbb R)\to C_{p-1}(M;\mathbb R)$ be the $p$th boundary operator. Place a metric on each chain vector space by declaring the simplices are orthogonal (*It is not necessary that they are orthonormal. Note that when simplices are assigned weights the adjoint operator is no longer the transpose*).  The boundary operator admits an adjoint $\partial_p^\*:C_{p-1}(M;\mathbb R)\to C_p(M;\mathbb R)$, such that $\langle\partial_p\alpha,\beta\rangle_{p-1}=\langle\alpha,\partial_p^\*\beta\rangle_p$. The *combinatorial Laplacian* is defined by 
$$
\square_p=\partial_{p+1}\partial_{p+1}^*+\partial_p^*\partial_p:C_p(M;\mathbb R)\to C_p(M;\mathbb R)
$$
From equation (8) we know we want to decompose $\square_p$ as a sum of a nonnegative definite matrix $B_p$ and a curvature-type matrix $F_p$. In fact we only need to construct $B_p$, since we do not know any property of $F_p$ so that we just put $F_p=\square_p-B_p$.

The way Forman defined $B_p$ is quite natural. Suppose $A$ is a symmetric matrix. Then 
$$
\mathbb{B}(A)=\left\{\begin{array}{l}A_{ij},\text{ for }i\neq j\\ \sum_{j\neq i} |A_{ij}|,\text{ for }i=j\end{array}\right.
$$
is a diagonally dominant matrix, thus is nonnegative definite. $\mathbb B(A)$ is called the Bochner matrix associated to $A$. Thereafter $\mathbb F(A)=A-\mathbb B(A)$ is called the curvature matrix associated to $A$. From this perspective we see that 'curvature' measures how **a symmetric matrix deviates from a diagonally dominant matrix**. This decomposition is useful in our case because $\mathbb B(\square)$ preserves the topological (or combinatorial) information of the simplicial complex $M$. Specifically, if $\alpha$ and $\beta$ are parallel neighbors, then $\square_{\alpha\beta}=\mathbb B(A)_{\alpha\beta}\neq 0$ by checking definition. Let $B$ be a symmetric $n\times n$ matrix. Define an equivalence relation on $\{1,2,\cdots,n\}$ by requiring $i\sim i$ and $i\sim j$ if and only if there is a sequence $i=k_0,k_1,\cdots,k_n=j$ such that $B(k_l,k_{l+1})\neq 0$. Let $\mathcal C(B)$ be the set of equivalence classes and $\mathcal N(B)=|\mathcal C(B)|$. The following nontrivial property of diagonally dominant matrices is used by Forman to prove Bochner's theorem for 1-chains.

> Let $B$ be a diagonally dominant metrix, then
>
> 1. $\text{dim(ker)}(B)\le \mathcal N(B)$;
> 2. Suppose $v=(v_1,\cdots,v_n)\in\text{ker}(B)$, if $B_{ij}\neq 0$, $v_j=-sign(B_{ij})v_i$. i.e. the components in the same equivalence class are completely determined at one element.

It suffices to prove 2. Let $c\in\mathcal C(B)$ be any class. Without loss of generality, assume $v_i=\max_{j\in c}|v_j|\ge0$. Then we have 
$$
0=(Bv)_i=\sum_{j}B_{ij}v_j=B_{ii}v_i+\sum_{j\in c,j\neq i}B_{ij}v_j\ge\sum_{j\in c,j\neq i}|B_{ij}|(v_i-|v_j|)\ge0
$$
The equality holds if and only if $v_j=0$ for all $j\in c$,  or, $B_{ii}=\sum_{j\neq i}|B_{ij}|$ and $v_j=-sign(B_{ij})v_i$ for all $j\neq c$. 

Recall that for graph Laplacian $L=D-A$ the dimension of kernel is always equal to the connected components. This is because the constant vector $\mathbf{1}$ provides a nontrivial element in the kernel if the graph is connected. However, one can easily construct an invertible matrix $B$ with the diagonal equal to the sum of off-diagonal elements. Thus the first inequality can be strict.

Let us see how this property can be used in our case. Suppose $\alpha$ and $\beta$ are parallel $p$-neighbors, which implies $\square_p(\alpha,\beta)\neq 0$ and thus $\mathbb{B}(\square_p)(\alpha,\beta)\neq 0$. If there is a $p$-chain $c=\sum c_\gamma\gamma\in\text{Ker}(\mathbb{B}(\square_p))$ with $c_\alpha=0$, then $c_\beta=0$. This continuation property will be important in the proof of Bochner-type theorems.

Now suppose $\mathbb{F}(\square_p)$ is nonnegative definite, which is equivalent to say $\mathbb{F}(\square_p)_{ii}\ge 0$. Being a sum of two nonnegative definite matrices, we have $\text{Ker}(\square_p)=\text{Ker}(\mathbb{B}(\square_p))\cap\text{Ker}(\mathbb{F}(\square_p))$. In the simplest case, suppose $\mathbb{F}(\square_p)$ is positive definite, then $\text{Ker}(\square_p)=\{0\}$. For $p=1$, we have the familiar statement: if $M$ has positive Ricci curvature (at present call $\mathbb{F}(\square_1)$ the Ricci curvature, which is positive if the diagonal elements are positive), then $H_1(M;\mathbb R)$ is trivial. 

More generally, assume $M$ has nonnegative Ricci curvature and there is a vertex $v$ such that $\text{Ric}(e)>0$ for all $e\succ v$. Let $c=\sum c_e e\in\text{Ker}(\square_1)=\text{Ker}(\mathbb{B}(\square_1))\cap\text{Ker(Ric)}$. Since $c\in\text{Ker(Ric)}$ we have $c_e=0$ for all $e\succ v$. The following lemma shows that $c$ will be identically zero.

> Suppose $c=\sum c_e e$ is a 1-chain such that $c\in\text{Ker}(\partial^\*)\cap\text{Ker}(\mathbb{B}(\square_1))$. In addition, there is a vertex $v$ with $c_e=0$ for all $e\succ v$. Then $c=0$.

Define $D:\{\text{1-simplices}\}\to\mathbb{Z}_{\ge 0}$ as: (1). $D(e)=0$ for $e\succ v$; (2). Inductively, if $D(e)$ is greater than $k$ and there is a 1-simplex $e_1$ such that $e\cap e_1\neq\emptyset$ and $D(e_1)=k$, set $D(e)=k+1$. 

From hypothesis $c_e=0$ for $D(e)=0$. Suppose $c_e=0$ for all $D(e)\le k$. Let $e$ be a 1-simplex with $D(e)=k+1$. Then there exists 1-simplex $e_1$ such that $D(e_1)=k$ and $e\cap e_1\neq \emptyset$. If $e$ and $e_1$ are parallel, by the continuation property of $\mathbb{B}(\square_1)$, $c_e=0$. If $e$ and $e_1$ are not parallel, there is a 2-simplex $f$ such that $f\succ e$ and $f\succ e_1$. Let the last edge of $f$ be $e_2$. Since $D(e_1)=k$, either $D(e)=k$ or $D(e_2)=k$. By assumption $D(e_2)=k$, thus $c_{e_1}=c_{e_2}=0$. Then 
$$
\langle\partial f,c\rangle=\langle f,\partial^*c\rangle=0=\pm c_e\langle e,e\rangle
$$
Hence $c=0$ by induction.

Now we give the explicit representation of $\square_p$ and the curvature function $\mathcal F_p$.

For each $(p+1)$-simplex $\beta$ with $\partial\beta=\sum_{\alpha\prec\beta}\epsilon_{\alpha\beta}\alpha$ where $\epsilon_{\alpha\beta}=\pm 1$ according to the orientation of $\beta$. By definition, $\langle\partial^\*\alpha,\beta\rangle=\langle\alpha,\partial\beta\rangle=\epsilon_{\alpha\beta}w_\alpha$ where we assume that $\langle\alpha,\alpha\rangle=w_\alpha$. Thus $\partial^\*\alpha=\sum_{\beta\succ\alpha}\epsilon_{\alpha\beta}\frac{w_\alpha}{w_\beta}\beta$. This gives
$$
\square_p\alpha_1=\sum_{\alpha_2}[\sum_{\beta\succ\alpha_1,\alpha_2}\epsilon_{\alpha_1\beta}\epsilon_{\alpha_2\beta}\frac{w_{\alpha_1}}{w_\beta}+\sum_{\gamma\prec\alpha_1,\alpha_2}\epsilon_{\gamma\alpha_1}\epsilon_{\gamma\alpha_2}\frac{w_\gamma}{w_{\alpha_2}}]\alpha_2
$$
We may work on orthonormal basis. Note that for different basis the definition of curvature will be different. Let $\alpha^\*=\alpha/\sqrt{w_\alpha}$. Then 
$$
\langle\square_p\alpha_1^*,\alpha_2^*\rangle=\sum_{\beta\succ\alpha_1,\alpha_2}\epsilon_{\alpha_1\beta}\epsilon_{\alpha_2\beta}\frac{\sqrt{w_{\alpha_1}w_{\alpha_2}}}{w_\beta}+\sum_{\gamma\prec\alpha_1,\alpha_2}\epsilon_{\gamma\alpha_1}\epsilon_{\gamma\alpha_2}\frac{w_\gamma}{\sqrt{w_{\alpha_2}w_{\alpha_1}}}
$$
Denote by $\square_p(\alpha_1^\*,\alpha_2^\*)$. Then under orthonormal basis, the curvature matrix is 
$$
\mathbb{F}(\square_p)(\alpha_1^*,\alpha_2^*)=\left\{\begin{array}{l}0,\text{ if }\alpha_1\neq\alpha_2\\ \square_p(\alpha_1^*,\alpha_2^*)-\sum_{\alpha^*\neq\alpha_2^*}|\square_p(\alpha^*,\alpha_1^*)|,\text{ if }\alpha_1=\alpha_2\end{array}\right.
$$
Define the $p$th curvature function by $\mathcal{F}_p(\alpha)=w_\alpha\mathbb{F}(\square_p)(\alpha^\*,\alpha^\*)$. Thus
$$
\begin{aligned}\mathcal{F}_p(\alpha)=w_\alpha(&\sum_{\beta\succ\alpha}\frac{w_\alpha}{w_\beta}+\sum_{\gamma\prec\alpha}\frac{w_\gamma}{w_\alpha}\\ &-\sum_{\eta\neq\alpha}|\sum_{\beta\succ\alpha,\eta}\epsilon_{\alpha\beta}\epsilon_{\eta\beta}\frac{\sqrt{w_{\alpha}w_{\eta}}}{w_\beta}+\sum_{\gamma\prec\alpha,\eta}\epsilon_{\gamma\alpha}\epsilon_{\gamma\eta}\frac{w_\gamma}{\sqrt{w_{\alpha}w_{\eta}}}|)\end{aligned}
$$
When $p=1$ and all weights are 1, the formula simplifies as what is given in the beginning. 