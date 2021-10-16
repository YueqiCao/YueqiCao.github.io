---
title: The Space of Persistence Diagrams
date: 2019-11-24 10:01:39
tags:
- TDA Stability
categories: TDA

---

**Notation.** In the following $\mathbb R^2$ is equipped with $\infty$-norm. Let $\Delta=\{(x,x)|x\in\mathbb R\}$ denote the diagonal, $\Delta_+=\{(x,y)|y>x\}$ denote the upper off-diagonal points, and $\overline{\Delta}_+=\Delta\cup\Delta_+$ is the closure of $\Delta_+$. Set $\overline{\mathbb N}=\{1,2,\cdots\}\cup\{\infty\}$.

-----

**Definition.** A persistence diagram $\mathcal T$ is a pair $(S_{\mathcal T},i_{\mathcal T})$ where $S_{\mathcal T}$ is a subset of $\mathbb R^2$ and $i_{\mathcal T}:S_{\mathcal T}\to \overline{\mathbb N}$ is a function such that 

1. $\Delta\subset S_{\mathcal T}\subset \overline{\Delta}_+$;
2. $i_{\mathcal T}(\Delta)=\{\infty\}$.

$S_{\mathcal T}$ is called the support of $\mathcal T$ while $i_{\mathcal T}$ is called the multiplicity function of $\mathcal T$.  

Two persistence diagrams are said to be equal if they have the same support and multiplicity function. The graph of $i_{\mathcal T}$, defined by $G(i_{\mathcal T})=\{^k{\bf x}:=({\bf x},k)\in S_{\mathcal T}\times \overline{\mathbb N}|k\le i_{\mathcal T}({\bf x})\}$, is called the bundle space over $\mathcal T$. The projection $\pi_{\mathcal T}:G(i_{\mathcal T})\to S_{\mathcal T}$ to the first factor defines a map from the bundle space to the support with fiber $\pi_{\mathcal T}^{-1}({\bf x})=\{1,2,\cdots,i_{\mathcal T}({\bf x})\}$ for each point ${\bf x}\in S_{\mathcal T}$. It is an easy consequence that two persistence diagrams are equal if and only if they have the same bundle spaces.

<!--more-->

**Definition.** Let $\mathcal T_1$ and $\mathcal T_2$ be two persistence diagrams. Their sum $\mathcal T_1+\mathcal T_2$ is a persistence diagram where $S_{\mathcal T_1+\mathcal T_2}=S_{\mathcal T_1}\cup S_{\mathcal T_2}$ is the union of two supports and $i_{\mathcal T_1+\mathcal T_2}=i_{\mathcal T_1}+i_{\mathcal T_2}$ is the natural extension on $S_{\mathcal T_1+\mathcal T_2}$. 

Let $0_{\Delta}$ be the trivial persistence diagram whose support is $\Delta$ and multiplicity function is the constant function $\infty$. It is clear that $0_{\Delta}$ is the neutral element for addition. Therefore, the set of persistence diagrams together with addition forms a monoid.

**Definition.** Let $\lambda\ge0$ be a nonnegative number. Define the scalar product  $\lambda \mathcal T$ to be the persistence diagram with $S_{\lambda\mathcal T}=\lambda S_{\mathcal T}=\{\lambda{\bf x}|{\bf x}\in S_{\mathcal T}\}$ and $i_{\lambda\mathcal T}(\lambda{\bf x})=i_{\mathcal T}({\bf x})$.

**Caveat.** It is easy to check that $\lambda(\mathcal T_1 +\mathcal T_2)=\lambda\mathcal T_1+\lambda\mathcal T_2$. However, for $\lambda_1,\lambda_2\neq 0$, $(\lambda_1+\lambda_2)\mathcal T$ may not equal to $\lambda_1\mathcal T+\lambda_2\mathcal T$.

**Definition.** Let $\mathcal T_1$ and $\mathcal T_2$ be two persistence diagrams and $p\ge 1$. The $p$th Wasserstein distance between $\mathcal T_1$ and $\mathcal T_2$ is defined as
$$
W_p(\mathcal T_1,\mathcal T_2)=(\inf_{\gamma}\{\sum_{^k{\bf x}\in G(i_{\mathcal T_1})}||\pi_{\mathcal T_1}(^k{\bf x})-\pi_{\mathcal T_2}(\gamma(^k{\bf x}))||_{\infty}^p\})^{1/p}
$$
where $\gamma$ ranges over all the bijections from $G(i_{\mathcal T_1})$ to $G(i_{\mathcal T_2})$. The summation is interpreted as integration with respect to the counting measure on $G(i_{\mathcal T_1})$. If such a bijection does not exist, the distance is defined to be $\infty$.

