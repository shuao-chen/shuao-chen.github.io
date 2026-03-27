---
layout: post
title: "Determinant vs Pseudo-Determinant"
date: 2026-03-27
categories: [theory]
tags: [linear-algebra, determinant, pseudo-determinant, eigenvalues]
published: true
---

### Why $\det(AB)=\det(A)\det(B)$ holds

The multiplicative property of the determinant
$$
\begin{align}
\det(AB)=\det(A)\det(B)
\end{align}
$$
holds for any square matrices $A,B$ of the same dimension.

One way to understand this is through eigenvalues. If $A$ and $B$ are both diagonalizable and share a compatible eigenbasis, then
$$
\begin{align}
A=\mathrm{diag}(\lambda_1,\dots,\lambda_n), \quad
B=\mathrm{diag}(\mu_1,\dots,\mu_n),
\end{align}
$$
and hence
$$
\begin{align}
AB=\mathrm{diag}(\lambda_1\mu_1,\dots,\lambda_n\mu_n).
\end{align}
$$
Therefore,
$$
\begin{align}
\det(AB)=\prod_{i=1}^n \lambda_i\mu_i
= \left(\prod_{i=1}^n \lambda_i\right)\left(\prod_{i=1}^n \mu_i\right)
= \det(A)\det(B).
\end{align}
$$

More generally, even without simultaneous diagonalization, the determinant can be defined as the product of all eigenvalues (counting multiplicity), which ensures this multiplicative structure always holds.

### Introducing the pseudo-determinant $\det^+(A)$

The pseudo-determinant of a matrix $A$ is defined as the product of its nonzero eigenvalues:
$$
\begin{align}
\det^+(A)=\prod_{\lambda_i\neq 0} \lambda_i.
\end{align}
$$

Equivalently, if $A$ has rank $r$ and eigenvalues $\lambda_1,\dots,\lambda_r \neq 0$, then
$$
\begin{align}
\det^+(A)=\prod_{i=1}^r \lambda_i.
\end{align}
$$

This quantity is useful when $A$ is singular, where $\det(A)=0$ but the nonzero spectral structure still carries information.

### Why $\det^+(AB)=\det^+(A)\det^+(B)$ generally fails

In general, the multiplicative property does not hold:
$$
\begin{align}
\det^+(AB) \neq \det^+(A)\det^+(B).
\end{align}
$$

The key reason is that $\det^+$ only involves nonzero eigenvalues, while the product $AB$ may change the rank:
$$
\begin{align}
\mathrm{rank}(AB) \le \min\{\mathrm{rank}(A),\mathrm{rank}(B)\}.
\end{align}
$$

Thus, some nonzero eigenvalues of $A$ and $B$ may collapse into zero eigenvalues in $AB$, breaking the multiplicative structure.

### A concrete counterexample

Consider
$$
\begin{align}
A=
\begin{pmatrix}
1 & 0\\
0 & 0
\end{pmatrix}, \quad
B=
\begin{pmatrix}
0 & 0\\
0 & 1
\end{pmatrix}.
\end{align}
$$

Then
$$
\begin{align}
\det^+(A)=1, \quad \det^+(B)=1.
\end{align}
$$

However,
$$
\begin{align}
AB=
\begin{pmatrix}
0 & 0\\
0 & 0
\end{pmatrix},
\end{align}
$$
whose spectrum contains no nonzero eigenvalues. By convention (empty product),
$$
\begin{align}
\det^+(AB)=1.
\end{align}
$$

This example shows that the behavior of $\det^+$ is not governed by a simple multiplicative rule.

### When does a multiplicative property hold?

#### Case 1: Both $A$ and $B$ are invertible

If $A$ and $B$ are full rank, then there are no zero eigenvalues, and
$$
\begin{align}
\det^+(A)=\det(A), \quad \det^+(B)=\det(B).
\end{align}
$$

Hence,
$$
\begin{align}
\det^+(AB)=\det(AB)=\det(A)\det(B)=\det^+(A)\det^+(B).
\end{align}
$$

#### Case 2: Aligned support (same nonzero eigenspace)

Suppose $A$ and $B$ share the same eigenbasis and the same null space:
$$
\begin{align}
A=\mathrm{diag}(\lambda_1,\dots,\lambda_r,0), \quad
B=\mathrm{diag}(\mu_1,\dots,\mu_r,0).
\end{align}
$$

Then
$$
\begin{align}
AB=\mathrm{diag}(\lambda_1\mu_1,\dots,\lambda_r\mu_r,0),
\end{align}
$$
and thus
$$
\begin{align}
\det^+(AB)
= \prod_{i=1}^r \lambda_i\mu_i
= \det^+(A)\det^+(B).
\end{align}
$$

### A useful identity in applications

In many applications (e.g., covariance matrices in information theory), one often encounters expressions like
$$
\begin{align}
\log \det^+(A B^{-1}).
\end{align}
$$

If $A$ and $B$ share the same support (i.e., the same nonzero eigenspace), then one can write
$$
\begin{align}
\log \det^+(A B^{-1})
= \log \det^+(A) - \log \det^+(B).
\end{align}
$$

This identity is valid because the ratio is effectively taken over the common nonzero subspace.

### Summary

- The determinant satisfies
$$
\begin{align}
\det(AB)=\det(A)\det(B).
\end{align}
$$

- The pseudo-determinant generally does not:
$$
\begin{align}
\det^+(AB) \neq \det^+(A)\det^+(B).
\end{align}
$$

- The failure is due to rank reduction and the loss of nonzero eigenvalues.

- A multiplicative structure is recovered only under strong conditions such as invertibility or aligned support.
