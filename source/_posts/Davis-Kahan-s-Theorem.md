---
title: Davis-Kahan Theorem
date: 2021-01-12 08:23:14
tags:
- Perturbation Theory
- Matrix Analysis
categories: Matrix-Analysis
---

## Problem Statement
Let $A$ be an $n\times n$ Hermitian matrix, and suppose we have the following spectral decomposition for $A$

$$
A=\sum_{i=1}^n\lambda_iu_iu_i^*
$$

where $\lambda_i$'s are eigenvalues of $A$ (*we do not need to sort eigenvalues here*), and $u_i$'s are corresponding eigenvectors and $u^*_i$ denotes conjugate transpose. Now, suppose $H$ is also an $n\times n$ Hermitian matrix that represents some perturbation added to $A$. The spectral decomposition for $A+H$ is

$$
A+H=\sum_{i=1}^n\mu_iv_iv_i^*
$$

We want to know 

- (1) the error bound for eigenvalues $\lambda_i$ and $\mu_i$;
- (2) the error bound for eigenvectors $u_i$ and $v_i$. 

It is worth thinking whether above two problems are **well-defined**. In fact, a critical thing is how to 'match' the original eigen-value/vector and the corresponding perturbed eigen-value/vector. For the first problem, we can sort the eigenvalues and match them according to the order. For the second problem, however, the situation is more intricate: think about two different eigenvalues that become equal after perturbation. Then any vector in the two-dimensional eigenspace will be an eigenvector corresponding to the new eigenvalue. Therefore, it is natural to place some assumptions on eigengaps to separate different eigenspaces.

Define
$$
P=\sum_{i=1}^ku_iu_i^*=UU^*
$$
to be the orthogonal projection operator to the $k$-dimensional eigenspace spanned by $u_1,\cdots,u_k$. Let
$$
P_\perp=I-P=\sum_{i=k+1}^nu_iu_i^*=U_\perp U_\perp^*
$$
Similarly, define
$$
Q=\sum_{i=1}^kv_iv_i^*=VV^*
$$
and $Q_\perp=I-Q$. The second problem can be generalized to 

- (2*) the error bound for projections $P$ and $Q$.

We focus on the generalized problem.

## Principal Angles

Recall that for nonzero vectors $x$ and $y$ we define their angles to be

$$
\angle x,y = \text{arccos} \frac{x^*y}{\|x\|\|y\|}
$$

The range for angles between two vectors is $[0,\pi]$. Recall that in affine geometry we have defined angles between lines and planes: we define the angle between $\mathbb{R}x$ and $\mathbb{R}y$ to be

$$
\angle \mathbb{R}x,\mathbb{R}y = \text{arccos} \frac{|x^*y|}{\|x\|\|y\|} = \inf_{a,b\in\mathbb{R}}\text{arccos} \frac{(ax)^*(by)}{\|ax\|\|by\|}
$$

Suppose $y$ and $z$ span a two-plane $\mathbb{R}\{y,z\}$. The angle between $\mathbb{R}x$ and $\mathbb{R}\{y,z\}$ is defined as

$$
\angle \mathbb{R}x,\mathbb{R}\{y,z\} = \angle \mathbb{R}x,\mathbb{R}(yy^*+zz^*)x = \inf_{a,b,c\in\mathbb{R}}\text{arccos}\frac{(ax)^*(by+cz)}{\|ax\|\|by+cz\|}
$$

Now we want to define angles between two vector spaces. Suppose $E=\mathbb{C}\{e_1,\cdots,e_r\}$ and $F=\mathbb{C}\{f_1,\cdots,f_s\}$ are two vector spaces, we define

$$
\angle E,F = \inf_{e\in E,f\in F}\text{arccos}\frac{e^*f}{\|e\|\|f\|}
$$

With a bit abuse of notation, we let $E$ denote the matrix $[e_1,\cdots,e_r]$ and similarly let $F$ denote $[f_1,\cdots,f_s]$. If we write

$$
e=E\alpha,\quad f=F\beta
$$

where $\alpha$ and $\beta$ are unit vectors. Then we see that 

$$
\angle E,F = \inf_{\alpha,\beta}\text{arccos}(\alpha^*E^*F\beta)=\text{arccos}(\lambda_{\max}(E^*F))
$$

where $\lambda_{\max}$ denotes the largest singular value. Since we have seen that the angle between two vector spaces is related to the singular value, it will be helpful to consider all the singular values instead of the largest one. We call each
$$
\theta_i=\text{arccos}\lambda_i(E^*F)
$$
the principal angle between $E$ and $F$. Note that each principal angle is between $[0,\pi/2]$. Define the following matrix
$$
\Theta_{E,F}=\text{arccos}(E^*F)
$$