$W_p$ is not a metric on the space of persistence diagrams, since $W_p(\mathcal T_1,\mathcal T_2)=0$ does not imply $\mathcal T_1=\mathcal T_2$. For example, consider $\mathcal T_1$ with support $\{(0,y)|y\in(0,1]\}\cup\Delta$ and for each $(0,y)$ the multiplicity is $1$. Excise the point $(0,1)$ and we obtain another persistence diagram $\mathcal T_2$ such that $W_p(\mathcal T_1,\mathcal T_2)=0$. However, $\mathcal T_1$ and $\mathcal T_2$ are not equal. 

**Definition.** Let $\mathcal T$ be a persistence diagram and $p\ge 1$. The $p$th Wasserstein norm of $\mathcal T$ is defined as $||\mathcal T||_{W_p}:=W_p(\mathcal T, 0_{\Delta})$. The $p$th finite persistence space is defined as the collection of persistence diagrams with finite $p$th Wasserstein norm, i.e. $\mathcal D_p=\{\mathcal T|||\mathcal T||_{W_p}< \infty\}$. 

**Example.** Let ${\bf x}=(x,y)\in\mathbb R^2$ with $y>x$. Define the indicator diagram at ${\bf x}$ to be the diagram{%  raw %}$\chi^{{\bf x}}_1$ with support $\Delta\cup\{{\bf x}\}$ and $i_{\chi^{\bf x}_1}({\bf x})=1$. Then $||\chi^{{\bf x}}_1||_{W_p}=(y-x)/2$. Similarly, we can define $\chi_k^{{\bf x}}=\sum^k_{r=1}\chi^{\bf x}_1$, called the indicator diagram at ${\bf x}$ in multiplicity $k$. Then $||\chi_k^{\bf x}||_{W_p}=k^{1/p}(y-x)/2$. More generally, we have the following lemma.{% endraw %}

**Lemma.** {%raw%}Let $\mathcal T=\sum_{r=1}^n\chi^{{\bf x}_r}_{1}$ be a finite sum of indicator diagrams. Then $||\mathcal T||_{W_p}=(\sum_{r=1}^n||\chi_1^{{\bf x}_r}||^p_{W_p})^{1/p}${%endraw%}. As a consequence, for any $\mathcal T\in\mathcal D_p$ and ${\bf x}\in S_{\mathcal T}\backslash\Delta$, the  multiplicity of ${\bf x}$ is finite. i.e. $i_{\mathcal T}({\bf x})<\infty$.  

**Remark.** In convention, the degree-$p$ total persistence of a persistence diagram $\mathcal T$ is defined to be $(2W_p(\mathcal T,0_{\Delta}))^p$. Thus a persistence diagram has finite $p$th Wasserstein norm if and only if its degree-$p$ total persistence is finite. This is why we call $\mathcal D_p$  $p$th finite persistence space. 

**Theorem.** $W_p$ is a metric on the space $\mathcal D_p$ for $p\ge 1$.

