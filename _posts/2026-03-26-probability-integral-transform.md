---
layout: post
title: "Probability Integral Transform"
date: 2026-03-26
categories: [theory]
tags: [probability, inverse-transform, PIT, measure-theory]
published: true
---

### Basic Definitions and Key Properties

Let a random variable $X$ have cumulative distribution function (CDF)
$$
\begin{align}
F_X(x)=\mathbb{P}(X\le x),\qquad x\in\mathbb{R}.
\end{align}
$$

Define the generalized inverse CDF as
$$
\begin{align}
F_X^{-1}(u)=\inf\{x\in\mathbb{R}:F_X(x)\ge u\},\qquad u\in(0,1).
\end{align}
$$

This definition applies to discrete, continuous, and mixed distributions.  
Unlike the usual inverse function, the generalized inverse does not require $F_X$ to be strictly monotonic, and therefore remains well-defined even in the presence of jumps or flat regions.

The generalized inverse satisfies the following fundamental equivalence: for any $x\in\mathbb{R}$ and $u\in(0,1)$,
$$
\begin{align}
F_X^{-1}(u)\le x \iff u\le F_X(x).
\end{align}
$$

**Proof.** 
If $F_X^{-1}(u)\le x$, then by the monotonicity of $F_X$,
$$
\begin{align}
F_X(F_X^{-1}(u))\le F_X(x),
\end{align}
$$
and by the definition of the generalized inverse, $F_X(F_X^{-1}(u))\ge u$, hence $u\le F_X(x)$.
Conversely, if $u\le F_X(x)$, then $x$ belongs to the set $\{t:F_X(t)\ge u\}$, and thus its infimum satisfies $F_X^{-1}(u)\le x$.
$\blacksquare$

Taking the negation of the above equivalence yields
$$
\begin{align}
F_X(x)<u \iff x<F_X^{-1}(u),
\end{align}
$$
which also plays an important role in the proof of the probability integral transform.

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

Then for any distribution function $F_X$,
$$
\begin{align}
Z\sim F_X.
\end{align}
$$

**Proof.**
For any $z\in\mathbb{R}$,
$$
\begin{align}
\mathbb{P}(Z\le z)
&=\mathbb{P}\big(F_X^{-1}(U)\le z\big) \\
&=\mathbb{P}\big(U\le F_X(z)\big) \\
&=F_X(z).
\end{align}
$$
The second step uses the fundamental equivalence above, and the third step uses the uniform distribution of $U$. Hence the distribution function of $Z$ is exactly $F_X$.
$\blacksquare$

Therefore, inverse transform sampling holds for discrete, continuous, and mixed distributions. The role of the generalized inverse is to unify the non-strictly monotone case: when $F_X$ is a step function or has flat regions, $F_X^{-1}$ can still uniquely map $u\in(0,1)$ to the corresponding sample.

### Probability Integral Transform (Continuous Case)

If $F_X$ is continuous, define
$$
\begin{align}
U=F_X(X),
\end{align}
$$
then
$$
\begin{align}
U\sim \mathrm{Unif}(0,1).
\end{align}
$$

**Proof.** For any $u\in[0,1]$,
$$
\begin{align}
\mathbb{P}(U\le u)
&=\mathbb{P}\big(F_X(X)\le u\big).
\end{align}
$$

Since $F_X$ is continuous, there exists $x_u$ such that
$$
\begin{align}
F_X(x_u)=u.
\end{align}
$$

By monotonicity of $F_X$,
$$
\begin{align}
\{F_X(X)\le u\}=\{X\le x_u\},
\end{align}
$$

thus
$$
\begin{align}
\mathbb{P}(U\le u)
=\mathbb{P}(X\le x_u)
=F_X(x_u)
=u.
\end{align}
$$
Hence $U$ follows the standard uniform distribution.
$\blacksquare$

This shows that in the continuous case, a random variable can be mapped to a uniform distribution through its own CDF.

### Probability Integral Transform (General Case with External Randomization)

When $X$ has discrete components, $F_X$ may have jumps. In this case, directly taking $U=F_X(X)$ does not yield a uniform distribution. To handle the general case, introduce an independent random variable
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

**Proof.** For any $u\in[0,1]$, define
$$
\begin{align}
x_u=\inf\{x:F_X(x)\ge u\}=F_X^{-1}(u).
\end{align}
$$

From the definition of the generalized inverse,
$$
\begin{align}
F_X(x_u^-)\le u\le F_X(x_u).
\end{align}
$$

Conditioned on $X=x$, the random variable $U$ is uniformly distributed over the interval
$$
\begin{align}
[F_X(x^-),\,F_X(x)].
\end{align}
$$

Therefore,
$$
\begin{align}
\mathbb{P}(U\le u\mid X=x)=
\begin{cases}
0, & u<F_X(x^-),\\[4pt]
\dfrac{u-F_X(x^-)}{F_X(x)-F_X(x^-)}, & F_X(x^-)\le u\le F_X(x),\\[10pt]
1, & u>F_X(x).
\end{cases}
\end{align}
$$

