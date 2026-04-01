---
layout: post
title: "Determinant vs Pseudo-Determinant"
date: 2026-03-27
categories: [theory]
tags: [linear-algebra, determinant, pseudo-determinant, eigenvalues]
published: true
---

### Multiplicativity of the determinant

Assume that $A,B \in \mathbb{C}^{n\times n}$. Let $E$ denote the $n\times n$ identity matrix.

The goal is to prove that
$$
\begin{align}
\det(AB)=\det(A)\det(B).
\end{align}
$$

To this end, several elementary identities for block matrices are first recalled.

**Lemma 1.**
<em>
For any $n\times n$ matrices $A,B,C$, the following identities hold:
$$
\begin{align}
\det\!\begin{pmatrix}
A & 0\\
C & B
\end{pmatrix}
&=
\det\!\begin{pmatrix}
A & C\\
0 & B
\end{pmatrix}
\\
&= \det(A)\det(B).
\end{align}
$$
</em>
These correspond to the determinant formulas for block lower and upper triangular matrices. In both cases, the determinant equals the product of the determinants of the diagonal blocks. This follows directly from the multilinearity of the determinant with respect to rows (or columns), since the zero block eliminates any cross-term contributions in the expansion.

**Lemma 2.**
<em>
For any $n\times n$ matrices $A,B,C,D,X$, the following identities hold:
$$
\begin{align}
\det\!\left(
\begin{pmatrix}
E & 0\\
X & E
\end{pmatrix}
\begin{pmatrix}
A & B\\
C & D
\end{pmatrix}
\right)
&=
\det\!\left(
\begin{pmatrix}
E & X\\
0 & E
\end{pmatrix}
\begin{pmatrix}
A & B\\
C & D
\end{pmatrix}
\right)
\\ 
&=
\det\!\begin{pmatrix}
A & B\\
C & D
\end{pmatrix}.
\end{align}
$$
Indeed,
$$
\begin{align}
\begin{pmatrix}
E & 0\\
X & E
\end{pmatrix}
\begin{pmatrix}
A & B\\
C & D
\end{pmatrix}
&=
\begin{pmatrix}
E & X\\
0 & E
\end{pmatrix}
\begin{pmatrix}
A & B\\
C & D
\end{pmatrix}
\\ 
&=
\begin{pmatrix}
A+XC & B+XD\\
C & D
\end{pmatrix}.
\end{align}
$$
</em>

Hence, left multiplication by $\begin{pmatrix} E & 0\\\\ X & E \end{pmatrix}$ amounts to adding $X$ times the first block row to the second block row, while left multiplication by $\begin{pmatrix} E & X\\\\ 0 & E \end{pmatrix}$ adds $X$ times the second block row to the first block row. Both operations are block versions of elementary row operations and therefore leave the determinant unchanged.

With these preparations, consider the identity
$$
\begin{align}
\begin{pmatrix}
E & 0\\ - E & E
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
E & B-AB\\
0 & AB
\end{pmatrix}.
\end{align}
$$

This identity is obtained by direct block multiplication. Taking determinants on both sides gives
$$
\begin{align}
\det\!\left(
\begin{pmatrix}
E & 0\\\\  
- E & E
\end{pmatrix}
\begin{pmatrix}
E & E\\\\  
0 & E
\end{pmatrix}
\begin{pmatrix}
E & -A\\\\ 
0 & E
\end{pmatrix}
\begin{pmatrix}
A & 0\\\\  
E & B
\end{pmatrix}
\right)
=
\det\!\begin{pmatrix}
E & B-AB\\\\  
0 & AB
\end{pmatrix}.
\end{align}
$$

Now the determinant of the left-hand side is simplified step by step.

First, by Lemma 3 and Lemma 4, multiplying on the left by
$\begin{pmatrix} E & 0\\\\ -E & E \end{pmatrix}$,
$\begin{pmatrix} E & E\\\\ 0 & E \end{pmatrix}$,
and
$\begin{pmatrix} E & -A\\\\ 0 & E \end{pmatrix}$
does not change the determinant. Therefore,
$$
\begin{align}
\det\!\left(
\begin{pmatrix}
E & 0\\\\  
- E & E
\end{pmatrix}
\begin{pmatrix}
E & E\\\\  
0 & E
\end{pmatrix}
\begin{pmatrix}
E & -A\\\\  
0 & E
\end{pmatrix}
\begin{pmatrix}
A & 0\\\\  
E & B
\end{pmatrix}
\right)
=
\det\!\begin{pmatrix}
A & 0\\\\  
E & B
\end{pmatrix}.
\end{align}
$$

Next, Lemma 1 yields
$$
\begin{align}
\det\!\begin{pmatrix}
A & 0\\  
E & B
\end{pmatrix}
=
\det(A)\det(B).
\end{align}
$$

On the other hand, by Lemma 2,
$$
\begin{align}
\det\!\begin{pmatrix}
E & B-AB\\  
0 & AB
\end{pmatrix}
=
\det(E)\det(AB)
=
\det(AB),
\end{align}
$$
since $\det(E)=1$.

Combining the two sides gives
$$
\begin{align}
\det(A)\det(B)=\det(AB).
\end{align}
$$

Equivalently,
$$
\begin{align}
\det(AB)=\det(A)\det(B).
\end{align}
$$

---

For convenience, the entire argument may also be summarized in the following chain:
$$
\begin{align}
\det(A)\det(B)
=&\det\!\begin{pmatrix} A & 0 \\ E & B\end{pmatrix} \\
=&\det\!\left(\begin{pmatrix} E & -A\\ 0& E\end{pmatrix} \begin{pmatrix} A & 0 \\ E& B\end{pmatrix}\right) \\
=&\det\!\left(\begin{pmatrix} E & E\\ 0& E\end{pmatrix} \begin{pmatrix} E & -A\\ 0& E\end{pmatrix} \begin{pmatrix} A & 0 \\ E& B\end{pmatrix}\right) \\
=&\det\!\left(\begin{pmatrix} E & 0\\ -E& E\end{pmatrix} \begin{pmatrix} E & E\\ 0& E\end{pmatrix} \begin{pmatrix} E & -A\\ 0& E\end{pmatrix} \begin{pmatrix} A & 0 \\ E& B\end{pmatrix}\right) \\
=&\det\!\begin{pmatrix} E & B-AB\\ 0&AB\end{pmatrix} \\
=&\det(E)\det(AB) \\
=&\det(AB).
\end{align}
$$

This note is based on:
- A block-matrix proof of $\det(AB)=\det(A)\det(B)$, Zhihu note. [Link](https://zhuanlan.zhihu.com/p/297827171)

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
