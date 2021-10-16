---
title: The Convergence Rate of Graph Laplacian
date: 2020-12-17 10:31:51
tags:
- Spectral Graph Theory
- Asymptotic Analysis
categories:
- Manifold-Learning
---

Amit Singer's paper [*From graph to manifold Laplacian: The convergence rate*](https://www.math.pku.edu.cn/teachers/yaoy/Fall2011/Amit06_laplacian.pdf) presents a very clear proof of the convergence rate of graph Laplacian that everyone can follow. Techniques involved in this proof have become standard in following works in manifold learning. We review the proof in this post.

## Setups

Let $x_1,\cdots,x_N$ be i.i.d. samples from uniform distribution on compact submanifold $\mathcal{M}^d\subseteq \mathbb{R}^m$. Construct the weight matrix $W$ by using heat kernel
$$
W_{ij}=\exp\{-\|x_i-x_j\|^2/2\epsilon\}
$$
Define the degree matrix by
$$
D_{ii}=\sum_j W_{ij}
$$
The graph Laplacian is given by
$$
L=D^{-1}W-I
$$
Let $f:\mathcal{M}\to\mathbb{R}$ be a smooth function and $\Delta_\mathcal{M}$ be the Beltrami-Laplacian operator  on $\mathcal{M}$. The convergence result states that for each $x_i$ we have
$$
\frac{1}{\epsilon}\sum_j L_{ij}f(x_j)=\frac{1}{2}\Delta_\mathcal{M}f(x_i)+O(\frac{1}{\sqrt{N\epsilon^{1+d/2}}},\epsilon)
$$
$\textbf{Remark}:$ In fact the convergence result holds for any $x\in\mathcal{M}$. However, if we choose $x$ to be a fixed data point, then in the following arguments there will be $N-1$ random data and the summation should exclude $x_i$. We follow the original paper and denote $x_i$ by $x$.



## Bias

Define
$$
\begin{aligned}
& F(x_j)=\exp\{-\|x-x_j\|^2/2\epsilon\}f(x_j)\\
& G(x_j)=\exp\{-\|x-x_j\|^2/2\epsilon\}
\end{aligned}
$$
The graph Laplacian can be written as
$$
(Lf)(x)=\frac{\sum_j F(x_j)}{\sum_j G(x_j)}-f(x)
$$
As we remarked above, we need to consider
$$
\frac{\sum_{j\neq i} F(x_j)}{\sum_{j\neq i} G(x_j)}
$$
As $N$ tends infinity, we may expect
$$
\frac{\sum_{j\neq i} F(x_j)}{\sum_{j\neq i} G(x_j)}\to\frac{\mathbb{E}F}{\mathbb{E}G}
$$
where
$$
\begin{aligned}
& \mathbb{E}F=\int_{\mathcal{M}} \exp\{-\|x-y\|^2/2\epsilon\}f(y)\frac{\rm{d}y}{vol(\mathcal{M})}\\
& \mathbb{E}G=\int_{\mathcal{M}} \exp\{-\|x-y\|^2/2\epsilon\}\frac{\rm{d}y}{vol(\mathcal{M})}
\end{aligned}
$$
The Taylor expansion for $\mathbb{E}F$ is given by
$$
\begin{aligned}
&\frac{1}{(2\pi \epsilon)^{d/2}}\int_\mathcal{M}\exp\{-\|x-y\|^2/2\epsilon\}f(y){\rm d}y\\
=&f(x)+\frac{\epsilon}{2}(E(x)f(x)+\Delta_\mathcal{M}f(x))+O(\epsilon^{2})
\end{aligned}
$$
Therefore,
$$
\begin{aligned}
\frac{\mathbb{E}F}{\mathbb{E}G}&=\frac{f(x)+\frac{\epsilon}{2}(E(x)f(x)+\Delta_\mathcal{M}f(x))+O(\epsilon^{2})}{1+\frac{\epsilon}{2}E(x)+O(\epsilon^{2})}\\
&=f(x)+\frac{\epsilon}{2}\Delta_\mathcal{M}f(x)+O(\epsilon^{2})
\end{aligned}
$$
The bias term is given by
$$
\frac{\mathbb{E}F}{\mathbb{E}G}-f(x)=\frac{\epsilon}{2}\Delta_\mathcal{M}f(x)+O(\epsilon^{2})
$$
$\textbf{Remark}$: In fact we have decomposed $Lf$ as 
$$
\begin{aligned}
(Lf)(x)=&\frac{\sum_j F(x_j)}{\sum_j G(x_j)}-\frac{\sum_{j\neq i} F(x_j)}{\sum_{j\neq i} G(x_j)}\\
&+\frac{\sum_{j\neq i} F(x_j)}{\sum_{j\neq i} G(x_j)}-\frac{\mathbb{E}F}{\mathbb{E}G}\\
&+\frac{\mathbb{E}F}{\mathbb{E}G}-f(x)
\end{aligned}
$$
For the first term, a rough estimate is given by
$$
\begin{aligned}
&\frac{\sum_j F(x_j)}{\sum_j G(x_j)}-\frac{\sum_{j\neq i} F(x_j)}{\sum_{j\neq i} G(x_j)}\\
=&\frac{(\sum_j F(x_j))(\sum_{j\neq i} G(x_j))-(\sum_{j\neq i} F(x_j))(\sum_{j} G(x_j))}{\sum_j G(x_j)\sum_{j\neq i} G(x_j)}\\
=&\frac{F(x)(\sum_{j\neq i} G(x_j))-G(x)(\sum_{j\neq i} F(x_j))}{\sum_j G(x_j)\sum_{j\neq i} G(x_j)}\\
=&\frac{f(x)(\sum_{j\neq i} G(x_j))-(\sum_{j\neq i} F(x_j))}{\sum_j G(x_j)\sum_{j\neq i} G(x_j)}\\
=&\frac{\sum_j F(x_j)}{\sum_j G(x_j)}\frac{f(x)}{\sum_j F(x_j)}-\frac{\sum_{j\neq i} F(x_j)}{\sum_{j\neq i} G(x_j)}\frac{1}{\sum_j G(x_j)}\\
\le& C\frac{1/N}{1/N\sum_j F(x_j)}f(x)-C'\frac{1/N}{1/N\sum_j G(x_j)}\\
=& O(\frac{1}{N\epsilon^{d/2}}) 
\end{aligned}
$$
where bounds $C$ and $C'$ come from the fact that convergent sequences are bounded. However, as we will see later $O(1/N\epsilon^{d/2})$ is negligible compared to bias and variance. 