**Proof.** Symmetry is obvious from definition. Let $\mathcal T_1,\mathcal T_2\in\mathcal D_p$. Assume $W_p(\mathcal T_1,\mathcal T_2)=0$. Let $^k{\bf z}\in G(i_{\mathcal T_1})$ and ${\bf z}$ be the corresponding point in $S_{\mathcal T_1}$. If ${\bf z}\in\Delta$, then it is clear $^k{\bf z}\in G(i_{\mathcal T_2})$. Suppose ${\bf z}\notin\Delta$. For any $\epsilon>0$, there is a bijection $\gamma_{\epsilon}$ from $G(i_{\mathcal T_1})$ to $G(i_{\mathcal T_2})$ such that 
$$
\sum_{^k{\bf x}\in G(i_{\mathcal T_1})}||\pi_{\mathcal T_1}(^k{\bf x})-\pi_{\mathcal T_2}(\gamma_{\epsilon}(^k{\bf x}))||_{\infty}^p<\epsilon
$$
Therefore we have $||{\bf z}-\pi_{\mathcal T_2}(\gamma_{\epsilon}(^k{\bf z}))||_{\infty}^p<\epsilon$. Take $\epsilon=1/2^{np}$ for $n=1,2,\cdots$ and denote $\pi_{\mathcal T_2}(\gamma_n(^k{\bf z}))$ by ${\bf z}_n$. If ${\bf z}_n={\bf z}$ for some large $n$, then ${\bf z}\in S_{\mathcal T_2}$ and $i_{\mathcal T_1}({\bf z})=i_{\mathcal T_2}(\bf z)$. If ${\bf z}_n$'s are distinct from ${\bf z}$, we have $||{\bf z}-{\bf z}_n||_{\infty}<1/2^n$. {%raw%}Writing in coordinates we find that $||\chi^{{\bf z}_n}_1||_{W_p}>||\chi^{\bf z}_1||_{W_p}-1/2^n$. Then $||\mathcal T_2||_{W_p}\ge (\sum_{r=n}^N||\chi_1^{{\bf z}_r}||_{W_p}^p)^{1/p}\ge (N-n)^{1/p}||\chi^{\bf z}_1||_{W_p}-(N-n)^{1/p-1}\frac{1}{2^{n-1}}${%endraw%}. The last inequality holds since $x^p$ is convex for $p\ge 1$. Let $N$ tend to infinity and we have a contradiction that $||\mathcal T_2||_{W_p}=\infty$. Over all, we conclude that $^k{\bf z}\in G(i_{\mathcal T_2})$. Hence $G(i_{\mathcal T_1})\subset G(i_{\mathcal T_2})$ and symmetry implies that $G(i_{\mathcal T_2})\subset G(i_{\mathcal T_1})$. i.e. $\mathcal T_1=\mathcal T_2$.

