---
layout: post
title: "Probability Integral Transform and Inverse Transform Sampling"
date: 2026-03-26
categories: [theory]
tags: [probability, inverse-transform, PIT, measure-theory]
published: true
---

## Unified Formulation of Probability Integral Transform and Inverse Sampling

### Basic Definitions and Key Properties

Let a random variable $X$ have CDF
$$
\begin{align}
F_X(x)=\mathbb{P}(X\le x),\qquad x\in\mathbb{R}.
\end{align}
$$

Define the generalized inverse
$$
\begin{align}
F_X^{-1}(u)=\inf\{x\in\mathbb{R}:F_X(x)\ge u\},\qquad u\in(0,1).
\end{align}
$$

This definition applies to discrete, continuous, and mixed distributions.

The key equivalence:
$$
\begin{align}
F_X^{-1}(u)\le x \iff u\le F_X(x).
\end{align}
$$

Proof. If $F_X^{-1}(u)\le x$, by monotonicity,
$$
\begin{align}
F_X(F_X^{-1}(u))\le F_X(x),
\end{align}
$$
and by definition $F_X(F_X^{-1}(u))\ge u$, hence $u\le F_X(x)$.

Conversely, if $u\le F_X(x)$, then $x$ belongs to $\{t:F_X(t)\ge u\}$, so $F_X^{-1}(u)\le x$.

Taking complement:
$$
\begin{align}
F_X(x)<u \iff x<F_X^{-1}(u).
\end{align}
$$

### Inverse Transform Sampling (General Case)

Let
$$
\begin{align}
U\sim \mathrm{Unif}(0,1),
\end{align}
$$

and define
$$
\begin{align}
Z=F_X^{-1}(U).
\end{align}
$$

Then
$$
\begin{align}
Z\sim F_X.
\end{align}
$$

Proof:
$$
\begin{align}
\mathbb{P}(Z\le z)
&=\mathbb{P}\big(F_X^{-1}(U)\le z\big) \\
&=\mathbb{P}\big(U\le F_X(z)\big) \\
&=F_X(z).
\end{align}
$$

### Probability Integral Transform (Continuous Case)

If $F_X$ is continuous, define
$$
\begin{align}
U=F_X(X).
\end{align}
$$

Then
$$
\begin{align}
U\sim \mathrm{Unif}(0,1).
\end{align}
$$

Proof:
$$
\begin{align}
\mathbb{P}(U\le u)
&=\mathbb{P}\big(F_X(X)\le u\big).
\end{align}
$$

There exists $x_u$ such that
$$
\begin{align}
F_X(x_u)=u.
\end{align}
$$

Thus
$$
\begin{align}
\{F_X(X)\le u\}=\{X\le x_u\},
\end{align}
$$

so
$$
\begin{align}
\mathbb{P}(U\le u)
=\mathbb{P}(X\le x_u)
=F_X(x_u)
=u.
\end{align}
$$

### Probability Integral Transform (General Case with Randomization)

Let
$$
\begin{align}
V\sim \mathrm{Unif}(0,1),\qquad V\perp X,
\end{align}
$$

and define
$$
\begin{align}
U=F_X(X^-)+V\big(F_X(X)-F_X(X^-)\big),
\end{align}
$$

where
$$
\begin{align}
F_X(x^-)=\lim_{t\uparrow x}F_X(t).
\end{align}
$$

Then
$$
\begin{align}
U\sim \mathrm{Unif}(0,1).
\end{align}
$$

### Probability Integral Transform Without Randomization

If
$$
\begin{align}
U=F_X(X),
\end{align}
$$

then
$$
\begin{align}
\mathbb{P}(U\le u)\le u,\qquad \forall u\in[0,1].
\end{align}
$$

and
$$
\begin{align}
\mathbb{P}(U\le u)=u \iff u\in \mathrm{Range}(F_X).
\end{align}
$$

where
$$
\begin{align}
\mathrm{Range}(F_X)=\{F_X(x):x\in\mathbb{R}\}.
\end{align}
$$

### Unified Conclusion

- Inverse transform sampling:
$$
\begin{align}
F_X^{-1}(U)\sim F_X.
\end{align}
$$

- Continuous case:
$$
\begin{align}
F_X(X)\sim \mathrm{Unif}(0,1).
\end{align}
$$

- General case:
$$
\begin{align}
U=F_X(X^-)+V\big(F_X(X)-F_X(X^-)\big).
\end{align}
$$

- Without randomization:
$$
\begin{align}
\mathbb{P}(F_X(X)\le u)\le u.
\end{align}
$$

### Key Insight

$$
\begin{align}
\text{Any distribution}
\;\Longleftrightarrow\;
\text{Uniform}(0,1) + \text{generalized inverse}.
\end{align}
$$
