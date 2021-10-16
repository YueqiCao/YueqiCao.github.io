---
title: Tangent Space Estimation Using Local PCA
date: 2020-05-21 16:13:57
tags:
- Submanifolds
- Asymptotic Analysis
categories:
- Manifold-Learning
---

In [this paper](https://arxiv.org/abs/1102.0075), A.Singer and H.-T. Wu derived an explicit expression for the bias and variance of local PCA in tangent space estimation. One thing to notice: when we have estimated a basis $\widehat{E}$ and want to compare with the true basis $E$, we can either

- consider the error between two projection operators $\|\widehat{E}\widehat{E}^T-EE^T\|$, 

or 

- consider the error up to rotation $\min_{O}\|O\widehat{E}-E\|$.

However, according to the original paper, the convergence rates for above two errors are different. Moreover, the authors did not claim the choice of bandwidth is optimal. So other choices of bandwidth may also by possible. 

Let $\mathcal{M}$ be an $m$-dimensional compact submanifold in a Euclidean space $\mathbb{R}^d$. Fix $x\in\mathcal{M}$. Without loss of generality assume that $x$ is placed at the origin and the tangent space $T_x\mathcal{M}$ coincides with the coordinate space spanned by the first $m$ standard vectors $\{e_1,\cdots,e_m\}$ in $\mathbb{R}^d$. Suppose $X$ is a random vector valued in $\mathcal{M}$ with a smooth positive density function $f:\mathcal{M}\to \mathbb{R}$. Let $K:\mathbb{R}\to\mathbb{R}$ be a smooth function supported on $[0,1]$ and $h>0$ be a positive number. To estimate the tangent space at $x$, we start by finding a direction $v$ such that the projection to $v$ is maximized
$$
\mathbb{E}[((X-x)\cdot v)^2K_h(X-x)]
$$
where $K_h:\mathbb{R}^d\to\mathbb{R}$ is the function $K_h(u)=1/h^mK(\|u\|/h)$. Therefore, we consider the following Lagrange function
$$
f(v)=\mathbb{E}[((X-x)\cdot v)^2K_h(X-x)]-\lambda(\|v\|-1)
$$
Setting $df/dv=0$ we have $\mathbb{E}[(X-x)(X-x)^tK_h(X-x)]v=\lambda v$ and the objective function is $\lambda$. Thus we choose the eigenvector of $\mathbb{E}[(X-x)(X-x)^tK_h(X-x)]$ with respect to the largest eigenvalue. 

Next, we proceed by finding another direction $v'$ orthogonal to $v$ such that the same objective function is maximized. The result turns out that the optimal $v'$ is the eigenvector of $\mathbb{E}[(X-x)(X-x)^tK_h(X-x)]$ of the second largest eigenvalue.  Iteratively, to estimate the tangent space $T_x\mathcal{M}$ we attempt to find the first $m$ eigenvectors of the matrix $\mathbb{E}[(X-x)(X-x)^tK_h(X-x)]$. We set 
$$
\mathbb{H}=\mathbb{E}[(X-x)(X-x)^tK_h(X-x)]
$$
and call it the **population covariance matrix**. In practice, $\mathbb{H}$ is not available. Suppose $X_1,\cdots,X_n$ are i.i.d. samples of $X$.  Then we can replace $\mathbb{H}$ by the empirical mean,
$$
H=\frac{1}{n}\sum_{i=1}^n(X_i-x)(X_i-x)^tK_h(X_i-x)
$$
which is called the **empirical covariance matrix**. Note that these are not in fact covariance matrices since the mean is forced to be $x$. But it will bring technical convenience for our analysis. We first give a detailed analysis of the covariance matrices.

For $h$ small enough, the contributed points will lie in a normal patch of $x$. Hence we can use the exponential map. Suppose $X=\exp_x(s_X\theta_X)$ where $\|\theta_X\|=1$. Then 
$$
X-x=s_X\theta_X+\frac{1}{2}\Pi(\theta_X,\theta_X)s_X^2-\frac{1}{6}A_{\Pi(\theta_X,\theta_X)}(\theta_X)s^3+\frac{1}{6}(\nabla_{\theta_X}\Pi)(\theta_X,\theta_X)s^3+o(s^3)
$$
Thus we have the following expansion for $\mathbb{H}$,
$$
\begin{aligned}
\mathbb{H}=&\underbrace{\mathbb{E}[(\theta_X\theta_X^ts_X^2-\frac{1}{6}(\theta_XA_\Pi^t+A_\Pi^t\theta_X)s_X^4+o(s^4_X))K_h(X-x)]}_{\mathbf{H}}\\
+&\underbrace{\mathbb{E}[(\frac{1}{2}(\theta_X\Pi^t+\Pi\theta_X^t)s_X^3+\frac{1}{6}(\theta_X(\nabla\Pi)^t+(\nabla\Pi)\theta^t)s_X^4+o(s_X^4))K_h(X-x)]}_{\mathbf{B}_r}\\
+&\underbrace{\mathbb{E}[(\frac{1}{4}\Pi\Pi^ts^4)K_h(X-x)]}_{\mathbf{B}_s}
\end{aligned}
$$
Note that $\mathbf{H}$, $\mathbf{B}_r$ and $\mathbf{B}_s$ are blocked matrices. i.e.
$$
\mathbf{H}=\left[\begin{array}{cc}*&0\\0&0\end{array}\right],\mathbf{B}_r=\left[\begin{array}{cc}0&*\\*&0\end{array}\right],\mathbf{B}_s=\left[\begin{array}{cc}0&0\\0&*\end{array}\right]
$$
Call $\mathbf{H}$ the true covariance matrix since the eigenvectors of $\mathbf{H}$ will give the true basis of the tangent space. $\mathbf{B}_r$ and $\mathbf{B}_s$ will called the basis matrices and we see from the expansion that the bias comes from the curvature of the manifold $\mathcal{M}$. 

Integration in the normal patch gives the leading terms of each matrices. Note that odd terms of $\theta$ will vanish. Therefore,
$$
\mathbf{H}=\left[\begin{array}{cc}ch^2I+O(h^4)&0\\0&0\end{array}\right],\mathbf{B}_r=\left[\begin{array}{cc}0&O(h^4)\\O(h^4)&0\end{array}\right],\mathbf{B}_s=\left[\begin{array}{cc}0&0\\0&O(h^4)\end{array}\right]
$$
Thus the bias deviates from the true matrix will be of order $O(h^4)$.

Then we consider the variance coming from $\mathbb{H}$ and $H$. By definition, $\mathbb{E}[H]=\mathbb{H}$. Thus we may write
$$
H=\mathbb{H}+V
$$
where $\mathbb{E}[V]=0$. For each element in $V$, the variance is
$$
\mathbb{Var}[V(i,j)]=\mathbb{E}[(H(i,j)-\mathbb{H}(i,j))^2]\le\frac{1}{n}\mathbb{E}[(X-x)_i^2(X-x)^2_jK^2_h(X-x)]
$$
By computation the second moments are given by
$$
\mathbb{E}[(X-x)_i^2(X-x)_j^2K_h(X-x)]=\left\{\begin{array}{l}O(\frac{h^4}{h^m})\quad i,j=1,\cdots,m\\ O(\frac{h^8}{h^m})\quad i,j=m+1,\cdots,d\\ O(\frac{h^6}{h^m})\quad \text{otherwise}\end{array}\right.
$$
Therefore, the variance matrix is given by
$$
\mathbb{Var}[V(i,j)]=\left\{\begin{array}{l}O(\frac{h^4}{nh^m})\quad i,j=1,\cdots,m\\ O(\frac{h^8}{nh^m})\quad i,j=m+1,\cdots,d\\ O(\frac{h^6}{nh^m})\quad \text{otherwise}\end{array}\right.
$$
Using Chebyshev's inequality, we see that for any $\epsilon>0$,
$$
\mathbb{Pr}\{|H(i,j)-\mathbb{H}(i,j)|>\epsilon\}\le\frac{\mathbb{Var}(V(i,j))}{\epsilon^2}
$$
If we set the right hand side to be $O(1)$, then with high probability $V(i,j)=O(\epsilon)$. Following this principle, with high probability, $V$ is in the following form
$$
V=\frac{h^2}{\sqrt{nh^m}}\left[\begin{array}{cc}O(1)& O(h)\\O(h)&O(h^2)\end{array}\right]
$$

Overall, we have shown that with high probability, 
$$
\begin{aligned}
\frac{1}{h^2}H=&c\left[\begin{array}{cc}I&0\\0&0\end{array}\right]+h^2\left[\begin{array}{cc}O(1)&O(1)\\O(1)&O(1)\end{array}\right]+\frac{1}{\sqrt{nh^m}}\left[\begin{array}{cc}O(1)&O(h)\\O(h)&O(h^2)\end{array}\right]
\end{aligned}
$$
If we set $O(\text{bias})=O(\text{variance})$, the *optimal bandwidth* $h=O(n^{-1/(m+4)})$. In this case we have
$$
H=h^2c\left[\begin{array}{cc}I+h^2A&h^2C\\h^2C^t&h^2B\end{array}\right]=h^2c(S+h^2T)
$$
where 
$$
S=\left[\begin{array}{cc}I&0\\0&0\end{array}\right], T=\left[\begin{array}{cc}A&C\\C^t&B\end{array}\right]
$$
Let $\mathbf{v}$ be an eigenvector of $S+h^2T$ with respect to the eigenvalue $\mathbf{\Lambda}$. Using the following expansion on both sides of $S\mathbf{v}=\mathbf{\Lambda}\mathbf{v}$,
$$
\begin{aligned}
&\mathbf{v}=v_0+h^2v_1+h^4v_2+\cdots\\
&\mathbf{\Lambda}=\lambda_0+h^2\lambda_1+h^4\lambda_2+\cdots
\end{aligned}
$$
and compare the coefficients on both sides. We have
$$
Sv_0=\lambda_0v_0
$$
which means that $\lambda_0=1$ and $v_0$ is in the form $[\bar{v}_0,0]^t$. For the first order term we have
$$
Sv_1+Tv_0=\lambda_0v_1+\lambda_1v_0
$$
Thus if we write $v_1=[\bar{v}_1,\tilde{v}_1]$ then $A\bar{v}_0=\lambda_1\bar{v}_0$ and $C^t\bar{v}_0=\tilde{v}_1$. For the second term, we have 
$$
Sv_2+Tv_1=v_2+\lambda_1v_1+\lambda_2v_0
$$
Then $A\bar{v}_1+C\tilde{v}_1=\lambda_1\bar{v}_1+\lambda_2\bar{v}_0$. Nothing will vanish after this step. Therefore, we have $\mathbf{v}=[\bar{v}_0,0]+O(h^2)$ and $\mathbf{\Lambda}=1+h^2\lambda_A+O(h^4)$. 

However, if we make the leading term of $A$ different from $B$ and $C$, that is, $O(\text{variance})>O(\text{bias})$ and the error mainly comes from sampling, the result will be different. As in the original paper we set $O(\text{variance})=O(h)$ which gives the sampling rate $h=O(n^{-1/(m+2)})$. In this case we have
$$
S=\left[\begin{array}{cc}I&0\\0&0\end{array}\right], T_1=\left[\begin{array}{cc}A&0\\0&0\end{array}\right], T_2=\left[\begin{array}{cc}0&C\\C^t&B\end{array}\right]
$$
By [Wielandt-Hoffman theorem](https://www.math.usm.edu/lambers/mat610/sum10/lecture13.pdf), the eigenvalues satisfy the following inequality
$$
\sum_{i=1}^d(\lambda_i(T_1+hT_2)-\lambda_i(T_1))^2\le\|hT_2\|_F^2
$$
Hence if we set the eigenvalues in descending order $\lambda_1\ge\lambda_2\ge\cdots\ge\lambda_d$, then $\lambda_k(T_1+hT_2)=\lambda_k^A+O(h)$ for $k=1,\cdots,m$ and $\lambda_l(T_1+hT_2)=O(h)$ for $k=m+1,\cdots,d$. 

For eigenvectors we use the same method as above. Suppose $\mathbf{v}$ is a unit eigenvector of $S+hT_1+hT_2$ corresponding to the eigenvalue $\mathbf{\Lambda}$. Using Taylor expansions for $\mathbf{v}$ and $\mathbf{\Lambda}$, 
$$
\begin{aligned}
&\mathbf{v}=v_0+hv_1+h^2v_2+h^3v_3+h^4v_4+O(h^5)\\
&\mathbf{\Lambda}=\lambda_0+h\lambda_1+h^2\lambda_2+h^3\lambda_3+h^4\lambda_4+O(h^5)
\end{aligned}
$$
and by the relation 
$$
(S+hT_1+h^2T_2)\mathbf{v}=\mathbf{\Lambda}\mathbf{v}
$$
we compare the coefficients on both sides. For the constants we have
$$
\begin{aligned}
&Sv_0=\lambda_0v_0
\end{aligned}
$$
which implies $\lambda_0=1$ and $v_0$ is in the form $[\bar{v}_0,0]^t$. For the first order term we have 
$$
Sv_1+T_1v_0=v_1+\lambda_1v_0
$$
which implies $v_1$ is also in the form $[\bar{v}_1,0]^t$, and $A\bar{v}_0=\lambda_1\bar{v}_0$. We see that $\bar{v}_0$ is an eigenvector of $A$. For the second order term we have
$$
T_2v_0+T_1v_1+Sv_2=v_2+\lambda_1v_1+\lambda_2v_0
$$
Note that $T_2v_0=[0,C^t\bar{v}_0]^t$. We see that the left side is $[A\bar{v}_1+\bar{v}_2,C^t\bar{v}_0]^t$ and the right side is $[\lambda_1\bar{v}_1+\lambda_2\bar{v}_0,0]^t+[\bar{v}_2,\tilde{v}_2]^t$. This gives $\tilde{v}_2=C^t\bar{v}_0$ and 
$$
A\bar{v}_1=\lambda_1\bar{v}_1+\lambda_2\bar{v}_0
$$
Multiplying both sides by $\bar{v}_0^t$, we have
$$
\lambda_1\bar{v}_0^t\bar{v}_1=\lambda_1\bar{v}_0^t\bar{v}_1+\lambda_2\bar{v}_0^t\bar{v}_0
$$
Thus, $\lambda_2=0$ and $A\bar{v}_1=\lambda_1\bar{v}_1$. If we assume the eigenvalues of $A$ are simple (as said in original paper it holds almost surely), then $\bar{v}_1=0$. For the third order term we have 
$$
Sv_3+T_1v_2+T_2v_1=v_3+\lambda_1v_2+\lambda_2v_1+\lambda_3v_0
$$
The left side is $[\bar{v}_3+A\bar{v}_2,0]^t$ and the right side is $[\bar{v}_3+\lambda_1\bar{v}_2+\lambda_3\bar{v}_0,\tilde{v}_3+\lambda_1\tilde{v}_2]$. Hence $\tilde{v}_3=-\lambda_1\tilde{v}_2$ and $A\bar{v}_2=\lambda_1\bar{v}_2+\lambda_3\bar{v}_0$. Using the same method as before we know that $\lambda_3=0$ and $\bar{v}_2=0$. For the fourth term we have
$$
Sv_4+T_1v_3+T_2v_2=v_4+\lambda_1v_3+\lambda_4v_0
$$
The left side is $[\bar{v}_4+A\bar{v}_3+C\tilde{v}_2,B\tilde{v}_2]^t$ and the right side is $[\bar{v}_4+\lambda_1\bar{v}_3+\lambda_4\bar{v}_0,\lambda_1\tilde{v}_3+\tilde{v}_4]^t$. Hence $\tilde{v}_4=B\tilde{v}_2-\lambda_1\tilde{v}_3$ and 
$$
A\bar{v}_3+CC^t\bar{v}_0=\lambda_1\bar{v}_3+\lambda_4\bar{v}_0
$$
We cannot cancel anything in this step. Overall we have shown that 
$$
\begin{aligned}
&\mathbf{v}=v_0+h^2v_2+h^3v_3+O(h^4)=[\bar{v}_0+\bar{v}_3h^3+O(h^4),\tilde{v}_2h^2+O(h^3)]\\
&\mathbf{\Lambda}=1+h\lambda_1+h^4\lambda_4+O(h^5)
\end{aligned}
$$
Suppose the first $m$ eigenvectors of $H$ are $u_1,\cdots,u_m$ and the eigenvectors of $A$ are $w_1,\cdots,w_m$. We have $u_k=[w_k+O(h^3),O(h^2)]^t$ for $k=1,\cdots,m$. Let $\mathbf{U}=[u_1,\cdots,u_m]$ be the $d\times m$ matrix and $\mathbf{O}=[w_1,\cdots,w_m]^t$ be the $m\times m$ orthogonal matrix. Furthermore, let $\mathbf{\Theta}=[e_1,\cdots,e_m]$ be the matrix consisting of $m$ standard basis of $\mathbb{R}^d$. We measure the deviation of the estimated $m$-plane spanned by $u_k$'s from $T_x\mathcal{M}$ by
$$
\min_{O\in O(m)} \|\mathbf{U}^t\mathbf{\Theta}-O\|_F\le\|\mathbf{U}^t\mathbf{\Theta}-\mathbf{O}\|_F=O(h^3)
$$
If we choose the optimal bandwidth, the order will be $O(h^2)$. Thus we see that by choosing 'non-optimal' bandwidth the convergence even become faster. However, from another perspective, if we want to find a rotation $\hat{O}$ such that the basis $Q=\mathbf{\Theta}\hat{O}$ is closest to $\mathbf{U}$, i.e. the error is measured by 
$$
\min_{\hat{O}\in O(m)}\|\mathbf{U}-\mathbf{\Theta}\hat{O}\|_F
$$
then the error is bounded by 
$$
\min_{\hat{O}\in O(m)}\|\mathbf{U}-\mathbf{\Theta}\hat{O}\|_F\le O(h^2)
$$
Then different bandwidths yield the same order of convergence. Note that the difference comes from the estimation of eigenvectors.

A final remark is that the method used above by comparing coefficients for different orders is not very strict, since it automatically assumes that there are no fractional order terms. Generalization to fractional order convergence needs further investigation. 

----

**Update:** In this [paper](https://arxiv.org/pdf/1512.02857.pdf) (appendix D theorem 38), a useful version of [Davis-Kahan](https://arxiv.org/pdf/1405.0680.pdf) theorem is stated as follows

> Let $O\in\mathbb{R}^{d\times d}$, $B\in\mathbb{R}^{m\times m}$ be positive semi-definite symmetric matrices such that 
> $$
> O=\left[\begin{array}{cc}B&0\\ 0&0\end{array}\right]+E
> $$
> Let $T_0$ be the vector space spanned by the first $m$ vectors of canonical basis and $T$ be the eigenspace spanned by the first $m$ eigenvectors of $O$. Then
> $$
> \angle (T_0,T)\le \frac{\sqrt{2}\|E\|_{op}}{\lambda_{\min}(B)}
> $$

Now we return back to the expression of $1/h^2H$, consider the decomposition
$$
\frac{1}{h^2}H=\left[\begin{array}{cc}cI+O(h^2)+O(\sqrt{nh^m})&0\\0&0\end{array}\right]+\left[\begin{array}{cc}0&O(h^2+\frac{h}{\sqrt{nh^m}})\\O(h^2+\frac{h}{\sqrt{nh^m}})&O(h^2)\end{array}\right]
$$
Note $\lambda_{\min}(cI+O(\cdot))\approx c$. Thus the convergence rate depends on the operator norm of the second matrix. If we set $1/\sqrt{nh^m}=h^\alpha$ where $0<\alpha<1$, then the rate is $O(h^{1+\alpha})$. If $\alpha\ge 1$, the rate is $O(h^2)$. 

---

**Update:** [This blog](https://djalil.chafai.net/blog/2011/12/03/the-hoffman-wielandt-inequality/) gives a very nice introduction to Wielandt-Hoffman inequality. The proof is short and readable. I also write a new blog on Davis-Kahan's $\sin(\Theta)$ theorem. See [this page](http://yueqicao.top/2021/01/12/Davis-Kahan-s-Theorem/) for more details.