---
title: "Convex Hull"
date: 2025-08-18
draft: false
tags: ["convex optimization", "convex hull", "convex set"]
---

## Convex Hull

Statement:

Given a set of points $S = \{v_1, v_2, \ldots, v_n\}$, the convex hull of $S$ is all the possible convex combination of the points in $S$, and is the smallest convex set that contains $S$.

## Proves

To prove the statement, we need to prove the following two statements:

1. The convex hull of $S$ is a convex set.
2. The convex hull of $S$ is the smallest convex set that contains $S$.

### Proof of first statement

Represent all the possible convex combination of the points in $S$:

$$
CV(S) = \{ \sum_{i=1}^n \theta_i v_i | \theta_i \ge 0, \sum_{i=1}^{n} \theta_i = 1 \}
$$

CV(S) is a union of all the convex combination of the points in $S$. For any single point $a$ in $S$, we also have $a \in CV(S)$.

To prove $CV(S)$ is a convex set, we need to prove given any 2 points $a, b$ in CV(S), the line segment between $a$ and $b$ is also in CV(S).

Given any two points $a, b$ in $CV(S)$, point $a, b$ can be written as:

$$
a = \sum_{i=1}^n \theta_i v_i
$$

$$
b = \sum_{i=1}^m \phi_i v_i
$$


we can apply a convex combination to get a new point $p$ (where $\sum_{i=1}^{n} \theta_i = 1$ and $\theta_i \ge 0$):

$$
p = \lambda a + (1-\lambda) b
$$

$\implies p$ can be written as:

$$
p = \lambda \sum_{i=1}^n \theta_i v_i + (1-\lambda) \sum_{i=1}^m \phi_i v_i
$$

we can easily find that $\sum_{i=1}^{n} \lambda \theta_i + \sum_{i=1}^{m} (1-\lambda) \phi_i = 1$ and $\lambda \theta_i, (1-\lambda) \phi_i \ge 0$. $\implies p \in CV(S)$.

Hence, based on the definition of convex set, $CV(S)$ is a convex set.



## Proof of second statement

Given following proposition:

Proposition:

If A set $T$ is a convex set for points $x_1, x_2 .. x_n$ in $T$, the convex combination of these points is also in $T$. 

Proof:

if $n = 0, 1, 2$, given any convex set $T$, the convex combination of any two points in $T$ is also in $T$.

if $n > 2$, we can prove by induction.

Assume the proposition is true for $n = k$, we need to prove the proposition is true for $n = k+1$. 

For a convex combination of $k$ points in $T$, we can write it as:

$$
p = \sum_{i=1}^k \theta_i x_i
$$

where $\sum_{i=1}^{k} \theta_i = 1$ and $\theta_i \ge 0$, $p \in T$. 

For any point $v_{k+1} \in S$, we can write $k$ points convex combination as:

$$
p_{k+1} = \lambda p_{k} + (1-\lambda) x_{k+1}
$$

which can be written as the result we want to prove:

$$
p_{k+1} = \sum_{i=1}^{k+1} \alpha_i x_i
$$

where $\sum_{i=1}^{k+1} \alpha_i = 1$ and $\alpha_i \ge 0$.

Hence, the proposition is true for $n = k+1$.

By induction, the proposition is true for any $n$.

Indeed, there is a convex set $T$, that $T \supe S $,

given points $x_1, x2, .. x_n$ in $S$, i.e. also in $T$, their convex combination is also in $T$ based on the proposition. Hence every point in $Cov S$ also in $T$. Hence $Cov S$ is the smallest convex set that contains $S$.


Ref:

- https://math.stackexchange.com/questions/2240533/prove-convex-hull-is-convex
- https://www.math.drexel.edu/~tyu/Math690Optimization/lec6.pdf
- https://ti.inf.ethz.ch/ew/courses/CG13/lecture/Chapter%203.pdf 