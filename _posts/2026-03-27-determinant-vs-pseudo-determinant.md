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
\begin{pmatrix} E & 0\\ -E & E \end{pmatrix}
\begin{pmatrix} E & E\\ 0 & E \end{pmatrix}
\begin{pmatrix} E & -A\\ 0 & E \end{pmatrix}
\begin{pmatrix} A & 0\\ E & B \end{pmatrix}
=
\begin{pmatrix} E & B-AB\\ 0 & AB \end{pmatrix}.
\end{align}
$$

This identity follows from direct block matrix multiplication.
Taking determinants on both sides yields
$$
\begin{align}
\det\!\left(
\begin{pmatrix} E & 0\\ -E & E \end{pmatrix}
\begin{pmatrix} E & E\\ 0 & E \end{pmatrix}
\begin{pmatrix} E & -A\\ 0 & E \end{pmatrix}
\begin{pmatrix} A & 0\\ E & B \end{pmatrix}
\right)
=
\det\!\begin{pmatrix} E & B-AB\\ 0 & AB \end{pmatrix}.
\end{align}
$$

On the left-hand side, each of the first three factors corresponds to a block elementary row operation. By Lemma 2, such operations do not change the determinant. Therefore,
$$
\begin{align}
\det\!\left(
\begin{pmatrix} E & 0\\ -E & E \end{pmatrix}
\begin{pmatrix} E & E\\ 0 & E \end{pmatrix}
\begin{pmatrix} E & -A\\ 0 & E \end{pmatrix}
\begin{pmatrix} A & 0\\ E & B \end{pmatrix}
\right)
=
\det\!\begin{pmatrix} A & 0\\ E & B \end{pmatrix}.
\end{align}
$$

Applying Lemma 1 gives
$$
\begin{align}
\det\!\begin{pmatrix} A & 0\\ E & B \end{pmatrix}
=
\det(A)\det(B).
\end{align}
$$

On the other hand, by Lemma 1 again (block upper triangular form),
$$
\begin{align}
\det\!\begin{pmatrix} E & B-AB\\ 0 & AB \end{pmatrix}
=
\det(AB),
\end{align}
$$
since $\det(E)=1$.

Combining the two expressions yields the desired identity
$$
\begin{align}
\det(A)\det(B)=\det(AB).
\end{align}
$$
$\blacksquare$

For clarity, the above argument can be summarized as follows:
$$
\begin{align}
\det(A)\det(B)
&= \det\!\begin{pmatrix} A & 0\\ E & B \end{pmatrix} \\
&= \det\!\left(
\begin{pmatrix} E & -A\\ 0 & E \end{pmatrix}
\begin{pmatrix} A & 0\\ E & B \end{pmatrix}
\right) \\
&= \det\!\left(
\begin{pmatrix} E & E\\ 0 & E \end{pmatrix}
\begin{pmatrix} E & -A\\ 0 & E \end{pmatrix}
\begin{pmatrix} A & 0\\ E & B \end{pmatrix}
\right) \\
&= \det\!\left(
\begin{pmatrix} E & 0\\ -E & E \end{pmatrix}
\begin{pmatrix} E & E\\ 0 & E \end{pmatrix}
\begin{pmatrix} E & -A\\ 0 & E \end{pmatrix}
\begin{pmatrix} A & 0\\ E & B \end{pmatrix}
\right) \\
&= \det\!\begin{pmatrix} E & B-AB\\ 0 & AB \end{pmatrix} \\
&= \det(AB).
\end{align}
$$

