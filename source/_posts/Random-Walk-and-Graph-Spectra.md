---
title: Random Walk and Graph Spectra
date: 2020-03-27 17:04:22
tags:
- Random Walk
- Spectral Graph Theory
categories:
- Network-Analysis

---

Random walks arise in many fields in mathematics and physics, recently in network analysis, graph learning, clustering etc. It also has a natural relation with spectral graph theory. The [survey](http://web.cs.elte.hu/~lovasz/erdos.pdf) written by L.Lovasz presents many beautiful results concerning random walks and graph spectra. We aim to write down some computation details missing in the original succinct paper.  <!--more-->

## Basic Notions

Let $G=(V,E)$ be a connected, undirected, simple graph with $n$ nodes and $m$ edges. Consider the following random walk on $G$: start from a node $v_0$; at the $t$th step move to the neighbor of $v_t$ with probability $1/d(v_t)$. i.e. It is a Markov chain with transition matrix 
$$
M=D^{-1}A
$$
where $A$ is the adjacency matrix and $D$ is the diagonal matrix such that $D_{ii}=d(i)=\sum_jA_{ij}$ ($\textbf{Caveat:}$ in original paper $D$ is adopted as $D^{-1}$ here, thus all the indices over $D$ are reversed in this note). Let $P_t$ be the distribution at time $t$. Then 
$$
(P_t)_i=\sum_j (P_{t-1})_jM_{ji}
$$
If we assume $P_t$'s are column vectors, the matrix form should be written as 
$$
P_t=M^TP_{t-1}
$$
A random walk is called stationary if $P_0=P_1$. We denote the stationary random walk by $\pi$. A simple calculation shows that $\pi=D\mathbf{1}/2m$ is a stationary distribution of $M$. The uniqueness and convergence are shown by the following.

## Stationary Distribution

Before discussing about the stationary distribution of the random walk $M$, we state the [Perron-Frobenius theorem]([https://en.wikipedia.org/wiki/Perron%E2%80%93Frobenius_theorem](https://en.wikipedia.org/wiki/Perron–Frobenius_theorem)) which reveals some important properties about nonnegative matrices.

A nonnegative matrix $A$ is called irreducible if there does **NOT** exist a permutation matrix $R$ such that 
$$
RAR^{-1}=\left[\begin{array}{cc}E&F\\ 0&G\end{array}\right]
$$
For an irreducible matrix $A$, the spectral radius $\rho(A)=r>0$ is an eigenvalue of $A$, whose corresponding (left /right) eigenspace is unidimensional. Moreover, $A$ has an (left/right) eigenvector $v$ associated with $r$ whose components are all positive, and conversely,  eigenvectors whose components are all positive are associated with $r$.  

Consider the special case where $A$ is the adjacency matrix of an undirected simple graph. $A$ is irreducible if and only if there does not exist a nontrivial partition $\{1,2,\cdots, n\}=I\cup J$ such that $A_{ij}=0$ for $i\in I$ and $j\in J$. i.e. $A$ is irreducible if and only if the graph $G$ is connected. This criterion easily generalizes to any similarity matrices on graphs. For example, consider $N=D^{-1/2}AD^{-1/2}$. It is irreducible if and only if $G$ is connected. Since $N$ is symmetric, write $N$ in spectral form 
$$
N=\sum_k\lambda_kv_kv_k^T
$$
where $\lambda_1\ge\lambda_2\ge\cdots\ge\lambda_n$ are eigenvalues of $N$ and $v_1,\cdots,v_n$ are corresponding  eigenvectors of unit length. Note that $A\mathbf{1}=D\mathbf{1}$, which gives $ND^{1/2}\mathbf{1}=D^{1/2}\mathbf{1}$. i.e. $D^{1/2}\mathbf{1}$ is an eigenvector of $N$ whose components are all positive. By Perron-Frobenius theorem, $v_1=\frac{D^{1/2}\mathbf{1}}{\sqrt{2m}}$ and $\lambda_1=1>\lambda_2\ge\cdots\ge\lambda_n\ge-1$. 

A simple calculation shows that $M=D^{-1/2}ND^{1/2}$ is similar to $N$. Now we have
$$
M^t=D^{-1/2}v_1v_1^TD^{1/2}+\sum_{k\ge 2}\lambda_k^tD^{-1/2}v_kv_k^TD^{1/2}=Q+\Lambda^t
$$
where $Q_{ij}=d(j)/2m=\pi(j)$ is such that $Q^TP=\pi$ for any probability distribution $P$. Hence if we can prove $\Lambda^t\to 0$ as $t\to\infty$ we obtain that $\pi$ is the stationary distribution. In addition, since $M$ is similar to $N$ and $\lambda_1=1$ is a simple eigenvalue of $N$, we see that $\pi$ will be the only probability distribution such that $M^T\pi=\pi$. Apparently, it suffices to exclude the case where $\lambda_n=-1$.

Let $L=D-A$ be the Laplacian matrix, $\mathcal{L}=D^{-1/2}LD^{-1/2}$ be the normalized Laplacian. Note that $\mathcal{L}=I-N$. Thus, $\lambda_n(N)=1-\lambda_1(\mathcal{L})$. By Rayleigh-Ritz theorem, 
$$
\lambda_1(\mathcal{L})=\sup_f\frac{f^T\mathcal{L}f}{f^Tf}
$$
Set $g=D^{-1/2}f$. Then by the fact $(g_i-g_j)^2\le 2(g_i^2+g_j^2)$,
$$
\lambda_1(\mathcal{L})=\sup_g\frac{1/2\sum_{i,j}a_{ij}(g_i-g_j)^2}{\sum_ig_i^2d_i}\le\sup_g\frac{\sum_{i,j}a_{ij}(g_i^2+g_j^2)}{\sum_ig_i^2d_i}=2
$$
where equality holds if and only if $g_i=-g_j$ if $a_{ij}\neq0$. Since $g\neq 0$, the components of $g$ is partitioned into two parts. Hence $\lambda_n(N)=-1$ if and only if $\lambda_1(\mathcal{L})=-2$ if and only if $G$ is bipartite. 

Overall we proved the following claim about stationary distribution.

> Let $G$ be an undirected, simple, connected, non-bipartite graph, with transition matrix $M=D^{-1}A$. It possesses a unique stationary distribution $\pi=D\mathbf{1}/2m$ such that $M^T\pi=\pi$ and $\lim_{t\to\infty}P_t=\pi$ for any initial distribution $P_0$.

## Spectra and Access Time

The access time (or hitting time) $H_{ij}$ is the expected number of steps the first time meeting node $j$ starting from node $i$. i.e. 
$$
H_{ij}=\sum n\times \text{Prob(meet node j in n steps)}
$$
By definition $H_{ii}=0$. For $i\neq j$, by conditional expectation formula
$$
H_{ij}=\frac{1}{d_i}(\sum_{k\sim i}1+H_{kj})=1+\frac{1}{d_i}\sum_{k\sim i}H_{kj}
$$
Let $J=\mathbf{1}\mathbf{1}^T$ be the all-one matrix. According to the above equation, the matrix $F=J+MH-H$ is a diagonal matrix. Direct computation shows that $F^T\pi=\mathbf{1}$. Hence $F=2mD^{-1}$. The access time matrix satisfies 
$$
(I-M)H=J-2mD^{-1}
$$
By the above discussion, the kernel of $I-M$ is unidimensional. If $X$ is a solution of (11), then $X+\mathbf{1}a^T$ gives all the solutions of (11). By the restriction $H_{ii}=0$, we can solve for the unique $H$. Let $V=[v_1,\cdots,v_n]$ be the orthogonal matrix such that 
$$
N=V\left[\begin{array}{ccc}\lambda_1&&\\&\ddots&\\&&\lambda_n\end{array}\right]V^T
$$
Set $U=D^{-1/2}V$. Then we have 
$$
I-M=U\left[\begin{array}{ccc}0&&\\&\ddots&\\&&1-\lambda_n\end{array}\right]U^{-1}
$$

Note the right side of (11) has nothing to do with $\lambda_i$. We try to get rid of these eigenvalues. Suppose the solution $X$ has a factor 
$$
U\left[\begin{array}{ccc}0&&\\&\ddots&\\&&\frac{1}{1-\lambda_n}\end{array}\right]U^{-1}
$$
The multiplication with (13) gives 
$$
\sum_{k\ge 2}D^{-1/2}v_kv_k^TD^{1/2}=-D^{-1/2}v_1v_1^TD^{1/2}+I=JD/2m+I
$$
In addition, multiplying (15) with $J-2mD^{-1}$ gives
$$
(\frac{JD}{2m}+I)(J-2mD^{-1})=J-2mD^{-1}
$$
Therefore one solution of (11) is
$$
\begin{aligned}
X&=U\left[\begin{array}{ccc}0&&\\&\ddots&\\&&\frac{1}{1-\lambda_n}\end{array}\right]U^{-1}(J-2mD^{-1})\\
&=D^{-1/2}(\sum_{k\ge 2}\frac{v_kv_k^T}{1-\lambda_k})D^{1/2}\mathbf{1}\mathbf{1}^T-2mD^{-1/2}(\sum_{k\ge 2}\frac{v_kv_k^T}{1-\lambda_k})D^{-1/2}\\
&=\sqrt{2m}D^{-1/2}(\sum_{k\ge 2}\frac{v_kv_k^T}{1-\lambda_k})v_1\mathbf{1}^T-2mD^{-1/2}(\sum_{k\ge 2}\frac{v_kv_k^T}{1-\lambda_k})D^{-1/2}\\
&=-2mD^{-1/2}(\sum_{k\ge 2}\frac{v_kv_k^T}{1-\lambda_k})D^{-1/2}
\end{aligned}
$$
Finally, we have to subtract the diagonals of $X$. Since 
$$
X_{ii}=-2m\sum_{k\ge 2}\frac{v_{ki}^2}{(1-\lambda_k)d_i}
$$
The access time matrix is $H=X-\mathbf{1}[X_{11},\cdots,X_{nn}]^T$. The elements are
$$
H_{ij}=2m\sum_{k\ge 2}\frac{1}{1-\lambda_k}(\frac{v_{kj}^2}{d_j}-\frac{v_{ki}v_{kj}}{\sqrt{d_id_j}})
$$

This equation has many applications. For example, we can quickly find the symmetric properties of $H$. 

> For any three nodes $u,v$ and $w$, $H_{uv}+H_{vw}+H_{wu}=H_{uw}+H_{wv}+H_{vu}$.

Direct computation shows that the sum $H_{uv}+H_{vw}+H_{wu}$ is 
$$
\sum_{k\ge 2}\frac{m}{1-\lambda_k}\left((\frac{v_{ku}}{\sqrt{d_u}}-\frac{v_{kv}}{\sqrt{d_v}})^2+(\frac{v_{kv}}{\sqrt{d_v}}-\frac{v_{kw}}{\sqrt{d_w}})^2+(\frac{v_{kw}}{\sqrt{d_w}}-\frac{v_{ku}}{\sqrt{d_u}})^2\right)
$$
which is invariant under permutation.

> Let $\pi$ be the stationary walk. Then $\sum_j\pi_jH_{ij}=\sum_{k\ge 2}\frac{1}{1-\lambda_k}$.

Use the fact that $\pi=D\mathbf{1}/2m$ and $v_1=D^{1/2}\mathbf{1}/\sqrt{2m}$ which is orthogonal to all $v_k$. In the summation,
$$
\sum_j\pi_jH_{ij}=\sum_{k\ge 2}\frac{1}{1-\lambda_k}(\sum_jv_{kj}^2-\frac{v_{ki}}{\sqrt{d_i}}\sum_jv_{kj}v_{1j}\sqrt{2m})=\sum_{k\ge 2}\frac{1}{1-\lambda_k}
$$
Note that this equality is independent of the starting point. Thus we can explain the formula as follows: in a stationary walk, no matter where we start on the graph, the average number of steps before meeting all the other nodes is a fix number which related to the graph spectra. Thus this formula nicely connects random walk with geometry of the graph.

> Let $\pi$ be the stationary walk. Then $\sum_i\pi_iH_{ij}\ge \frac{(1-\pi_j)^2}{\pi_j}$

Using again $v_1$ is orthogonal to $v_k$, we have
$$
\sum_i\pi_iH_{ij}=\frac{2m}{d_j}\sum_{k\ge 2}\frac{1}{1-\lambda_k}v_{kj}^2
$$
By Cauchy-Schwartz inequality,
$$
\sum_{k\ge 2}\frac{v_{kj}^2}{1-\lambda_k}\sum_{k\ge 2}(1-\lambda_k)v_{kj}^2\ge(\sum_{k\ge 2}v_{kj}^2)^2
$$
Note that $\sum_{k\ge 2}v_{kj}^2=1-\pi(j)$, and $\sum_{k\ge2}(1-\lambda_k)v_{kj}^2=\sum_{k}(1-\lambda_k)v_{kj}^2=1-N_{jj}=1$. Thus we obtain the claim.

To give an example where the access time is calculable, consider the $k$-cube $Q_k$. Let $\mathbf{0}=(0,0,\cdots,0)$ and $\mathbf{1}=(1,1,\cdots,1)$. The nodes are elements in $\{0,1\}^k$ and two nodes are connected by an edge if they differ by one digit (see [hypercube graph](https://en.wikipedia.org/wiki/Hypercube_graph) ). To find all the eigenvalues and eigenvectors of $M$ (or $A$ since $D$ is a scalar matrix), L.Lovasz's paper gives a beautiful construction: for every vector $b\in\{0,1\}^k$, define $(v_b)_x=(-1)^{b\cdot x}$. i.e. the component of $v_b$ at node $x$ is $1$ if $b$ and $x$ share even number of $1$'s  and is $0$ otherwise. Note that 
$$
\sum_ja_{ij}(v_b)_j=\sum_{j:|i-j|=1}(-1)^{b\cdot j}
$$
Now if $j$ changes one digit of $i$ where the component of $b$ is $0$, $b\cdot j=b\cdot i$. This gives $k-b\cdot\mathbf{1}$ number of $(-1)^{b\cdot i}$. Otherwise  (the component of $b$ is $1$) each change from $j$ will yields $b\cdot j=b\cdot i\pm 1$, giving $b\cdot\mathbf{1}$ number of $-(-1)^{b\cdot i}$. Hence $v_b$ is an eigenvector of $M$ with eigenvalue $1-\frac{2}{k}b\cdot\mathbf{1}$. Normalizing $v_b$ and using the formula for $H$ we have 
$$
\begin{aligned}
H(\mathbf{0},\mathbf{1})&=\sum_{b\in\{0,1\}^k,b\neq 0}\frac{k}{b\cdot\mathbf{1}}(1-(-1)^{b\cdot\mathbf{1}})\\
&=k\sum_{j=1}^kC_k^j\frac{1}{2j}(1-(-1)^j)\\
&\ge \frac{k}{2(k+1)}\sum_{j=1}^{k}C_{k+1}^{j+1}(1-(-1)^j)\\
&=\frac{k}{k+1}(2^k-1)
\end{aligned}
$$
To obtain an upper bound, use the identity $C_k^j=\sum_{p=0}^{k-1}C_p^{j-1}$, where $C_p^{j-1}=0$ for $p<j-1$. We have 
$$
\begin{aligned}
H(\mathbf{0},\mathbf{1})&=k\sum_{j=1}^k\sum_{p=0}^{k-1}C_{p}^{j-1}\frac{1}{2j}(1-(-1)^j)\\
&=k\sum_{j=1}^k\sum_{p=0}^{k-1}\frac{1}{2(p+1)}C_{p+1}^{j}(1-(-1)^j)\\
&=k\sum_{p=0}^{k-1}\frac{1}{2(p+1)}\sum_{j=1}^kC_{p+1}^j(1-(-1)^j)\\
&= k\sum_{p=0}^{k-1}\frac{1}{2(p+1)}2^{p+1}\\
&\le k2^{k/2-1}\sum_{p<k/2-1}\frac{1}{1+p}+2\sum_{p\ge k/2-1}2^p\\
&\le 2^{k+1}+k\log k2^{k/2}
\end{aligned}
$$
Thus for large $k$ the exact value of $H(\mathbf{0},\mathbf{1})$ is between $2^k$ and $2^{k+1}$.

## Spectra and Mixing Rate

Let $\lambda=\max\{|\lambda_2|,|\lambda_n|\}$. By equation (6) we have
$$
P_t=(M^T)^tP_0=Q^TP_0+(\Lambda^T)^tP_0=\pi+(\Lambda^T)^tP_0
$$
For a random walk starting at node $i$, i.e. $P_0(i)=1$, we have
$$
P_t(j)=\pi(j)+\sum_{k\ge 2}\lambda_k^t\sqrt{\frac{d(j)}{d(i)}}v_{kj}v_{ki}
$$
Thus by geometric-arithmetic inequality,
$$
|P_t(j)-\pi(j)|\le\lambda^t\sqrt{\frac{d(j)}{d(i)}}\sum\frac{v_{kj}^2+v_{ki^2}}{2}\le \sqrt{\frac{d(j)}{d(i)}}\lambda^t
$$
Moreover, for any subset $S\subset\{1,\cdots,n\}$, by Cauchy inequality $\sum_{s\in S}\sqrt{d(s)}v_{ks}\le\sqrt{\sum_{s\in S}d(s)}\sqrt{\sum_{s\in S}v_{ks}}$, we have
$$
|P_t(S)-\pi(S)|\le \frac{|S|+1}{2}\sqrt{\frac{\pi(S)}{\pi(i)}}\lambda^t
$$
Note that $P_t(j)$ is nothing but the probability of transferring from node $i$ to node $j$ in $t$ steps. Define the mixing rate
$$
\mu=\limsup_{t\to\infty}\max_{i,j}|M^t(i,j)-\pi(j)|
$$
From equation (25) we immediately have $\mu=\lambda$. Thus we obtain

> The mixing rate of a random walk on a non-bipartite graph is $\lambda=\max\{|\lambda_2|,|\lambda_n|\}$.

To get rid of $\lambda_n$, consider the following lazy random walk
$$
M_L=\frac{1}{2}I+\frac{1}{2}D^{-1}A=\frac{1}{2}(I+M)
$$
That is, we have half of the probability to stay rather than move, which is also equal to adding $d(i)$ loops at each node $i$. Set $N_L=D^{-1/2}(D+A)D^{-1/2}$. We have $D^{1/2}M_LD^{-1/2}=\frac{1}{2}N_L=\frac{1}{2}(I+N)$. If $Nv=\lambda v$, it holds $M_LD^{-1/2}v=\frac{1+\lambda}{2}D^{-1/2}v$. Thus we have $\lambda(M_L)=(1+\lambda(M))/2\ge0$. Furthermore,
$$
M_L^t=D^{-1/2}v_1v_1^TD^{1/2}+\sum_{k\ge 2}(\frac{1+\lambda_k(M)}{2})^tD^{-1/2}v_kv_k^TD^{1/2}
$$
we see that lazy random walk always converges to the stationary distribution, with rate $(1+\lambda_2(M))/2>\lambda_2$, which makes sense that lazy walk is slower.

 Thus the mixing rate is closely related to $\lambda_2$, or equivalently, the spectral gap $\lambda_1-\lambda_2=1-\lambda_2$. Let $\emptyset\neq S\subset V$ and $\nabla(S)$ be the set of edges connecting $S$ to $V\backslash S=\bar{S}$, i.e. $\nabla(S)$ is the edge cut of the graph with respect to $S$ (see this [post](http://yueqicao.top/2020/03/10/Spectral-Graph-Partitioning/) ). Define the conductance of the set $S$ by 
$$
\Phi(S)=\frac{|\nabla(S)|}{2m\pi(S)\pi(V\backslash S)}
$$
Here $\pi(S)=\sum_{s\in S}d(s)/2m=vol(S)/2m$. The conductance of the graph is defined by 
$$
\Phi=\min_S\Phi(S)
$$
It turns out that the spectral gap is controlled by the graph conductance. 

> $\frac{\Phi^2}{16}\le 1-\lambda_2\le \Phi$

Recall that the normalized Laplacian is $\mathcal{L}=D^{-1/2}LD^{-1/2}=I-N$, which implies $\lambda(\mathcal{L})=1-\lambda(N)=1-\lambda(M)$. The second largest eigenvalue of $M$ is the second smallest eigenvalue of $\mathcal{L}$. By Rayleigh-Ritz theorem,
$$
1-\lambda_2=\min_{f\perp D^{1/2}\mathbf{1}}\frac{f^T\mathcal{L}f}{f^Tf}
$$
Let $g=D^{-1/2}f$ and set $g^TDg=1$. By the basic property of graph Laplacian,
$$
1-\lambda_2=\min\{\sum_{i\sim j}(x_i-x_j)^2:\sum_i d(i)x_i=0,\sum_i d(i)x_i^2=1\}
$$
Let $S$ be the set with minimum conductance, and consider the vector given by 
$$
x_i=\left\{\begin{array}{l}a,i\in S\\ b,i\in\bar{S}\end{array}\right.
$$
where
$$
a=\sqrt{\frac{\pi(\bar{S})}{2m\pi(S)}},b=-\sqrt{\frac{\pi(S)}{2m\pi(\bar{S})}}
$$
Then
$$
\sum_{i\sim j}(x_i-x_j)^2=\sum_{i\in S,j\in\bar{S}}\frac{\pi(\bar{S})}{2m\pi(S)}+\frac{\pi(S)}{2m\pi(\bar{S})}+\frac{1}{m}=\frac{|\nabla(S)|}{2m\pi(S)\pi(\bar{S})}=\Phi
$$
This proves the upper bound. To obtain the lower bound, we first prove the following lemma

> Let $y\in\mathbb{R}^{|V|}$ such that $\pi(\{i:y_i>0\})\le 1/2$, $\pi(\{i:y_i<0\})\le 1/2$ and $\sum_i\pi(i)|y_i|=1$. Then $\sum_{i\sim j}|y_i-y_j|\ge m\Phi$. 

Sort the vector $y$ such that $y_1\le y_2\le\cdots\le y_t<0=y_{t+1}=\cdots=y_s<y_{s+1}\le\cdots y_n$. Consider the sets defined by $S_i=\{1,\cdots,i\}$. For a fixed node $i$, in the sum $\sum_{i\sim j}|y_j-y_i|$ the quantity $y_{i+1}-y_i$ is counted for $|\nabla(S_i)|$ times if we substitute $|y_j-y_i|$ by $y_{j}-y_{j-1}+\cdots+y_{i+1}-y_i$. We have 
$$
\sum_{i\sim j}|y_i-y_j|=\sum_{i=1}^{n-1}|\nabla(S_i)|(y_{i+1}-y_i)\ge2m\Phi\sum_{i=1}^{n-1}(y_{i+1}-y_i)\pi(S_i)\pi(\bar{S}_i)
$$
Since $\pi(S_i)\le 1/2$ for $i\le t$ and $\pi(S_i)\ge 1/2$ for $i\ge s+1$, we have 
$$
\begin{aligned}
\sum_{i\sim j}|y_i-y_j|&\ge m\Phi\sum_{i=1}^t(y_{i+1}-y_i)\pi(S_i)+m\Phi\sum_{i=s}^{n-1}(y_{i+1}-y_i)\pi(\bar{S}_i)\\
&=m\Phi\sum_{i=1}^t(-y_i)\pi(i)+m\Phi\sum_{i=s+1}^{n}y_i\pi(i)\\
&=m\Phi\sum_{i=1}^n|y_i|\pi(i)=m\Phi
\end{aligned}
$$
Return to the proof of lower bound. Let $x$ be any vector satisfying 
$$
\sum_i d(i)x_i=0,\sum_id(i)x_i^2=1
$$
Assume $x_1\ge \cdots\ge x_n$. Let $k$ be the index such that $\pi(\{1,\cdots,k-1\})\le 1/2$ and $\pi(\{1,\cdots,k\})>1/2$. Therefore, $x_1-x_k\ge\cdots\ge x_{k-1}-x_k\ge0\ge x_{k+1}-x_k\ge\cdots\ge x_n-x_k$. Set $z_i=\max\{0,x_i-x_k\}$. Then $z_i=0$ for $i\ge k$. 
$$
\sum_i \pi_i(x_i-x_k)^2=\sum_{i}\pi_iz_i^2+\sum_{i>k}\pi_i(x_i-x_k)^2
$$
By replacing $x$ with $-x$ we may assume $\sum_{i}\pi_iz_i^2\ge\sum_{i>k}\pi_i(x_i-x_k)^2$. Thus we have
$$
\sum_i\pi_iz_i^2\ge \frac{1}{2}\sum_i\pi_i(x_i-x_k)^2\ge\frac{1}{4m}
$$
Apply the above lemma to $y_i=z_i^2/\sum_i\pi_iz_i^2$. We obtain
$$
\sum_{i\sim j}|z^2_i-z_j^2|\ge m\Phi\sum_i\pi_iz_i^2
$$
On the other hand, by Cauchy inequality
$$
(\sum_{i\sim j}|z_i^2-z_j^2|)^2\le(\sum_{i\sim j}(z_i-z_j)^2)(\sum_{i\sim j}(z_i+z_j)^2)
$$
Furthermore,
$$
\sum_{i\sim j}(z_i+z_j)^2\le 2\sum_{i\sim j}z_i^2+z_j^2=\sum_{i,j}a_{ij}(z_i^2+z_j^2)=4m\sum_i\pi_iz_i^2
$$
Combining these results together, we have
$$
\sum_{i\sim j}(z_i-z_j)^2\ge \frac{m^2\Phi^2}{4m}\sum_i\pi_iz_i^2\ge\frac{\Phi^2}{16}
$$
The theorem follows from the fact that $\sum_{i\sim j}(x_i-x_j)^2\ge\sum_{i\sim j}(z_i-z_j)^2$.

We remark that conductance is similar to what is so called [Cheeger constant](https://en.wikipedia.org/wiki/Cheeger_constant_(graph_theory)) defined as 
$$
h_G=\min_S\frac{|\nabla(S)|}{2m\min\{\pi(S),\pi(\bar{S})\}}
$$
the lower bound lemma goes without modification for $h_G$. Thus we can feel free to  replace $\Phi$ with $h_G$.