## Variance

For the variance error
$$
\frac{\sum_{j\neq i} F(x_j)}{\sum_{j\neq i} G(x_j)}-\frac{\mathbb{E}F}{\mathbb{E}G}
$$
we can only expect it to be small *in probability* when $N$ tends to infinity. 

Recall that the [Chebyshev inequality](https://en.wikipedia.org/wiki/Chebyshev%27s_inequality) states that for a random variable $X$ with finite mean $\mu$ and variance $\sigma^2$ then for any $t>0$ we have
$$
\mathbb{P}(|X-\mu|\ge t)\le \frac{\sigma^2}{t^2}
$$
$\textbf{Remark}$: In the original paper the author used Chernoff inequality. However, according to the context it seems to be [Bernstein inequality](https://en.wikipedia.org/wiki/Bernstein_inequalities_(probability_theory) ). But in the final statement the author only used variance and missed another term in the denominator. It seems Chebyshev inequality is enough for our use.

Consider the following probability
$$
\begin{aligned}
p(N,\alpha)&=\mathbb{P}\left(\left|\frac{\sum_{j\neq i} F(x_j)}{\sum_{j\neq i} G(x_j)}-\frac{\mathbb{E}F}{\mathbb{E}G}\right|\ge \alpha\right)\\
&=p_+(N,\alpha)+p_-(N,\alpha)\\
&=\mathbb{P}\left(\frac{\sum_{j\neq i} F(x_j)}{\sum_{j\neq i} G(x_j)}-\frac{\mathbb{E}F}{\mathbb{E}G}\ge \alpha\right)\\
&+\mathbb{P}\left(\frac{\sum_{j\neq i} F(x_j)}{\sum_{j\neq i} G(x_j)}-\frac{\mathbb{E}F}{\mathbb{E}G}\le -\alpha\right)
\end{aligned}
$$
Since $G(x_j)$ are positive, it is equivalent to 
$$
\begin{aligned}
p(N,\alpha)&=p_+(N,\alpha)+p_-(N,\alpha)\\
&=\mathbb{P}\left(\sum_{j\neq i}F(x_j)\mathbb{E}G-G(x_j)\mathbb{E}F-\sum_{j\neq i}\alpha G(x_j)\mathbb{E}G\ge 0\right)\\
&+\mathbb{P}\left(\sum_{j\neq i}F(x_j)\mathbb{E}G-G(x_j)\mathbb{E}F+\sum_{j\neq i}\alpha G(x_j)\mathbb{E}G\le 0\right)
\end{aligned}
$$
If we define
$$
Y_j=F(x_j)\mathbb{E}G-G(x_j)\mathbb{E}F+\alpha\mathbb{E}G(\mathbb{E}G-G(x_j))
$$
Then $Y_j$ are i.i.d. samples with zero mean. The probability $p(N,\alpha)$ can be expressed by
$$
p(N,\alpha)=\mathbb{P}\left(\left|\sum_{j\neq i} Y_j\right|\ge (N-1)\alpha(\mathbb{E}G)^2\right)
$$
To apply Chebyshev inequality, we only need to compute $\mathbb{E}Y_j^2$. Using the expansion from $\mathbb{E}F$ we have
$$
\begin{aligned}
& \mathbb{E}F=\frac{(2\pi\epsilon)^{d/2}}{vol(\mathcal{M})}\left(f(x)+\frac{\epsilon}{2}(E(x)f(x)+\Delta_\mathcal{M}f(x))+O(\epsilon^2)\right)\\
& \mathbb{E}G=\frac{(2\pi\epsilon)^{d/2}}{vol(\mathcal{M})}\left(1+\frac{\epsilon}{2} E(x)+O(\epsilon^2)\right)\\
& \mathbb{E}F^2=\frac{(\pi\epsilon)^{d/2}}{vol(\mathcal{M})}\left(f^2(x)+\frac{\epsilon}{4}(E(x)f^2(x)+\Delta_\mathcal{M}f^2(x))+O(\epsilon^2)\right)\\
& \mathbb{E}G^2=\frac{(\pi\epsilon)^{d/2}}{vol(\mathcal{M})}\left(1+\frac{\epsilon}{4} E(x)+O(\epsilon^2)\right)\\
& \mathbb{E}FG=\frac{(\pi\epsilon)^{d/2}}{vol(\mathcal{M})}\left(f(x)+\frac{\epsilon}{4}(E(x)f(x)+\Delta_\mathcal{M}f(x))+O(\epsilon^2)\right)
\end{aligned}
$$
Note that in the derivation of bias term, the coefficient before $\Delta_\mathcal{M}f$ is $\epsilon/2$. Therefore, we should focus on $\alpha\ll \epsilon$. Neglecting $\alpha$ and $\alpha^2$ term, we have
$$
\mathbb{E}Y_j^2=\frac{2^d(\pi\epsilon)^{3d/2}}{vol(\mathcal{M})^3}\frac{\epsilon}{2}(\|\nabla_\mathcal{M} f\|^2+O(\epsilon))
$$
Substituting into Chebyshev inequality we have
$$
\begin{aligned}
&p(N,\alpha)\\
\le&\frac{\mathbb{E}Y_j^2}{(N-1)\alpha^2(\mathbb{E}G)^4}\\
=&\frac{\frac{2^d(\pi\epsilon)^{3d/2}}{vol(\mathcal{M})^3}\frac{\epsilon}{2}(\|\nabla_\mathcal{M} f\|^2+O(\epsilon))}{(N-1)\alpha^2\frac{(2\pi\epsilon)^{2d}}{vol(\mathcal{M})^4}\left(1+\frac{\epsilon}{2} E(x)+O(\epsilon^2)\right)^4}\\
=&\frac{vol(\mathcal{M})\epsilon(\|\nabla_\mathcal{M} f\|^2+O(\epsilon))}{2^{d+1}(\pi\epsilon)^{d/2}(N-1)\alpha^2\left(1+\frac{\epsilon}{2} E(x)+O(\epsilon^2)\right)^4}
\end{aligned}
$$
If we take 
$$
\alpha\approx\sqrt{\frac{vol(\mathcal{M})\epsilon(\|\nabla_\mathcal{M} f\|^2+O(\epsilon))}{2^{d+1}(\pi\epsilon)^{d/2}(N-1)}}
$$
Thus the noise error is 
$$
\frac{\alpha}{\epsilon}=O(\frac{1}{\sqrt{N\epsilon^{1+d/2}}})
$$