This section is based on:
- A block-matrix proof of $\det(AB)=\det(A)\det(B)$, [Zhihu note.](https://zhuanlan.zhihu.com/p/297827171)

### Pseudo-determinant and failure of multiplicativity

We first give the definition of the pseudo-determinant.

**Definition 1.**
<em>
Let $A \in \mathbb{C}^{n\times n}$ with eigenvalues $\\{\lambda_i\\}\_{i=1}^n$ (counted with multiplicity). The pseudo-determinant of $A$ is defined as
$$
\begin{align}
\det^+(A) = \prod_{\lambda_i \neq 0} \lambda_i.
\end{align}
$$
Equivalently, if $\mathrm{rank}(A)=r$, then
$$
\begin{align}
\det^+(A)=\prod_{i=1}^{r}\lambda_i,
\end{align}
$$
where $\\{\lambda_i\\}_{i=1}^r$ denote the nonzero eigenvalues of \(A\), arranged in nondecreasing order.
</em>

In general, a key point of this note is to emphasize that the pseudo-determinant does not satisfy a multiplicative property, i.e.,
$$
\begin{align}
\det^+(AB) \neq \det^+(A)\det^+(B).
\end{align}
$$
This can be seen from the following counterexamples.

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

Both matrices have eigenvalues $\\{1,0\\}$, hence
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
which has nonzero eigenvalue $\\{2\\}$, and thus
$$
\begin{align}
\det^+(AB)=2.
\end{align}
$$

#### Counterexample 2 (one matrix invertible)

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
2 & 0\\
0 & 1
\end{pmatrix}.
\end{align}
$$

Then
$$
\begin{align}
\det^+(A)=1, \quad \det^+(B)=2.
\end{align}
$$

Moreover,
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

### Structural reason for the failure

The ordinary determinant and the pseudo-determinant encode fundamentally different geometric objects.

For a square matrix $A \in \mathbb{C}^{n\times n}$, the determinant $\det(A)$ describes the signed volume scaling of the linear map induced by $A$ on the entire ambient space $\mathbb{C}^n$. Since matrix multiplication corresponds to composition of linear maps, and volume scaling is multiplicative under composition, one obtains the identity
$$
\begin{align}
\det(AB)=\det(A)\det(B).
\end{align}
$$

The pseudo-determinant $\det^+(A)$ is of a different nature. When $A$ is singular, it does not describe the action of $A$ on the whole space, since part of the space is annihilated. Instead, it only records the product of the nonzero eigenvalues, that is, the multiplicative effect of $A$ on the spectral component associated with its nonzero spectrum.

The essential difficulty is that this effective subspace is not fixed under multiplication. More precisely, the subspace on which $A$ acts nontrivially need not coincide with the corresponding subspace for $B$, nor with that for $AB$. Thus, although $\det^+(A)$ and $\det^+(B)$ each describe a partial spectral effect of the individual matrices, these two effects are generally associated with different subspaces, and therefore cannot be combined multiplicatively in any canonical way.

This can also be seen from the spectral viewpoint. The eigenvalues of a product $AB$ are not determined by the eigenvalues of $A$ and $B$ separately, unless strong additional assumptions are imposed, such as simultaneous diagonalizability on a common invariant subspace. In particular, after zero eigenvalues are removed, the remaining nonzero spectrum of $AB)$ is not obtained by simply multiplying the nonzero eigenvalues of $A$ and those of $B$ term by term. Hence, the operation of “discarding the zero spectrum” is not compatible with matrix multiplication.

Another way to phrase this is through rank and support. Although
$$
\begin{align}
\mathrm{rank}(AB)\le \min\{\mathrm{rank}(A),\mathrm{rank}(B)\},
\end{align}
$$
the failure of multiplicativity is not merely a consequence of rank reduction itself. The deeper reason is that the support of the product $AB$ is determined by the interaction between the range of $B$ and the null space of $A$. Part of the nontrivial action of $B$ may be mapped into directions that are subsequently annihilated by $A$, while new nonzero eigenvalues of $AB$ may emerge from the way these two operators are composed on the surviving subspace. Therefore, the nonzero spectral data of $AB$ depends on the relative position of the invariant, range, and null spaces of $A$ and $B$, rather than only on the separate nonzero spectra of the two matrices.