where $\text{arccos}$ acts on singular values in the singular decomposition. Though in general cases $\Theta_{E,F}\neq \Theta_{F,E}$, in the following discussion we only focus on $\sin(\Theta)$ whose nonzero singular values are equal for $\sin(\Theta_{E,F})$ and $\sin(\Theta_{F,E})$.   Now we have prepared to look at the Davis-Kahan theorem. 

## Davis-Kahan's $\sin(\Theta)$ Theorem

Back to our set-up, we want to compare two projection matrices $P$ and $Q$. Using the Frobenius norm for matrices, we have

$$
\|P-Q\|_{F}^2=\text{tr}((P-Q)^2)=2k-2\text{tr}(PQ)
$$

Note that
$$
\text{tr}(PQ)=\|U^*V\|_F^2=\|\cos(\Theta_{U,V})\|^2_F
$$
Therefore, we have
$$
\|P-Q\|_F=\sqrt{2}\|\sin(\Theta_{U,V})\|_F
$$

To bound the error between two projection matrices, it suffices to bound $\|\sin(\Theta_{U,V})\|_F$.

We write the eigen-decomposition for $A$ with respect to $U$ and $U_\perp$ as

$$
A = [U,U_\perp]\left[\begin{array}{cc}
    \Lambda & 0\\
    0 & \Lambda_\perp
\end{array}\right]\left[\begin{array}{c}
    U^*\\ U^*_\perp
\end{array}\right]
$$

where $\Lambda$ is the diagonal matrix consisting of eigenvalues $\lambda_1,\cdots,\lambda_k$ whereas $\Lambda_\perp$ consists of eigenvalues $\lambda_{k+1},\cdots,\lambda_n$. Similarly, write the eigen-decomposition for $A+H$ with respect to $V$ and $V_\perp$ as

$$
A+H = [V,V_\perp]\left[\begin{array}{cc}
    M & 0\\
    0 & M_\perp
\end{array}\right]\left[\begin{array}{c}
    V^*\\ V^*_\perp
\end{array}\right]
$$

Finally, we write $H$ in the following form

$$
H = [U,U_\perp]\left[\begin{array}{cc}
    H_0 & B\\
    B^* & H_1
\end{array}\right]\left[\begin{array}{c}
    U^*\\ U^*_\perp
\end{array}\right]
$$

so that under the basis $[U,U_\perp]$, we have

$$
A+H = [U,U_\perp]\left[\begin{array}{cc}
    \Lambda+H_0 & B\\
    B^* & \Lambda_\perp+H_1
\end{array}\right]\left[\begin{array}{c}
    U^*\\ U^*_\perp
\end{array}\right]
$$

Since our focus is the eigenspace spanned by $u_1,\cdots,u_k$, define the following residual

$$
\begin{aligned}
R =& (A+H)U-AU=UH_0+U_{\perp} B^*\\
=& VM V^*U+V_\perp M_\perp V_\perp^*U-U\Lambda
\end{aligned}
$$

If we multiply $V_\perp^*$ on the left, we have

$$
V_\perp^*R=M_\perp V_\perp^*U-V_\perp^*U\Lambda
$$

Note that $M_\perp$ and $\Lambda$ are nonnegative diagonal matrices. For Frobenius norm we have the following lemma

> Suppose $D$ is a nonnegative diagonal matrix whose largest and smallest elements are $d_{\max}$ and $d_{\min}$, respectively. Then we have $d_{\min}\|X\|_F\le \|DX\|_F\le d_{\max}\|X\|_F$.

This lemma inspires us to place some assumption on gaps between $M_\perp$ and $\Lambda$ to obtain a bound for $R$. It coincides with our intuition: In most cases we often assume that there is some eigengap between $\Lambda$ and $\Lambda_\perp$. After a small perturbation $H$, we may expect $M_\perp$ is close to $\Lambda_\perp$. Now if there is still a gap between $\Lambda$ and $M_\perp$, we believe that the original projection is close to the perturbed projection. So, we may assume the following

> Suppose there exists some $\delta>0$ such that $|\lambda_i-M_j|>\delta$ for all $i=1,\cdots,k$ and $j=k+1,\cdots,n$.

Under this assumption we see that 

$$
\|R\|_F\ge\|V_\perp^*R\|_F\ge \delta\|V_\perp^*U\|_F
$$

However, $\|V^*_\perp U\|_F$ is nothing but $\|\sin(\Theta_{U,V})\|_F$. To see that, we have

