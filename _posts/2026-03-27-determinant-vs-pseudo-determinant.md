---
layout: post
title: "Determinant vs Pseudo-Determinant"
date: 2026-03-27
categories: [theory]
tags: [linear-algebra, determinant, pseudo-determinant, eigenvalues]
published: true
---

### Multiplicativity of the determinant

Assume $A,B \in \mathbb{C}^{n\times n}$.

We first state several basic lemmas.

**Lemma 1.** For block matrices,
$$
\begin{align}
\left|\begin{array}{cc}
A & 0\\
C & B
\end{array}\right| = |A||B|.
\end{align}
$$

**Lemma 2.**
$$
\begin{align}
\left|\begin{array}{cc}
A & C\\
0 & B
\end{array}\right| = |A||B|.
\end{align}
$$

**Lemma 3.**
$$
\begin{align}
\left|\begin{pmatrix}
E & 0\\
X & E
\end{pmatrix}
\begin{pmatrix}
A & B\\
C & D
\end{pmatrix}\right|
=
\left|\begin{pmatrix}
A & B\\
C & D
\end{pmatrix}\right|.
\end{align}
$$
This follows from the invariance of the determinant under elementary row operations (adding a multiple of one row to another).

**Lemma 4.**
$$
\begin{align}
\left|\begin{pmatrix}
E & X\\
0 & E
\end{pmatrix}
\begin{pmatrix}
A & B\\
C & D
\end{pmatrix}\right|
=
\left|\begin{pmatrix}
A & B\\
C & D
\end{pmatrix}\right|.
\end{align}
$$

---

Now consider the matrix identity
$$
\begin{align}
\begin{pmatrix}
E & 0\\
- E & E
\end{pmatrix}
\begin{pmatrix}
E & E\\
0 & E
\end{pmatrix}
\begin{pmatrix}
E & -A\\
0 & E
\end{pmatrix}
\begin{pmatrix}
A & 0\\
E & B
\end{pmatrix}
=
\begin{pmatrix}
E & B - AB\\
0 & AB
\end{pmatrix}.
\end{align}
$$

Taking determinants on both sides yields
$$
\begin{align}
\left|
\begin{pmatrix}
E & 0\\
- E & E
\end{pmatrix}
\begin{pmatrix}
E & E\\
0 & E
\end{pmatrix}
\begin{pmatrix}
E & -A\\
0 & E
\end{pmatrix}
\begin{pmatrix}
A & 0\\
E & B
\end{pmatrix}
\right|
=
\left|
\begin{array}{cc}
E & B - AB\\
0 & AB
\end{array}
\right|.
\end{align}
$$

By Lemmas 3, 4, and 1, the left-hand side becomes
$$
\begin{align}
\left|
\begin{pmatrix}
A & 0\\
E & B
\end{pmatrix}
\right|
= |A||B|.
\end{align}
$$

By Lemma 2, the right-hand side satisfies
$$
\begin{align}
\left|
\begin{array}{cc}
E & B - AB\\
0 & AB
\end{array}
\right|
= |E||AB| = |AB|.
\end{align}
$$

Combining the above equalities yields
$$
\begin{align}
|A||B| = |AB|.
\end{align}
$$

---

For completeness, the above argument can be summarized compactly as
$$
\begin{align}
|A||B|
=&\left|\begin{pmatrix} A & 0 \\ E& B\end{pmatrix} \right| \\
=&\left|\begin{pmatrix} E & -A\\ 0& E\end{pmatrix} \begin{pmatrix} A & 0 \\ E& B\end{pmatrix}\right| \\
=&\left|\begin{pmatrix} E & E\\ 0& E\end{pmatrix} \begin{pmatrix} E & -A\\ 0& E\end{pmatrix} \begin{pmatrix} A & 0 \\ E& B\end{pmatrix}\right| \\
=&\left|\begin{pmatrix} E & 0\\ -E& E\end{pmatrix} \begin{pmatrix} E & E\\ 0& E\end{pmatrix} \begin{pmatrix} E & -A\\ 0& E\end{pmatrix} \begin{pmatrix} A & 0 \\ E& B\end{pmatrix}\right| \\
=&\left|\begin{pmatrix} E & B-AB\\ 0&AB\end{pmatrix}\right| \\
=&|E||AB| \\
=&|AB|.
\end{align}
$$

---

*This proof follows a standard block matrix factorization argument; see also:*  
https://zhuanlan.zhihu.com/p/297827171

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

Both matrices have eigenvalues $\{1,0\}$, hence
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
whose eigenvalues are again $\{1,0\}$, hence
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
and the nonzero eigenvalues of $AB$ are not determined solely by those of $A$ and $B$. In particular, multiplication may:
- create new nonzero eigenvalues,
- or eliminate existing ones through rank deficiency.

Therefore, the multiplicative structure of eigenvalues is not preserved after removing zeros, which breaks the identity.

---

### Cases where multiplicativity holds

A multiplicative relation can be recovered under restrictive conditions.

1) **Invertible case**:  
If both $A$ and $B$ are invertible, then
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
If $A$ and $B$ share the same nonzero eigenspace and are simultaneously diagonalizable on that subspace, then
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
