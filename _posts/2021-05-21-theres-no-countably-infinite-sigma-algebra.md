---
title: There's no countably infinite sigma algebra!
layout: post
categories: mathematics
tags:
    - sigma-algebra
    - measure-theory

sidebar: []
image: 
    path: "/assets/images/infinite-path-collection.png"
---

To show this, let $\mathcal{A} \subseteq \mathcal{P}{(X)}$ be our $\sigma$-algebra. If we could show there's a countable family $\mathcal{F} = \\{ A_i  \\}$ of disjoint sets in $\mathcal{A}$, we could establish a bijection between $2^\mathbb{N}$ and the unions in $\mathcal{F}$ as follows:

$$
A^f_i =
\begin{cases}
\emptyset, && f(i) = 0 \\
A_i, && f(i) = 1
\end{cases}
\; ,
\hspace{5mm}
f \to \bigcup^\infty_{i = 0} A^f_i \; .
$$

Since $\mathcal{A}$ is a $\sigma$-algebra, it contains all such unions, so it contains uncountably many different sets.

So it suffices to show that on the assumption $\mathcal{A}$ contains infinitely many members, it must contain an infinite family of disjoint sets. Our strategy for obtaining such family is intuitively simple: we start with a set and its complement $C_1 = \\{ A, A^c \\}$, find a set which intersects one "partially" (that is, neither the set nor its complement are disjoint), so we can "split" the set: $\\{ A, A^c \\} \to \\{ B \cap A, B^c \cap A, A^c \\}$, and denote this new collection by $C_2$.

<img src="{{ 'assets/images/set-splitting.png' | relative_url }}" alt="expansion-tree" style="width: 50%; height: auto;">

How do we find such set? Since each $C_i$ is finite, we collect all unions of elements in C_i, which are finitely many, and discard them, leaving infinitely many sets remaining. Then any remaining set that we pick must intersect some member of $C_i$ "partially", otherwise it would be an union of the members of $C_i$. This we can construct $C_1, C_2, C_3, \dots$. We view this process as a tree whose nodes are sets with bifurcations leading to the "split" subsets:

<img src="{{ 'assets/images/set-splitting-tree.png' | relative_url }}" alt="expansion-tree" style="width: 50%; height: auto;">

Now, since a tree with $2$ branches at each node and paths of length at most $n$ must have at most $2^{n - 1}$ branches, and so, since our process is infinite, we must have paths of arbitrary size, so our tree resulting from such process cannot be finite. More formally, we can consider the $T_i$ from $C_i$ as a set of sequences of members of $C_i$ representing paths, and so we define our resulting tree as $T = \bigcup^\infty T_i$.

Now, we apply Kőnig's lemma: since our tree is infinite and finitely branching (more precisely, bifurcating), we must have an infinite path. Then, considering such path, since each node bifurcates, for the $i$th node in the path, we have a bifurcation where one branch leads to some other node and the other to the $(i + 1)$th node in the path, and we collect the subset corresponding to such other node. We thus have a sequence $s_1, s_2, \dots$ of collected subsets such that (denoting by $p_i$ the subset corresponding to the $i$th node in our infinite path) $s_i \subseteq p_{i - 1}$, $p_i \cap s_i = \emptyset$, which follows from the cosntruction of our tree, hence $d_1, d_2, \dots$ is the desired infinite set of disjoint sets.

<img src="{{ 'assets/images/infinite-path-collection.png' | relative_url }}" alt="expansion-tree" style="width: 20%; height: auto;">

