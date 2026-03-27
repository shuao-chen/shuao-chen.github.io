layout: post
title: "Determinant vs Pseudo-Determinant"
date: 2026-03-27
categories: [theory]
tags: [linear-algebra, determinant, pseudo-determinant, eigenvalues]
published: true

### Why $\det(AB)=\det(A)\det(B)$ holds

The multiplicative property of the determinant
$$
\begin{align}
\det(AB)=\det(A)\det(B)
\end{align}
$$
holds for any square matrices $A,B$.

One way to understand this is through eigenvalues. If $A$ and $B$ are diagonalizable and share a compatible eigenbasis, then
$$
\begin{align}
A=\mathrm{diag}(\lambda_1,\dots,\lambda_n), \quad
B=\mathrm{diag}(\mu_1,\dots,\mu_n),
\end{align}
$$
which implies
$$
\begin{align}
AB=\mathrm{diag}(\lambda_1\mu_1,\dots,\lambda_n\mu_n).
\end{align}
$$

Therefore,
$$
\begin{align}
\det(AB)
= \prod_{i=1}^n \lambda_i\mu_i
= \left(\prod_{i=1}^n \lambda_i\right)\left(\prod_{i=1}^n \mu_i\right)
= \det(A)\det(B).
\end{align}
$$

More generally, since the determinant equals the product of all eigenvalues (counting multiplicity), this multiplicative structure always holds.

### Introducing the pseudo-determinant $\det^+(A)$

The pseudo-determinant of a matrix $A$ is defined as the product of its nonzero eigenvalues:
$$
\begin{align}
\det^+(A)=\prod_{\lambda_i\neq 0} \lambda_i.
\end{align}
$$

If $A$ has rank $r$ and nonzero eigenvalues $\lambda_1,\dots,\lambda_r$, then
$$
\begin{align}
\det^+(A)=\prod_{i=1}^r \lambda_i.
\end{align}
$$

This definition is meaningful for singular matrices, where $\det(A)=0$ but the nonzero spectrum still contains useful information.

### Why $\det^+(AB)=\det^+(A)\det^+(B)$ generally fails

In general,
$$
\begin{align}
\det^+(AB) \neq \det^+(A)\det^+(B).
\end{align}
$$

The reason is that $\det^+$ only involves nonzero eigenvalues, while matrix multiplication may reduce rank:
$$
\begin{align}
\mathrm{rank}(AB) \le \min\{\mathrm{rank}(A),\mathrm{rank}(B)\}.
\end{align}
$$

Thus, the set of nonzero eigenvalues is not preserved under multiplication, and the multiplicative structure breaks.

### A correct counterexample

Consider
$$
\begin{align}
A=
\begin{pmatrix}
1 & 1\\
0 & 0
\end{pmatrix}, \quad
B=
\begin{pmatrix}
1 & 0\\
1 & 0
\end{pmatrix}.
\end{align}
$$

For $A$, the characteristic polynomial is
$$
\begin{align}
\det(\lambda I-A)
=
\lambda(\lambda-1),
\end{align}
$$
so the eigenvalues are $1$ and $0$, and
$$
\begin{align}
\det^+(A)=1.
\end{align}
$$

Similarly for $B$,
$$
\begin{align}
\det(\lambda I-B)
=
\lambda(\lambda-1),
\end{align}
$$
so
$$
\begin{align}
\det^+(B)=1.
\end{align}
$$

However,
$$
\begin{align}
AB
=
\begin{pmatrix}
2 & 0\\
0 & 0
\end{pmatrix},
\end{align}
$$
which has nonzero eigenvalue $2$, hence
$$
\begin{align}
\det^+(AB)=2.
\end{align}
$$

Therefore,
$$
\begin{align}
\det^+(AB)=2 \neq 1=\det^+(A)\det^+(B).
\end{align}
$$

### When does a multiplicative property hold?

If $A$ and $B$ are invertible, then there are no zero eigenvalues, and
$$
\begin{align}
\det^+(A)=\det(A), \quad \det^+(B)=\det(B).
\end{align}
$$

Thus,
$$
\begin{align}
\det^+(AB)=\det(AB)=\det(A)\det(B)=\det^+(A)\det^+(B).
\end{align}
$$

Another case is when $A$ and $B$ share the same eigenbasis and null space:
$$
\begin{align}
A=\mathrm{diag}(\lambda_1,\dots,\lambda_r,0), \quad
B=\mathrm{diag}(\mu_1,\dots,\mu_r,0),
\end{align}
$$
which implies
$$
\begin{align}
AB=\mathrm{diag}(\lambda_1\mu_1,\dots,\lambda_r\mu_r,0).
\end{align}
$$

Then,
$$
\begin{align}
\det^+(AB)=\prod_{i=1}^r \lambda_i\mu_i
= \det^+(A)\det^+(B).
\end{align}
$$

### A useful identity in applications

In many applications, one encounters
$$
\begin{align}
\log \det^+(A B^{-1}).
\end{align}
$$

If $A$ and $B$ share the same support (nonzero eigenspace), then
$$
\begin{align}
\log \det^+(A B^{-1})
= \log \det^+(A) - \log \det^+(B).
\end{align}
$$

### Summary

- The determinant always satisfies
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

- The failure is due to rank reduction and loss of nonzero eigenvalues.

- Multiplicativity is recovered only under strong conditions such as invertibility or aligned support.
