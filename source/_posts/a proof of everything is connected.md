---
title: A Proof of 'Everything is connected'
date: 2019-07-14 08:14:28
tags: About My Blog
categories: About-My-Blog
---

## Stories

The idea about building my own blog was originated from a long time ago when I first read [Terry Tao's homepage](https://terrytao.wordpress.com/). In 2019, when I became a graduate student, I realized it is necessary to write down the mathematics to keep track of my research. Honestly speaking, repetitions and failures really make one suffer. It is those tiny progresses that encourage me to hold on.

<!--more-->

The title of this blog comes from an [essay](https://mp.weixin.qq.com/s?__biz=MjM5NDEzNjI0Mg==&mid=2698897605&idx=1&sn=a19cb1dd989bbb6740345ceb476b01a7&chksm=83a52118b4d2a80e6d4254aa2dac5442302180583a257c251e051a33f18b3a4a7a993d68cd36&mpshare=1&scene=1&srcid=0716ytVjaAJNShmEwGSlmWpF&key=dd5051400a9fb58f808d2da53b802b8acf4d01cc85436ece84b72433ba3fd12b83709bd533967b30d98fcbb2cafbb52010be54affd44f1114534efd269163755ef08943a54bd6644af14d7e46d5cd77b&ascene=1&uin=MTU3ODQ1MjIwNg%3D%3D&devicetype=Windows+10&version=62060833&lang=zh_CN&pass_ticket=hrTohvqyTgd41p4viiU31IowGnkdWinCUMu%2FwVIpE0dlQBF2lbrj1dBRey65qCVn) which ingeniously describes a philosophy, that every thing, every event, every people are connected with each other. Like [da Vinci](https://en.wikipedia.org/wiki/Leonardo_da_Vinci) said, *Learn how to see. Realize that everything connects to everything else*. When I read these, a great idea hit me that I could formulate a mathematical proposition and prove it. Though the proof seems naive, I was happy to find such an explanation. 

## Modeling

Let us recall some basics from [probabilistic graphical model](https://en.wikipedia.org/wiki/Graphical_model). We use random variables to represent true events in real life. The relationship between events is modeled by **conditional independence**. Suppose $X,Y$ and $Z$ are three random variables. If the joint probability density function of $X,Y$ and $Z$ satisfy the following equation

$$f(x,y|z)=f(x|z)f(y|z),$$ 

$X$ and $Y$ are said to be conditional independent given $Z$. It generalizes the concept of **independence** where we known nothing prior ($Z=\emptyset$). In our case, it is reasonable that two events have no relationship if they are independent when we know all the other things.

Now we can construct a graph based on the above argument. The vertices are random variables. Two distinct vertices are connected by an edge if they are not conditional independent. One event is 'connected' to another if there is a path joining them. Therefore, when we say 'Everything is connected', we actually mean that the graph is connected.

However, we should be cautious about 'everything' since we just considered finite number of events. Given arbitrary $n$ events, we can say 'These $n$ things are connected' if the corresponding graph is connected. But it is too stupid to say such things, and we are not going to infer whether a graph is connected, either. Instead, let us look at the probability that a graph with $n$ nodes is connected.

## Proof

Let $\mathbb{G}_n$ be the space of undirected simple graphs with $n$ nodes. $\mathbb{G}_n$ is a finite set with $2^\frac{n(n-1)}{2}$ elements. Let $\mathbb{G}_n^c$ be the subset of all connected graphs, $\mathbb G_n^d$ be the subset of all disconnected graphs. Define the connectivity ratio 

$$R_n=\frac{ \#(\mathbb{G}_n^d)}{ \#(\mathbb{G}_n)}:=\frac{K_n^d}{K_n^c+K_n^d}.$$

where we have $K_n^c+K_n^d=2^\frac{n(n-1)}{2}$.

Let $v_0,v_1,\cdots,v_n$ be vertices of a graph $G\in\mathbb{G}_{n+1}^d$. Suppose $C_0$ is the component containing $v_0$ with $i$ points. Let $C_1$ be the complement of $C_0$ with $n+1-i$ points. The we have the following recursion 

$$K_{n+1}^d=\sum_{i=1}^n\binom{n}{i-1}K_i^c2^\frac{(n+1-i)(n-i)}{2}.$$

Dividing both sides by $2^\frac{(n+1)n}{2}$, we have

$$R_{n+1}=\sum_{i=1}^n\binom{n}{i-1}(1-R_i)2^\frac{-i(n+1-i)}{2}.$$  

Note that $1-R_i<1$ when $i>1$. Multiply both sides by $2^n$,

$$2^nR_{n+1}<1+n+\sum_{i=2}^{n-1}\binom{n}{i-1}2^{-(n-i)(i-1)}.$$

When $1<i<n$, $2^{-(n-i)(i-1)}<2^{-(n-2)}$. We obtain that $2^nR_{n+1}<n+5$. That is, the connectivity ratio $R_n<\frac{n+4}{2^{n-1}}$. When $n$ tends to infinity, $R_n$ tends to $0$.

Given arbitrarily $n$ events, we are right to guess that they are connected with probability greater than $1-\frac{n+4}{2^{n-1}}$. The probability grows with respect to the number of events. When $n$ goes to infinity, we are 100% certain that 'Everything is connected'!









  

##   

 