Taking expectation over $X$, note that only those $x$ satisfying
$$
\begin{align}
F_X(x^-)<u\le F_X(x)
\end{align}
$$
contribute partially, and by definition of $x_u$, such points correspond at most to $x=x_u$. Hence,
$$
\begin{align}
\mathbb{P}(U\le u)
=
\mathbb{P}(X<x_u)
+
\mathbb{P}(X=x_u)\,
\frac{u-F_X(x_u^-)}{F_X(x_u)-F_X(x_u^-)}.
\end{align}
$$

Since
$$
\begin{align}
\mathbb{P}(X<x_u)=F_X(x_u^-),\qquad
\mathbb{P}(X=x_u)=F_X(x_u)-F_X(x_u^-),
\end{align}
$$
we obtain
$$
\begin{align}
\mathbb{P}(U\le u)
&=
F_X(x_u^-)
+
\big(F_X(x_u)-F_X(x_u^-)\big)
\frac{u-F_X(x_u^-)}{F_X(x_u)-F_X(x_u^-)} \\
&=u.
\end{align}
$$

Thus
$$
\begin{align}
U\sim \mathrm{Unif}(0,1).
\end{align}
$$
$\blacksquare$

When $F_X$ is continuous, $F_X(x^-)=F_X(x)$, and the above reduces to
$$
\begin{align}
U=F_X(X),
\end{align}
$$
recovering the classical probability integral transform.

### Probability Integral Transform (General Case: Without External Randomization)

If no additional randomization is introduced and we directly define
$$
\begin{align}
U=F_X(X),
\end{align}
$$
then when $F_X$ is not continuous, $U$ generally does not follow the standard uniform distribution. However, it still satisfies the **sub-uniformity** property:
$$
\begin{align}
\mathbb{P}(U\le u)\le u,\qquad \forall u\in[0,1].
\end{align}
$$

Moreover,
$$
\begin{align}
\mathbb{P}(U\le u)=u \iff u\in \mathrm{Range}(F_X),
\end{align}
$$
where
$$
\begin{align}
\mathrm{Range}(F_X)=\{F_X(x):x\in\mathbb{R}\}
\end{align}
$$
denotes the range of the CDF.

**Proof.** Using the previously established relation
$$
\begin{align}
F_X(x)<u \iff x<F_X^{-1}(u),
\end{align}
$$
we obtain
$$
\begin{align}
\mathbb{P}(U<u)
&=\mathbb{P}\big(F_X(X)<u\big) \\
&=\mathbb{P}\big(X<F_X^{-1}(u)\big) \\
&=F_X\big(F_X^{-1}(u)^-\big) \\
&\le u.
\end{align}
$$

Next, we distinguish two cases for $\mathbb{P}(U\le u)$.

**Case 1: $u\notin \mathrm{Range}(F_X)$**

In this case, there is no $x$ such that $F_X(x)=u$. Hence the events $\{U\le u\}$ and $\{U<u\}$ coincide, and thus
$$
\begin{align}
\mathbb{P}(U\le u)=\mathbb{P}(U<u)\le u.
\end{align}
$$

**Case 2: $u\in \mathrm{Range}(F_X)$**

In this case, there exists some $x^*$ such that
$$
\begin{align}
F_X(x^*)=u.
\end{align}
$$

Thus,
$$
\begin{align}
\mathbb{P}(U\le u)
&=\mathbb{P}\big(F_X(X)\le F_X(x^*)\big) \\
&=\mathbb{P}(X\le x^*) \\
&=F_X(x^*) \\
&=u.
\end{align}
$$
$\blacksquare$

In summary, the distribution function of $F_X(X)$ always lies below the diagonal $y=u$, and achieves equality only when $u$ belongs to the range of $F_X$. In other words, without external randomization, the probability integral transform yields a sub-uniform variable rather than a truly uniform one.

### Unified Conclusion

The above results show that:

- Inverse transform sampling always holds in the general case: if $U\sim\mathrm{Unif}(0,1)$, then
$$
\begin{align}
F_X^{-1}(U)\sim F_X.
\end{align}
$$

- In the continuous case, the probability integral transform can be written directly as
$$
\begin{align}
F_X(X)\sim \mathrm{Unif}(0,1),
\end{align}
$$

- In the discrete or mixed case, independent randomization is required:
$$
\begin{align}
U=F_X(X^-)+V\big(F_X(X)-F_X(X^-)\big)
\end{align}
$$
to recover uniformity.

- Without external randomization, $F_X(X)$ generally only satisfies sub-uniformity:
$$
\begin{align}
\mathbb{P}(F_X(X)\le u)\le u.
\end{align}
$$

- The generalized inverse is the key tool for unifying discrete, continuous, and mixed distributions, and underlies both inverse transform sampling and the generalized probability integral transform.

Therefore, the probability integral transform and inverse transform sampling describe two directions of the same principle: on one hand, any distribution can be generated from a uniform distribution via the generalized inverse mapping; on the other hand, any random variable can be mapped to a uniform distribution (with appropriate randomization) via its CDF. Formally,
$$
\begin{align}
\text{Any distribution}
\;\Longleftrightarrow\;
\text{Uniform}(0,1)+\text{generalized inverse}.
\end{align}
$$