For this reason, unlike the ordinary determinant, the pseudo-determinant does not define a multiplicative functional on the full matrix algebra. Its value is not governed solely by the individual nonzero eigenvalues of the factors, but by how their effective spectral subspaces align under composition.

### Cases where multiplicativity holds

Although the pseudo-determinant is not multiplicative in general, a multiplicative relation can be recovered under restrictive structural conditions.

#### Invertible case

If both $A$ and $B$ are invertible, then there are no zero eigenvalues, and the pseudo-determinant reduces to the ordinary determinant:
$$
\begin{align}
\det^+(A)=\det(A), \quad \det^+(B)=\det(B).
\end{align}
$$
Therefore, multiplicativity follows immediately from that of the determinant:
$$
\begin{align}
\det^+(AB)=\det(AB)=\det(A)\det(B)=\det^+(A)\det^+(B).
\end{align}
$$
In this case, no information is discarded, and the pseudo-determinant coincides with a fully multiplicative functional.

#### Aligned support (common invariant subspace)

A nontrivial multiplicative structure can still be recovered when the effective spectral subspaces of $A$ and $B$ are aligned.

Specifically, suppose that there exists a decomposition of the ambient space
$$
\mathbb{C}^n = \mathcal{U} \oplus \mathcal{U}^\perp,
$$
such that:

- both $A$ and $B$ leave $\mathcal{U}$ invariant,
- both $A$ and $B$ vanish on $\mathcal{U}^\perp$,
- and the restrictions of $A$ and $B$ to $\mathcal{U}$ are simultaneously diagonalizable.

Then, with respect to a suitable basis, $A$ and $B$ admit the block forms
$$
\begin{align}
A=\mathrm{diag}(\lambda_1,\dots,\lambda_r,0), \quad
B=\mathrm{diag}(\mu_1,\dots,\mu_r,0),
\end{align}
$$
where the nonzero parts act on the same $r$-dimensional subspace $\mathcal{U}$.

In this setting, the product satisfies
$$
\begin{align}
AB=\mathrm{diag}(\lambda_1\mu_1,\dots,\lambda_r\mu_r,0),
\end{align}
$$
and hence
$$
\begin{align}
\det^+(AB)
= \prod_{i=1}^r \lambda_i \mu_i
= \left(\prod_{i=1}^r \lambda_i\right)\left(\prod_{i=1}^r \mu_i\right)
= \det^+(A)\det^+(B).
\end{align}
$$

The key feature here is that the nonzero spectral components of $A$ and $B$ are supported on the same invariant subspace. As a result, the composition $AB$ acts on a fixed subspace where both operators are simultaneously diagonalizable, and the usual multiplicative structure of eigenvalues is preserved after restricting to this subspace.

In contrast, when the supports are not aligned, the action of $B$ may partially lie in directions that are annihilated by $A$, or may be rotated into different subspaces, thereby destroying any canonical pairing between the nonzero eigenvalues of $A$, $B$, and $AB$.

### Summary

The determinant and the pseudo-determinant exhibit fundamentally different algebraic behaviors.

The determinant $\det(\cdot)$ defines a multiplicative functional on the full matrix algebra, reflecting the multiplicative nature of volume scaling under composition of linear maps. This multiplicativity holds without any structural assumptions.

In contrast, the pseudo-determinant $\det^+(\cdot)$ captures only the nonzero spectral component of a matrix and therefore depends on an implicit choice of effective subspace. Since this subspace is not preserved under matrix multiplication in general, the pseudo-determinant fails to be multiplicative.

A multiplicative relation can be recovered only when no information is lost (invertible case) or when the effective subspaces of the matrices are aligned and invariant under both operators. Outside of such restrictive settings, the pseudo-determinant is inherently non-multiplicative, and its value for a product $AB$ depends on the relative geometric configuration of the spectral subspaces of $A$ and $B$, rather than solely on their individual nonzero eigenvalues.