Let $\mathcal T_1,\mathcal T_2,\mathcal T_3\in\mathcal D_p$. If $W_p(\mathcal T_1,\mathcal T_2)=\infty$ or $W_p(\mathcal T_2,\mathcal T_3)=\infty$, then triangle inequality trivially holds. Otherwise, for any $\epsilon>0$, there are bijections $\gamma_1:G(i_{\mathcal T_1})\to G(i_{\mathcal T_2})$ and $\gamma_2:G(i_{\mathcal T_2})\to G(i_{\mathcal T_3})$ such that 
$$
\begin{aligned}
&(\sum_{^k{\bf x}\in G(i_{\mathcal T_1})}||\pi_{\mathcal T_1}(^k{\bf x})-\pi_{\mathcal T_2}(\gamma_1(^k{\bf x}))||_{\infty}^p)^{1/p}<W_p(\mathcal T_1,\mathcal T_2)+\epsilon/2\\
&(\sum_{^k{\bf y}\in G(i_{\mathcal T_2})}||\pi_{\mathcal T_2}(^k{\bf y})-\pi_{\mathcal T_3}(\gamma_2(^k{\bf y}))||_{\infty}^p)^{1/p}<W_p(\mathcal T_2,\mathcal T_3)+\epsilon/2
\end{aligned}
$$
Note that $\gamma_2\circ\gamma_1$ is a bijection from $G(i_{\mathcal T_1})$ to $G(i_{\mathcal T_3})$. Therefore, we have
$$
\begin{aligned}
& W_p(\mathcal T_1,\mathcal T_3)\le(\sum_{^k{\bf x}\in G(i_{\mathcal T_1})}||\pi_{\mathcal T_1}(^k{\bf x})-\pi_{\mathcal T_3}(\gamma_2\circ\gamma_1(^k{\bf x}))||_{\infty}^p)^{1/p}\\
&\le(\sum_{^k{\bf x}\in G(i_{\mathcal T_1})}(||\pi_{\mathcal T_1}(^k{\bf x})-\pi_{\mathcal T_2}(\gamma_1(^k{\bf x}))||_{\infty}+||\pi_{\mathcal T_2}(\gamma_1(^k{\bf x}))-\pi_{\mathcal T_3}(\gamma_2\circ\gamma_1(^k{\bf x}))||_{\infty})^p)^{1/p}\\
&\le(\sum_{^k{\bf x}\in G(i_{\mathcal T_1})}(||\pi_{\mathcal T_1}(^k{\bf x})-\pi_{\mathcal T_2}(\gamma_1(^k{\bf x}))||_{\infty}^p)^{1/p}+(\sum_{^k{\bf x}\in G(i_{\mathcal T_1})}(||\pi_{\mathcal T_2}(\gamma_1(^k{\bf x}))-\pi_{\mathcal T_3}(\gamma_2\circ\gamma_1(^k{\bf x}))||_{\infty}^p)^{1/p}\\
&\le W_p(\mathcal T_1,\mathcal T_2)+W_p(\mathcal T_2,\mathcal T_3)+\epsilon
\end{aligned}
$$
where the third line used Minkowski's inequality. Since $\epsilon$ is arbitrary, the triangle inequality holds.

**Corollary.** 

1. $W_p(\mathcal T_1,\mathcal T_2)<\infty$ for $\mathcal T_1,\mathcal T_2\in \mathcal D_p$;
2. Note that symmetry and triangle inequality holds for any persistence diagrams, but positive definiteness requires finiteness assumption; 
3. {%raw%}An off-diagonal point of $\mathcal T\in \mathcal D_p$ can not be a cluster point. i.e. for any off-diagonal point ${\bf x}$ in $S_{\mathcal T}$ there is an open ball $B_{\epsilon}({\bf x})$ such that $B_{\epsilon}({\bf x})\cap S_{\mathcal T}=\{{\bf x}\}$. As a consequence, for any $\mathcal T\in\mathcal D_p$, $G(i_{\mathcal T})\backslash G(0_{\Delta})$ is at most countable.{%endraw%}

**Definition.** A persistence diagram $\mathcal T\in\mathcal D_p$ is called constructible if $S_{\mathcal T}\backslash\Delta$ consists of finitely many points. The collection of all constructible persistence diagrams is denoted by $\mathcal C_p$. 

**Remark.** The name 'constructible' comes from the fact that any constructible persistence diagram can be obtained as a persistence diagram of a finite filtration of simplicial complexes.

**Theorem.** Let $\mathcal T\in\mathcal D_p$ be arbitrary and $\epsilon>0$ be any given positive number. There exists $\mathcal T_c\in\mathcal C_p$ and $\mathcal T_s\in\mathcal D_p$ such that $\mathcal T=\mathcal T_c+\mathcal T_s$ with $||\mathcal T_s||_{W_p}<\epsilon$.

**Proof.** Enumerate the off-diagonal points {%raw%}$\{{\bf x}_1,{\bf x}_2,\cdots\}=S_{\mathcal T}\backslash\Delta${%endraw%}. By definition,
$$
||\mathcal T||_{W_p}=(\sum_{n=1}^{\infty}||\chi^{\bf x_n}_{k_n}||_{W_p}^p)^{1/p}=(\lim_{l\to\infty}\sum_{||\chi^{\bf x_n}_1||_{W_p}\ge\frac{1}{l}}||\chi^{\bf x_n}_{k_n}||_{W_p}^p)^{1/p}<\infty
$$
Thus, for $\epsilon>0$, there exists $l>0$ such that $||\mathcal T||_{W_p}^p-\sum_{||\chi^{\bf x_n}_1||_{W_p}\ge\frac{1}{l}}||\chi^{\bf x_n}_{k_n}||_{W_p}^p<\epsilon^p$. Let $\mathcal T_u$ be the persistence diagram such that $S_{\mathcal T_u}$ consists of those points in $\mathcal T$ with $||\chi^{\bf x}_1||_{W_p}\ge 1/l$ and $i_{\mathcal T_u}$ is the restriction of $i_{\mathcal T}$ on $S_{\mathcal T_u}$, $\mathcal T_s$ be such that $S_{\mathcal T_s}$ consists of points with $||\chi^{\bf x}_1||_{W_p}<1/l$ and $i_{\mathcal T_s}$ is the restriction of $i_{\mathcal T}$ on $S_{\mathcal T_s}$. It is immediate that $\mathcal T_u\in\mathcal C_p$ and $||\mathcal T_s||_{W_p}<\epsilon$ and $\mathcal T=\mathcal T_u+\mathcal T_s$.

