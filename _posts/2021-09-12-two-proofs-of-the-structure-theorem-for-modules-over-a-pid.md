---
title: Two proofs of the structure theorem for modules over a PID
layout: post
categories:
- mathematics
tags:
- commutative-algebra
- modules
sidebar: []
---

We consider $p$-primary modules, since the primry decomposition is pretty straightforward.
#### Proof 1: Simple, using pure submodules
For reference, a **simple submodule** $S$ is such that $rx = a\in S$ impplies there's $s \in S$ with $rs = a$. Moreover, a $A$-module $M$ is called **divisible** if for every $r \in A, m \in M$ there's $n \in M$ with $rn = m$.

With that said, it is easy to see a finitely generated torsion module cannot be divisible, or there would not be a largest prime power. We shall show every $p$-primary module which is not divisible has a cyclic pure submodule.

First, since $M$ is not divisible, we can take some $m \in M$ with the property that $m \notin pM$ of minimal order, that is, with smallest prime power. Now, suppose $np^j n = p^k m$. We can write this way because $A$ is a PID hence an UFD, and we can cancel any other factor on the right hand but the powers of $p$. Now, if $j \leq k$, we are done. If $p^km = 0$, we are done as well. Otherwise, write $p^k (p^{j - k} (na) - m)$. Note that the expression inside cannot be in $pM$ lest $m$ be there too, but it has strictly smaller order, contradicting the minimality of order of $m$ with this property.

Now, back to our $p$-primary module, we show $\langle m \rangle$ is a direct summand, where $m$ generates the pure submodule. We go like this: we call a subset $X$ of $M$ pure-independent if its generated submodule $K = \langle X \rangle$ is pure and $\sum a_i x_i = 0 \implies a_i x_i = 0$, for $x_i \in X$, a slightly different version of linear independency. Now, start with $X$ empty and take $N = M/K$. Then we get a pure generator $\overline{m}$ in $N$. Let $m$ be any element in its class. Then if $p^k$ is the order of $\overline{m}$, $p^k m \in K$. but $K$ is pure so $p^k m = p^k n$, $n \in K$. Let $w = m - n$. Then it is in the same class as $m$, and has the same order as $\overline{m}$ in $M/K$. Now, let $X^\prime = X \cup \\{ w \\}$. Then we show $X$ is pure-independent: $\sum m_i x_i = rw \implies \overline{rw} = 0$, thus $rw = 0$, so all summands are $0$. Now, let $rv \in K^\prime = \langle X^\prime \rangle$. Then $rv = \sum m_i x_i + sw$, so $\overline{rv} = \overline{sw}$, thus $\overline{rkw} = \overline{rv}$, so $rv - r(kw) = \sum n_i x_i = r(\sum k_i x_i)$, thus $K^\prime$ is pure, and a direct sum of cyclic modules.

This process must eventually stop since $M$ is Noetherian. Alternatively, we can use Zorn's Lemma to show there's a maximal pure-independent subset, with generated submodule $K$, such that $M/K$ must be divisible by maximality, hence $M/K = \\{ 0 \\}$.

#### Proof 2: Nice, but using some results
Baer's criterion gives a sufficient condition for a $A$-module to be injective: every map from an ideal to $M$ can be extended to the whole ring. Now, by Baer's criterion we can show that if $A$ is a PID and $a \in A$ neither $0$ nor an unit, $A/(a)$ is injective over itself. Using this, we take any element $m$ of maximal order in $M$. Then $\langle m \rangle \cong A/\langle p^n \rangle$ is self-injective, and $M$ is the same as a $A/\langle p^n \rangle$-module, hence $\langle a \rangle$ is a direct summand inside $M$, so $M = \langle a \rangle \oplus N$. Now, since each new module is a direct summand, this process must eventually stop, since $M$ is Noetherian.