$$
\|V_\perp^*U\|_F^2=\text{tr}(P(I-Q))=k-\text{tr}(PQ)=\|\sin(\Theta_{U,V})\|_F^2
$$

Thus we obtain the so-called Davis-Kahan's $\sin(\Theta)$ theorem

$$
\|P-Q\|_F\le \frac{\sqrt{2}\|R\|_F}{\delta}\le \frac{\sqrt{2}\|H\|_F}{\delta}
$$

If we are interested in the spectral norm, apply the inequality $\|R\|_F\le \sqrt{k}\|R\|_{op}$, and note that $\|R\|_{op}\le\|H\|_{op}$. So we also have

$$
\|P-Q\|_{op}\le \|P-Q\|_F\le \frac{\sqrt{2k}\|H\|_{op}}{\delta}
$$

It is also possible to make assumptions on gaps between $\Lambda_\perp$ and $M$. Consider another residual

$$
\begin{aligned}
R_\perp =& (A+H)U_\perp-AU_\perp=UB+U_\perp H_1\\
=& VM V^*U_\perp+V_\perp M_\perp V_\perp^*U_\perp-U_\perp \Lambda_\perp
\end{aligned}
$$

Multiply $V^*$ on the left

$$
V^*R_\perp = M V^*U_\perp-V^*U_\perp\Lambda_\perp
$$

But what is $\|V^*U_\perp\|_F$? The computation shows that 

$$
\|V^*U_\perp\|_F^2=\text{tr}(Q(I-P))=k-\text{tr}(PQ)=\|\sin(\Theta_{U,V})\|_F^2
$$

Thus we come to the same conclusion.

## Generalizations

A defect in Davis-Kahan's theorem is that we need to compare either $\Lambda$ with $M_\perp$ or $\Lambda_\perp$ with $M$. However, in practice (especially in statistics where $A$ usually stands for some population matrix and $H$ stands for random noises), it is more reasonable to assume a priori comparison between $\Lambda$ and $\Lambda_\perp$. Can we change the assumption but still keep the same error bound? The answer is YES. It is noted by [this paper](http://www.statslab.cam.ac.uk/~rjs57/Biometrika-2015-Yu-315-23.pdf) that the theorem also holds if we only assume an eigengap on $A$. The proof is straightforward: without perturbation we have $AU=U\Lambda$. After perturbation we want to know the residual $L=AV-V\Lambda$. On the one hand,

$$
L=AV-V\Lambda+HV-HV=V(M-\Lambda)-HV
$$

