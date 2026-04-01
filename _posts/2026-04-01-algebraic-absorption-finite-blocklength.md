---
layout: post
title: "Algebraic Absorption of Finite-Blocklength Corrections via q-Logarithms"
date: 2026-04-01
categories: [theory]
tags: [information-theory, finite-blocklength, q-logarithm, edgeworth, asymptotics]
published: true
---

### Finite-Blocklength Setting and Limitation of Normal Approximation

Consider the information density
$$
\begin{align}
S_n := -\ln P(X^n) = \sum_{i=1}^n -\ln P(X_i),
\end{align}
$$
with mean $nH_1$ and variance $nV$.

The second-order approximation gives
$$
\begin{align}
L^*(n,\epsilon)
= nH_1 + \sqrt{nV} Q^{-1}(\epsilon) + O(1).
\end{align}
$$

This approximation relies on a Gaussian approximation of $S_n$. For short blocklength or asymmetric sources, the distribution of $S_n$ exhibits non-negligible skewness and kurtosis, leading to systematic deviations.

### Classical Higher-Order Correction

**Definition 1.**
<em>
The third-order expansion via Edgeworth correction takes the form
$$
\begin{align}
L^*(n,\epsilon)
= nH_1 + \sqrt{nV} Q^{-1}(\epsilon)
+ B(T,\epsilon) + O(n^{-1/2}),
\end{align}
$$
where $T$ denotes the third central moment.
</em>

This approach introduces correction terms through Hermite polynomials. The complexity increases rapidly when higher-order moments are incorporated.

### q-Logarithmic Mapping

To incorporate higher-order effects structurally, consider the $q$-logarithm
$$
\begin{align}
\ln_q x = \frac{x^{1-q}-1}{1-q}.
\end{align}
$$

Its local expansion around $q=1$ is
$$
\begin{align}
\ln_q x
= \ln x + \frac{1-q}{2}(\ln x)^2 + O((1-q)^2).
\end{align}
$$

Applying this to $S_n$ yields
$$
\begin{align}
S_q(X^n)
= S_n + \frac{1-q}{2} S_n^2 + O((1-q)^2).
\end{align}
$$

Since $S_n = O(n)$, the quadratic term scales as $O(n^2)$, which dominates the expansion.

### Centralization

Define the fluctuation
$$
\begin{align}
W_n := S_n - nH_1,
\end{align}
$$
which satisfies $W_n = O(\sqrt{n})$.

**Definition 2.**
<em>
The centralized q-generalized information density is defined as
$$
\begin{align}
S_{q_n}(X^n)
= nH_1
+ \frac{\exp((1-q_n)W_n)
- \mathbb{E}[\exp((1-q_n)W_n)]}{1-q_n}.
\end{align}
$$
</em>

This construction preserves the mean, i.e.,
$$
\begin{align}
\mathbb{E}[S_{q_n}(X^n)] = nH_1.
\end{align}
$$

### Dynamic Scaling Law

**Proposition 1.**
<em>
To obtain a non-trivial finite-blocklength correction, the parameter must satisfy
$$
\begin{align}
1 - q_n = O(n^{-1}).
\end{align}
$$
</em>

Expanding the definition gives
$$
\begin{align}
S_{q_n}(X^n)
= nH_1 + W_n
+ \frac{1-q_n}{2}(W_n^2 - nV)
+ O((1-q_n)^2).
\end{align}
$$

Since $W_n^2 = O(n)$, the term $(1-q_n)W_n^2$ is of order $O(1)$ under this scaling.

### Matching the Third-Order Expansion

Under the Gaussian approximation $W_n = \sqrt{nV} Z$, one obtains
$$
\begin{align}
S_{q_n}
= nH_1 + \sqrt{nV} Z
+ \frac{1-q_n}{2} nV (Z^2 - 1) + O(n^{-1/2}).
\end{align}
$$

**Theorem 1.**
<em>
Let $1-q_n = \alpha n^{-1}$. If
$$
\begin{align}
\alpha = \frac{T}{3V^2},
\end{align}
$$
then the induced correction coincides with the third-order Edgeworth expansion.
</em>

Indeed,
$$
\begin{align}
\frac{\alpha V}{2}(Z^2-1)
= \frac{T}{6V}(Z^2-1).
\end{align}
$$

### Higher-Order Structure

**Theorem 2.**
<em>
Under the scaling $1-q_n = O(n^{-1})$, the $k$-th order term satisfies
$$
\begin{align}
O(n^{1-k/2}),
\end{align}
$$
which matches the asymptotic order of the $(k+1)$-th moment correction in the Edgeworth expansion.
</em>

This yields:

- $k=1$: $O(\sqrt{n})$
- $k=2$: $O(1)$
- $k=3$: $O(n^{-1/2})$

### Structural Interpretation

The classical approach treats higher-order effects as additive corrections to a Gaussian baseline. In contrast, the q-algebraic framework embeds these corrections into the algebraic structure of the information measure.

The centralization step introduces a moment-generating-function normalization, which is closely related to exponential tilting techniques in large deviation theory.

### Summary

- The normal approximation captures only second-order fluctuations.
- Higher-order corrections arise from non-Gaussian behavior of $S_n$.
- The q-logarithmic mapping generates higher-order terms intrinsically.
- The scaling law $1-q_n = O(n^{-1})$ ensures correct asymptotic magnitude.
- Proper tuning recovers the third-order term without explicit polynomial corrections.

### References

This note is based on:
- H. Suyari, “Unified Algebraic Absorption of Finite-Blocklength Penalties via Generalized Logarithmic Mapping,” arXiv, 2026. [arXiv:2603.22358](https://arxiv.org/abs/2603.22358)
