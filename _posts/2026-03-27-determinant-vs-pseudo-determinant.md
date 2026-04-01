---
layout: post
title: "Determinant vs Pseudo-Determinant"
date: 2026-03-27
categories: [theory]
tags: [linear-algebra, determinant, pseudo-determinant, eigenvalues]
published: true
---

### Multiplicativity of the determinant

For any square matrices \(A,B \in \mathbb{C}^{n\times n}\), the determinant satisfies
$$
\begin{align}
\det(AB)=\det(A)\det(B).
\end{align}
$$

This property follows from the fundamental definition of the determinant as an alternating multilinear function of the columns. Specifically, for any fixed matrix \(A\), the mapping
$$
\begin{align}
B \mapsto \det(AB)
\end{align}
$$
is multilinear in the columns of \(B\), and inherits the alternating property. Therefore, it must be proportional to \(\det(B)\), i.e.,
$$
\begin{align}
\det(AB) = c(A)\det(B),
\end{align}
$$
for some scalar \(c(A)\). Evaluating at \(B=I\) yields \(c(A)=\det(A)\), which establishes the result.

---

### Definition of the pseudo-determinant

For a matrix \(A \in \mathbb{C}^{n\times n}\) with eigenvalues \(\{\lambda_i\}_{i=1}^n\), the pseudo-determinant is defined as
$$
\begin{align}
\det^+(A) = \prod_{\lambda_i \neq 0} \lambda_i.
\end{align}
$$

Equivalently, if \(\mathrm{rank}(A)=r\), then
$$
\begin{align}
\det^+(A)=\prod_{i=1}^{r}\lambda_i,
\end{align}
$$
where \(\{\lambda_i\}_{i=1}^r\) are the nonzero eigenvalues counted with multiplicity.

---

### Failure of multiplicativity: counterexamples

In general, the pseudo-determinant does not satisfy a multiplicative property. This can be seen from explicit counterexamples.

#### Counterexample 1 (both matrices rank-deficient)

Let
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

Both matrices have eigenvalues \(\{1,0\}\), hence
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
2 & 0\\
0 & 0
\end{pmatrix},
\end{align}
$$
so that
$$
\begin{align}
\det^+(AB)=2.
\end{align}
$$

Thus,
$$
\begin{align}
\det^+(AB) \neq \det^+(A)\det^+(B).
\end{align}
$$

---

#### Counterexample 2 (only one matrix rank-deficient)

Let
$$
\begin{align}
A=
\begin{pmatrix}
1 & 0\\
0 & 0
\end{pmatrix}, \quad
B=
\begin{pmatrix}
1 & 1\\
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

But
$$
\begin{align}
AB=
\begin{pmatrix}
1 & 1\\
0 & 0
\end{pmatrix},
\end{align}
$$
whose eigenvalues are again \(\{1,0\}\), hence
$$
\begin{align}
\det^+(AB)=1.
\end{align}
$$

Now consider instead
$$
\begin{align}
B'=
\begin{pmatrix}
2 & 0\\
0 & 1
\end{pmatrix},
\end{align}
$$
then
$$
\begin{align}
\det^+(B')=2, \quad
AB'=
\begin{pmatrix}
2 & 0\\
0 & 0
\end{pmatrix},
\end{align}
$$
so that
$$
\begin{align}
\det^+(AB')=2.
\end{align}
$$

This shows that even when one matrix is invertible, the multiplicative structure is not governed solely by individual pseudo-determinants, but depends on how the nonzero eigenspaces interact.

---

### Structural reason for the failure

The determinant depends on the full spectrum, while the pseudo-determinant depends only on the nonzero spectrum. Under matrix multiplication,
$$
\begin{align}
\mathrm{rank}(AB) \le \min\{\mathrm{rank}(A),\mathrm{rank}(B)\},
\end{align}
$$
and the nonzero eigenvalues of \(AB\) are not determined solely by those of \(A\) and \(B\). In particular, multiplication may:
- create new nonzero eigenvalues,
- or eliminate existing ones through rank deficiency.

Therefore, the multiplicative structure of eigenvalues is not preserved after removing zeros, which breaks the identity.

---

### Cases where multiplicativity holds

A multiplicative relation can be recovered under restrictive conditions.

1) **Invertible case**:  
If both \(A\) and \(B\) are invertible, then
$$
\begin{align}
\det^+(A)=\det(A), \quad \det^+(B)=\det(B),
\end{align}
$$
and hence
$$
\begin{align}
\det^+(AB)=\det^+(A)\det^+(B).
\end{align}
$$

2) **Aligned support (common invariant subspace)**:  
If \(A\) and \(B\) share the same nonzero eigenspace and are simultaneously diagonalizable on that subspace, then
$$
\begin{align}
A=\mathrm{diag}(\lambda_1,\dots,\lambda_r,0), \quad
B=\mathrm{diag}(\mu_1,\dots,\mu_r,0),
\end{align}
$$
which implies
$$
\begin{align}
\det^+(AB)=\prod_{i=1}^r \lambda_i \mu_i
= \det^+(A)\det^+(B).
\end{align}
$$

---

### Summary

- The determinant always satisfies
$$
\begin{align}
\det(AB)=\det(A)\det(B).
\end{align}
$$

- The pseudo-determinant does not admit such a general multiplicative property.

- The failure arises from the instability of the nonzero spectrum under matrix multiplication.

- Multiplicativity holds only under restrictive structural conditions such as invertibility or aligned support.