Using [Wielandt-Hoffman theorem](http://i.stanford.edu/pub/cstr/reports/cs/tr/70/150/CS-TR-70-150.pdf) we have

$$
\|L\|_F\le \|V(M-\Lambda)\|_F+\|HV\|_F\le 2\|H\|_F
$$

On the other hand, using the eigen-decomposition for $A$, we have

$$
L=U\Lambda U^*V+U_\perp\Lambda_\perp U_\perp^*V-V\Lambda
$$

Note that
$$
V\Lambda=(P+P_\perp)V\Lambda=UU^*V\Lambda+U_\perp U_\perp^*V\Lambda
$$
Thus,
$$
L=U(\Lambda U^*V-U^*V\Lambda)+U_\perp(\Lambda_\perp U_\perp^*V-U_\perp^*V\Lambda)
$$

Since $U$ and $U_\perp$ are orthogonal, we have

$$
\|L\|_F\ge \|\Lambda_\perp U_\perp^*V-U_\perp^*V\Lambda\|_F
$$

Now if we assume

> $|\lambda_i-\lambda_j|\ge \delta>0$ for all $i=1,\cdots,k$ and $j=k+1,\cdots,n$.

from the above discussions it holds

$$
\delta \|\sin(\Theta_{U,V})\|_F\le \|L\|_F\le 2\|H\|_F
$$

If we are interested in the spectral norm, control $\|L\|_F$ by $2\sqrt{k}\|H\|_{op}$. So it holds

$$
\|\sin(\Theta_{U,V})\|_F\le \frac{2\min\{\sqrt{k}\|H\|_{op},\|H\|_F\}}{\delta} 
$$

if $k=1$, obviously $\|H\|_{op}\le\|H\|_F$. Hence,

$$
\|\sin(\Theta_{U,V})\|_F\le \frac{2\|H\|_{op}}{\delta}
$$

One may also consider the generalization of Davis-Kahan theorem to rectangular matrices. It is not hard if we notice that for any matrix $A$, 

$$
A^*A \text{ and } AA^*
$$

are Hermitian matrices, and their eigenvalues are nothing but the square of singular values. The only thing to take care of is that we need to relate 

$$
\widehat{A}^*\widehat{A}-A^*A \text{ and } \widehat{A}\widehat{A}^*-AA^*
$$

with $\widehat{A}-A=H$. This is done by the following

$$
\begin{aligned}
    \|\widehat{A}^*\widehat{A}-A^*A\|_{op}=&\|(\widehat{A}-A)^*\widehat{A}+A^*(\widehat{A}-A)\|_{op}\\
    \le & (\|\widehat{A}\|_{op}+\|A\|_{op})\|\widehat{A}-A\|_{op}\\
    \le & (2\|A\|_{op}+\|A-\widehat{A}\|_{op})\|\widehat{A}-A\|_{op}\\
    \|\widehat{A}^*\widehat{A}-A^*A\|_F=&\|(\widehat{A}-A)^*\widehat{A}+A^*(\widehat{A}-A)\|_{F}\\
    \le & \|(\widehat{A}-A)^*\widehat{A}\|_F+\|A^*(\widehat{A}-A)\|_F\\
    =& \|(\widehat{A}^*\otimes I)vec(\widehat{A}-A)\|+\|(I\otimes A^*)vec(\widehat{A}-A)\|\\
    \le & (\|\widehat{A}\|_{op}+\|A\|_{op})\|vec(\widehat{A}-A)\|\\
    \le & (2\|A\|_{op}+\|A-\widehat{A}\|_{op})\|\widehat{A}-A\|_{F}\\
\end{aligned}
$$

Alternatively, for any $A\in\mathbb{R}^{m\times n}$, we can define the $(m+n)\times (m+n)$ matrix

$$
\tilde{A}=\left[\begin{array}{cc}
    0 & A\\
    A^*&0
\end{array}\right]\text{ and }
\tilde{H}=\left[\begin{array}{cc}
    0 & H\\
    H^*&0
\end{array}\right]
$$

If $Av=\sigma u$ Then

$$
\tilde{A}\left[\begin{array}{c}
    u\\
    v
\end{array}\right]=\sigma \left[\begin{array}{c}
    u\\
    v
\end{array}\right]\text{ and }
\tilde{A}\left[\begin{array}{c}
    u\\
    -v
\end{array}\right]=-\sigma \left[\begin{array}{c}
    u\\
    -v
\end{array}\right]
$$

Therefore, the non-zero eigenvalues of $\tilde{A}$ are the positive and negative of singular values of $A$, and the eigenvectors are formed by the left and right singular vectors of $A$. Note that $\tilde{A}$ and $\tilde{H}$ are Hermitian matrices, which implies we can use Davis-Kahan theorem directly. The only thing we should take care of is that we need to relate $\sin(\tilde{\Theta})$ with $\sin(\Theta_u)$ and $\sin(\Theta_v)$. A typical model is stated as follows.

Let
$$
\tilde{u}=\left[\begin{array}{c}
    u_1\\
    u_2
\end{array}\right]\text{ and }
\tilde{v}=\left[\begin{array}{c}
    v_1\\
    v_2
\end{array}\right]
$$

Note that $\|u_i\|=\|v_i\|=1$ so $\|\tilde{u}\|=\|\tilde{v}\|=2$. Then

$$
\cos^2(\tilde{u},\tilde{v})=\frac{1}{4}|\tilde{u}\cdot\tilde{v}|^2\le\frac{1}{2}\cos^2(u_1,v_1)+\frac{1}{2}\cos^2(u_2,v_2)
$$

Therefore,

$$
\sin^2(\tilde{u},\tilde{v})\ge \frac{1}{2}\sin^2(u_1,v_1)+\frac{1}{2}\sin^2(u_2,v_2)
$$


The first generalization to singular spaces is carried out by [Wedin](https://www.semanticscholar.org/paper/Perturbation-bounds-in-connection-with-singular-Wedin/133c76f0d580e09de0ca28ff0fb599d5e57321f8). Thus Davis-Kahan theorem is also called Davis-Kahan-Wedin theorem in literature. 

## A Final Remark

In Davis and Kahan's [original paper](https://epubs.siam.org/doi/10.1137/0707001), they actually proved four types of theorems. Except for the $\sin(\Theta)$ theorem, the remaining three are: (1) $\sin(2\Theta)$ theorem; (2) $\tan(\Theta)$ theorem; (3) $\tan(2\Theta)$ theorem. For $2\Theta$ theorems, they allow the principal angle to be close to either 0 or $\pi/2$. It seems that $2\Theta$ theorems are more general. However, it is rather difficult to find practical applications. 