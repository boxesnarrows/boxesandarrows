---
title: A combinatorial proof of the formula for the nth Fibonacci number
layout: post
categories: mathematics
tags:
    - combinatorics
    - fibonacci-numbers

sidebar: []
image: 
    path: "/assets/images/tree-expansion.png"
---

The aim of this post is to present a combinatorial proof of the formula for the $n$th fibonacci number. More generally, let $X\_n$ be a sequence such that $X_0, X_1$ are constants and $X\_n = X\_{n - 1} + X\_{n - 2}$ for $n \geq 2$. We shall prove that

$$ X\_n = \sum^{\left\lfloor \frac{n - 1}{2} \right\rfloor}\_{k = 0} \binom{n - k - 1}{k} X\_1 + \sum^{\left\lfloor \frac{n - 2}{2} \right\rfloor}\_{k = 0} \binom{n - k - 2}{k} X\_0 \; ,$$

where $\left\lfloor x \right\rfloor$ is the *floor function*, that is, it is defined as the greatest integer less than or equal to $x$.

We can compute $X\_n$ by using the relation $X\_n = X\_{n - 1} + X\_{n - 2}$ to expand the values recursively, until no term left can be expanded any further (that is, we have only $X\_0$s and $X\_1$s). We can look at this computation as if we were creating a tree from bifurcations of each term we expand. Consider the image below:

<img src="{{ 'assets/images/tree-expansion.png' | relative_url }}" alt="expansion-tree" style="width: 50%; height: auto;">

We can see, looking once again at the image above, that each final node ($X\_0$ or $X\_1$) has a unique path leading to it, which represents the previous (and expanded) terms from which such term originated (recursively) from. A path, here, consists in an ordered list of choices, which are either left or right. The left choice, for each node $X\_k$, yields $X\_{k - 1}$, and the right choice, $X\_{k - 2}$. The leftmost $X\_1$, for instance, originates from the path **[left, left, left, left]**, while the second $X\_0$ (from the left) originates from **[left, right, right]**. To make an analogy, if we created a recursive function to compute the list of $X\_0$s and $X\_1$s yielded from the expansion of $X\_n$, which would call itself on the values $X\_{n - 1}$ and $X\_{n - 2}$ recursively, then the path of each item would be the stack of calls from which it originated:
```
    f(5) -> [f(4), f(3)] : f(3) -> [f(2), f(1)] : f(2) -> [f(0)] : f(0) -> X0

    Stack of X0:
        f(5) -> f(3) -> f(2) -> f(0)
```

With that, we can solve the problem by counting the number of paths yielding a $X_0$ or a $X_1$, for all possible paths occur in an expansion.

First, let us count the number of possible paths leading to $X\_1$. Before counting the paths, let's consider them grouped by number of left choices and right choices. Such possible pairs of values must be the nonnegative integer solutions for

$$n - 2k - j = 1 \; ,$$

where $k$ is the number of left choices ($n - 2$) and $j$ the number of right choices ($n - 1$). To compute all the pairs of solutions, since the equation has only two variables, we just range over all the (possible) values of $k$, from $0$ to $\left\lfloor{\frac{n - 1}{2}} \right\rfloor$, and obtain $j$ from $j = n - 2k - 1$. With all pair of solutions $(j, k)$, we have all possible configurations of paths which lead to $X\_1$, up to number of choices for each option (left or right). Now we need to count the number of paths corresponding to each pair. To do that, we just need to consider the following: for each pair $(j, k)$, all such paths consist of $j + k$ choices. Moreover, if we choose the position (among the $j + k$ available) of each of the $j$ left choices, the path will be completely determined, for the $k$ right choices must fill the remaining positions, and permutating identical elements makes no difference. With that, we conclude that the number of distinct paths leading to $X\_1$ with $k$ left choices and $j$ right choices is $\binom{j + k}{j} = \binom{j + k}{k}$. Since we have the relation $j = n - 2k - 1$, the binomial coefficient can be rewritten as $\binom{n - k - 1}{k}$. We can therefore conclude that the number of distinct paths leading to $X\_1$ is

$$\sum^{\left\lfloor \frac{n - 1}{2} \right\rfloor}\_{k = 0} \binom{n - k - 1}{k} \; .$$

One might be tempted to conclude that the acse of $X_0$ is analogous, with equation

$$n - 2k - j = 0 \; .$$

The equation above, however, isn't appropriate. Consider, for instance, the two paths below:

<img src="{{ 'assets/images/paths.png' | relative_url }}" alt="expansion-tree" style="width: 50%; height: auto;">

We have a path **[left, right]** leading to $X\_0$, but whose permutation **[right, left]** is invalid! If we choose right first, we reach $X\_1$ and there's nothing else to do. In other words, if we count all paths with $j$ left choices and $k$ right choices, we'll be counting invalid paths, that is, paths which don't lead to $X_0$. In order to solve this problem, consider the following: every path leading to $X\_0$ must contain a $X\_2$, for if the last choice were **left**, we'd have $X_{k - 1} = X_0$, but then $k = 1$! Hence we conclude the last choice must always be **right**, which implies that the node before $X_0$ must be $X_2$. We must therefore count paths leading to $X_2$ instead. 

Our equation becomes

$$n - 2k - j = 2 \; ,$$

and everything follows analogously to the case of $X_1$, so that we obtain the formula

$$\sum^{\left\lfloor \frac{n - 2}{2} \right\rfloor}\_{k = 0} \binom{n - k - 2}{k} \; .$$

We can therefore conclude that the expansion of $X\_n$, when carried out, will yield the respective amounts of $X\_1$s and $X\_0$s, and hence we conclude that


$$X\_n = \sum^{\left\lfloor \frac{n - 1}{2} \right\rfloor}\_{k = 0} \binom{n - k - 1}{k} X\_1 + \sum^{\left\lfloor \frac{n - 2}{2} \right\rfloor}\_{k = 0} \binom{n - k - 2}{k} X\_0 \; .$$


The special case $X\_0 = 0$, $X\_1 = 1$ is that of the Fibonacci sequence:
$$F\_n = \sum^{\left\lfloor \frac{n - 1}{2} \right\rfloor}\_{k = 0} \binom{n - k - 1}{k} \; .$$


#### Relation to Pascal's Triangle

One of the properties of Pascal's Triangle is that the sum of the elements in its $n$th "shallow diagonal" is the $(n + 1)$th Fibonacci number.

<img src="{{ 'assets/images/pascal-triangle-fib.png' | relative_url }}" alt="expansion-tree" style="width: 50%; height: auto;">

Note that the $n$th shallow diagonal has its length increased by $1$ every $2$ lines, hence its length is given by $\left\lfloor \frac{n}{2} \right\rfloor$, and the value of the $k$th element (from right to left) of such line is $\binom{n - k}{k}$, hence both expressions coincide (for $F_{n + 1}$ instead of $F_n$).