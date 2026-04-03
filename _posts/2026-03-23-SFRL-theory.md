---
layout: post
title: "Strong Functional Representation Lemma Notes"
date: 2026-03-23
categories: [theory]
tags: [information-theory, SFRL, functional-representation]
published: true
---

### Strong Functional Representation Lemma

In information theory, a fundamental problem is how to characterize the correlation structure between $(X,Y)$ using a random variable $Z$ that is independent of the input $X$.
In other words, whether $Y$ can be represented as a deterministic function of $X$ and some independent randomness, while controlling the information redundancy introduced by this randomness.
The Strong Functional Representation Lemma (SFRL) provides a quantitative answer to this problem: it not only guarantees the existence of such a representation, but also further characterizes the information complexity of the required random variable $Z$.

**Theorem 1 (Strong Functional Representation Lemma, SFRL).**
<em>
For any pair of random variables $(X,Y)\sim P_{XY}$, there exists a random variable $Z$ such that
$$\begin{align}
Z \perp X,\qquad Y = g(X,Z)
\end{align}$$
for some deterministic function $g$, and satisfying
$$\begin{align}
I(X;Z|Y) \le \log\big(I(X;Y)+1\big) + 4.
\end{align}$$
If $X,Y$ are discrete random variables with cardinalities $|\mathcal X|,|\mathcal Y|$, then one can further restrict
$$\begin{align}
|\mathcal Z| \le |\mathcal X|(|\mathcal Y|-1)+2.
\end{align}$$
Moreover, it follows that
$$
\begin{align}
H(Y|Z) \le I(X;Y) + \log\big(I(X;Y)+1\big) + 4.
\end{align}
$$
</em>

The above entropy bound is a consequence of the chain rule of mutual information. Indeed,
$$
\begin{align}
I(X;Y,Z) = I(X;Y) + I(X;Z|Y),
\end{align}
$$
while
$$
\begin{align}
I(X;Y,Z)
&= I(X;Z) + I(X;Y|Z) \\
&= I(X;Y|Z) \\
&= H(Y|Z),
\end{align}
$$
where the second step uses $Z \perp X$, and the third step uses $Y=g(X,Z)$. Combining these identities with the bound on $I(X;Z|Y)$ yields the stated inequality. This result shows that there exists a random variable $Z$ independent of $X$ such that the gap between $H(Y|Z)$ and $I(X;Y)$ is at most logarithmic in $I(X;Y)$.

### Poisson Functional Representation

Next, we present the key construction that realizes the lemma, namely the so-called Poisson functional representation. Consider a marked Poisson point process defined on $\mathcal Y\times \mathbb R_+$:
$$\begin{align}
Z = \{(\tilde Y_i, T_i)\}_{i\ge 1},
\end{align}$$
where the marks $\tilde Y_i$ and the time coordinates $T_i$ are independent, and satisfy
$$\begin{align}
\tilde Y_i \overset{\text{i.i.d.}}{\sim} P_Y,
\qquad
T_i - T_{i-1} \overset{\text{i.i.d.}}{\sim} \text{Exp}(1), \quad T_0=0.
\end{align}$$

Thus, $\\{T_i\\}$ forms a Poisson process with rate $1$, where the “rate” represents the average number of events per unit time, and each arrival point is independently assigned a mark distributed according to $P_Y$.

Given $x\in\mathcal X$ and the entire point set $Z$, define the index
$$\begin{align}
k_{X\to Y}(x,Z)
=
\arg\min_i \;
T_i \cdot
\frac{dP_Y}{dP_{Y|X}(\cdot|x)}(\tilde Y_i).
\end{align}$$

This selection rule assigns a weight to each point $(\tilde Y_i,T_i)$, where the weight is given by the likelihood ratio $\frac{dP_Y}{dP_{Y \mid X}}(\tilde Y_i \mid x)$, thereby introducing a non-uniform scaling in the time coordinate depending on the realization $x$.

Based on this index, define the mapping
$$\begin{align}
g_{X\to Y}(x,Z)
=
\tilde Y_{\,k_{X\to Y}(x,Z)},
\end{align}$$
and finally construct the output random variable
$$\begin{align}
Y = g_{X\to Y}(X,Z).
\end{align}$$

In summary, $Y$ is obtained by selecting the mark $\tilde Y_i$ corresponding to the point that minimizes the scaled time $T_i \cdot \frac{dP_Y}{dP_{Y\|X}}(\tilde Y_i \mid X)$, i.e., the first arrival after a likelihood-ratio-based rescaling of the time axis.

### Continuous Case: Intuition via Uniform Distribution

We now provide an example to give an intuitive understanding. Suppose
$$\begin{align}
Y \sim \mathrm{Unif}[0,1],
\qquad
Y\,|\,\{X=x\} \sim f_{Y|X}(y|x).
\end{align}$$

In this case, the marked point process in the Poisson functional representation is $Z=\\{(\tilde Y_i,T_i)\\}\_{i=1,2,\dots},$ where $\tilde Y_i \overset{\text{i.i.d.}}{\sim} \mathrm{Unif}[0,1]$, and $\\{T_i\\}$ are the arrival times of a Poisson process with rate $1$, i.e., $T_i-T_{i-1}\overset{\text{i.i.d.}}{\sim} \text{Exp}(1)$ with $T_0=0$.

Since the unconditional distribution is $Y \sim \mathrm{Unif}[0,1]$, we have $p_Y(y)=1$ for $y\in[0,1]$. For a given $x$, the general construction simplifies to
$$\begin{align}
K
=
\arg\min_i \frac{T_i}{f_{Y|X}(\tilde Y_i|x)},
\end{align}$$
and output
$$\begin{align}
Y=\tilde Y_K.
\end{align}$$

From a geometric perspective, the point set $\\{(\tilde y_i,t_i)\\}$ can be viewed as a collection of random points on $[0,1] \times \mathbb{R}\_+$, where the horizontal coordinate $\tilde y_i$ is uniformly distributed over $[0,1]$, and the vertical coordinate $t_i$ represents increasing random times. For each point $(\tilde y_i,t_i)$, we compare its vertical coordinate $t_i$ with the value of $f_{Y \mid X}(y \mid x)$ at the corresponding position, thereby forming a normalized ratio and selecting the point with the smallest value.
Equivalently, from a dynamic perspective, one can imagine gradually scaling up the graph of $f_{Y \mid X}(y \mid x)$; when it first touches a random point, the horizontal coordinate of that point is taken as the output.

Next, we show that this construction indeed generates the desired conditional distribution. Fix any $x$, and consider the above marked Poisson point process. Apply the transformation
$$\begin{align}
(\tilde Y_i, T_i) \mapsto \left(\tilde Y_i,\; \frac{T_i}{f_{Y|X}(\tilde Y_i|x)}\right).
\end{align}$$

By the mapping property of Poisson point processes, the transformed process is still a Poisson point process, whose intensity measure on $[0,1]\times\mathbb{R}_+$ is
$$\begin{align}
f_{Y|X}(y|x)\,dy \times dt.
\end{align}$$

**Remark 1.**
Here we briefly explain the ingredients used above. The mapping property of Poisson point processes states that if a Poisson point process is transformed via a measurable mapping, then the resulting point process is still Poisson, with its intensity measure given by the pushforward of the original intensity measure under this mapping.

In the present setting, the original marked Poisson point process $\{(\tilde Y_i, T_i)\}$ has intensity measure $dy \times dt$, since $\tilde Y_i \sim \mathrm{Unif}[0,1]$ and the arrival times form a unit-rate Poisson process.
Under the transformation $(\tilde Y_i, T_i) \mapsto \left(\tilde Y_i,\; \frac{T_i}{f_{Y|X}(\tilde Y_i|x)}\right)$, the time coordinate is rescaled by a factor depending on $\tilde Y_i$. As a result, the intensity measure is correspondingly scaled, yielding $f_{Y|X}(y|x)\,dy \times dt$.
$\blacklozenge$

The original selection rule is equivalent to choosing the point with the smallest vertical coordinate in this transformed process, and outputting its horizontal coordinate.

For later analysis, we first state a basic result.

**Lemma 1.**
<em>
Let $\Pi$ be a Poisson process on $\mathbb R_+$ with rate $\lambda$, and let $N(A)$ denote the number of points of $\Pi$ falling in a measurable set $A \subset \mathbb R_+$. In particular, $N([0,t])$ is the number of arrivals up to time $t$. Denote the first arrival time by
$$\begin{align}
\tau := \inf\{t\ge 0 : N([0,t])\ge 1\}.
\end{align}$$
Then
$$\begin{align}
\tau \sim \text{Exp}(\lambda).
\end{align}$$
</em>

**Proof.**
For any $t\ge 0$, the event $\\{\tau>t\\}$ is equivalent to having no arrivals in the interval $[0,t]$, i.e.,
$$\begin{align}
\{\tau>t\}=\{N([0,t])=0\}.
\end{align}$$
Since $\Pi$ is a Poisson process with rate $\lambda$, we have
$$\begin{align}
N([0,t])\sim \mathrm{Poisson}(\lambda t).
\end{align}$$
Thus,
$$\begin{align}
\mathbb P(\tau>t)
=\mathbb P\big(N([0,t])=0\big)
= e^{-\lambda t},
\end{align}$$
where the last equality follows from the Poisson probability mass function $\mathbb P\big(N([0,t])=k\big) = \frac{(\lambda t)^k}{k!} e^{-\lambda t}$ by taking $k=0$.
This is exactly the tail distribution of an exponential distribution with parameter $\lambda$, hence $\tau \sim \text{Exp}(\lambda).$
$\blacksquare$

Now apply this result to the current setting, namely the transformed marked Poisson point process with intensity measure $f_{Y|X}(y|x)\,dy \times dt$.
For any measurable set $A\subseteq [0,1]$, let $N_A(t)$ denote the number of points in the region $A\times[0,t]$. Then
$$
\begin{align}
N_A(t)\sim \mathrm{Poisson}\left(t\int_A f_{Y|X}(y|x)\,dy\right),
\end{align}
$$
since for a Poisson point process, the number of points in any measurable region follows a Poisson distribution with parameter equal to the intensity measure of that region.

Define the first arrival time into the set $A$ as $\tau_A := \inf\\{t\ge 0 : N_A(t)\ge 1\\}$, so that
$$\begin{align}
\tau_A \sim \text{Exp}\left(\int_A f_{Y|X}(y|x)\,dy\right).
\end{align}$$

Similarly,
$$\begin{align}
\tau_{A^c} \sim \text{Exp}\left(\int_{A^c} f_{Y|X}(y|x)\,dy\right),
\end{align}$$
and the two are independent.
Note that the event $\\{Y \in A\\}$ is equivalent to the event that the earliest point in the transformed process falls in $A$, i.e.,
$$\begin{align}
\{Y\in A\} = \{\tau_A < \tau_{A^c}\}.
\end{align}$$

Next, we use a basic result on independent exponential random variables.

**Lemma 2.**
<em>
Let $T_1,\dots,T_n$ be independent exponential random variables with
$$\begin{align}
T_i \sim \text{Exp}(\lambda_i),\qquad \lambda_i>0,\; i=1,\dots,n.
\end{align}$$
Then
$$\begin{align}
\mathbb P\big(T_i = \min_{1\le j\le n} T_j\big)
=
\frac{\lambda_i}{\sum_{j=1}^n \lambda_j}.
\end{align}$$
</em>

**Proof.**
For any fixed $i$, we have
$$\begin{align}
\mathbb P\big(T_i = \min_{1\le j\le n} T_j\big)
=
\mathbb P\big(T_i < T_j,\ \forall j\ne i\big).
\end{align}$$
By independence,
$$\begin{align}
\mathbb P\big(T_i < T_j,\ \forall j\ne i\big)
&=
\int_0^\infty
\mathbb P\big(T_j > t,\ \forall j\ne i\big)\, f_{T_i}(t)\,dt \\
&=
\int_0^\infty
\prod_{j\ne i} e^{-\lambda_j t}\;
\lambda_i e^{-\lambda_i t}\,dt \\
&=
\lambda_i \int_0^\infty
e^{-\left(\sum_{j=1}^n \lambda_j\right)t}\,dt \\
&=
\frac{\lambda_i}{\sum_{j=1}^n \lambda_j}.
\end{align}$$
$\blacksquare$

Applying this to $\tau_A$ and $\tau_{A^c}$, we obtain
$$\begin{align}
\mathbb{P}(Y \in A \mid X=x)
&=
\mathbb P(\tau_A<\tau_{A^c}) \\
&=
\frac{\int_A f_{Y|X}(y|x)\,dy}{\int_A f_{Y|X}(y|x)\,dy + \int_{A^c} f_{Y|X}(y|x)\,dy} \\
&=
\int_A f_{Y|X}(y|x)\,dy,
\end{align}$$
where the last step uses the normalization condition $\int_{[0,1]} f_{Y|X}(y|x)\,dy = 1.$
Therefore,
$$\begin{align}
Y \mid \{X=x\} \sim f_{Y|X}(y|x).
\end{align}$$

In summary, this construction rescales the time coordinate depending on $x$, transforming the distribution of the mark of the earliest arrival point from the uniform distribution to the target conditional distribution. Since the point set $\\{(\tilde Y_i, T_i)\\}$ is randomly generated (with both $\tilde Y_i$ and $T_i$ being random variables), by repeatedly generating the process independently and applying the above selection rule, one obtains independent samples following $f_{Y \mid X}(\cdot \mid x)$.

### Discrete Case: Exponential Race Representation

When $\mathcal{Y}$ is a finite set, the above Poisson construction can be equivalently represented as an exponential race form. Let $\\{Z_y\\}_{y\in\mathcal{Y}}$ be a collection of independent exponential random variables, $Z_y \sim \text{Exp}(1), \; y\in\mathcal{Y}.$
Given $x$, define the selection rule
$$\begin{align}
Y
=
\arg\min_{y\in\mathcal{Y}} \frac{Z_y}{p_{Y|X}(y|x)}.
\end{align}$$

This construction can be interpreted as a “competition” among all candidate values $y$: each $y$ is associated with a random time $Z_y$, which is scaled according to the weight $p_{Y \mid X}(y \mid x)$, and the one with the smallest scaled value is selected.

Next, we explain the relationship between this discrete exponential construction and the original Poisson construction. Consider the marked Poisson point process $\\{(\tilde Y_i, T_i)\\}_{i\ge 1},$ where $\tilde Y_i \sim p_Y$, and $\\{T_i\\}$ are the arrival times of a Poisson process with rate $1$. The original selection rule is
$$\begin{align}
K
=
\arg\min_i \;
T_i \cdot \frac{p_Y(\tilde Y_i)}{p_{Y|X}(\tilde Y_i|x)},
\qquad
Y = \tilde Y_K.
\end{align}$$

Group the index set according to the values of $\tilde Y_i$. For each $y\in\mathcal{Y}$, define $\mathcal{I}_y := \\{\, i : \tilde Y_i = y \,\\}.$ Then the above minimization can be equivalently written as
$$\begin{align}
Y
=
\arg\min_{y\in\mathcal{Y}}
\left[
\frac{p_Y(y)}{p_{Y|X}(y|x)}
\cdot
\min_{i\in \mathcal{I}_y} T_i
\right].
\end{align}$$

For each fixed $y$, the subprocess $\\{T_i:\tilde Y_i=y\\}$ is still a Poisson process by the thinning property, with rate $p_Y(y)$. Hence, its first arrival time satisfies
$$\begin{align}
\min_{i:\tilde Y_i=y} T_i \sim \text{Exp}\big(p_Y(y)\big),
\end{align}$$
and these are independent across different $y$.

Define
$$\begin{align}
Z_y := p_Y(y)\cdot \min_{i:\tilde Y_i=y} T_i,
\end{align}$$
then by the scaling property of exponential distributions,
$$\begin{align}
Z_y \sim \text{Exp}(1),
\end{align}$$
and $\\{Z_y\\}_{y\in\mathcal{Y}}$ are independent. Substituting back, we obtain
$$\begin{align}
Y
=
\arg\min_{y\in\mathcal{Y}}
\frac{Z_y}{p_{Y|X}(y|x)},
\end{align}$$
which is exactly the exponential race form above.

Therefore, the original minimization over indices $i$ can be equivalently reduced to a minimization over the alphabet $\mathcal{Y}$. That is, instead of comparing all points $(\tilde Y_i,T_i)$, one only needs to keep the earliest arrival time for each class $y$, leading to the exponential race representation.

Next, we show that this construction indeed generates the target conditional distribution. Since $\frac{Z_y}{p_{Y|X}(y|x)} \sim \text{Exp}\big(p_{Y|X}(y|x)\big),$ and the variables corresponding to different $y$ are independent, by the minimum property of exponential distributions, we have
$$\begin{align}
\mathbb P\left(Y=y \mid X=x\right)
=
\frac{p_{Y|X}(y|x)}{\sum_{y'} p_{Y|X}(y'|x)}
=
p_{Y|X}(y|x),
\end{align}$$
where the normalization condition $\sum_{y'} p_{Y|X}(y'|x)=1$ is used.
Therefore,
$$\begin{align}
Y \mid \{X=x\} \sim p_{Y|X}(\cdot|x).
\end{align}$$

Moreover, the selection rule is invariant to common scaling of $\\{Z_y\\}$, i.e., for any constant $c>0$, $\arg\min_{y} \frac{Z_y}{p_{Y|X}(y|x)} = \arg\min_{y} \frac{cZ_y}{p_{Y|X}(y|x)}.$
Hence, one can normalize $\\{Z_y\\}$ such that $\sum_{y\in\mathcal{Y}} Z_y = 1,$ in which case the random vector $\\{Z_y\\}_{y\in\mathcal{Y}}$ is uniformly distributed over the probability simplex, i.e., follows a Dirichlet$(1,\dots,1)$ distribution. This normalization does not affect the selection result.

### Derivation of the Mutual Information Upper Bound

Next, we prove the mutual information upper bound corresponding to this construction. Since $Y=\tilde Y_K$ is uniquely determined by $Z$ and the index $K$, $Y$ has no additional uncertainty given $Z$ and $K$, i.e.,
$$\begin{align}
H(Y|Z,K)=0.
\end{align}$$

By the chain rule,
$$\begin{align}
H(Y|Z)
&\le H(Y,K|Z) \\
&= H(K|Z)+H(Y|Z,K) \\
&= H(K|Z) \\
&\le H(K).
\end{align}$$

Here, the first step follows from the fact that adding random variables does not decrease joint entropy; the second step uses the chain rule of conditional entropy; the third step uses that $Y$ is a deterministic function of $(Z,K)$; and the last step follows from conditioning reducing entropy.

Next, we analyze the uncertainty of $K$. Recall that
$$\begin{align}
K := \arg\min_i \; T_i \cdot \frac{dP_Y}{dP_{Y|X}(\cdot|X)}(\tilde Y_i),
\end{align}$$
where the weighting term depends on $X$, hence the distribution of $K$ varies with $X$. For analysis, fix $X=x$.
When $P_{Y \mid X}(\cdot \mid x)$ is close to $P_Y$, we have $\frac{dP_Y}{dP_{Y|X}(\cdot|x)}(y)\approx 1,$ in which case the selection rule is mainly determined by $\\{T_i\\}$. Since $\\{T_i\\}$ is increasing, smaller indices $i$ are more likely to be selected, hence $K$ tends to be small; in particular, when $P_{Y|X}(\cdot|x)=P_Y$, we have $K=1$.

This shows that the uncertainty of $K$ is closely related to the discrepancy between $P_{Y \mid X}(\cdot \mid x)$ and $P_Y$. One can show
$$\begin{align}
\mathbb{E}[\log K \mid X=x] \le D\big(P_{Y|X}(\cdot|x)\,\|\,P_Y\big) + e^{-1}\log e + 1.
\end{align}$$

Taking expectation over $X$,
$$\begin{align}
\mathbb{E}[\log K]
\le
I(X;Y) + e^{-1}\log e + 1.
\end{align}$$

Here we used the equivalent representation of mutual information.
Finally, it remains to upper bound $H(K)$ as a function of $\mathbb{E}[\log K]$.

We now state a relation between $H(K)$ and $\mathbb{E}[\log K]$.

**Lemma 3.**
<em>
Let $K\in\\{1,2,\dots\\}$. Then
$$\begin{align}
H(K)
\le
\mathbb E[\log K]
+
\log\big(\mathbb E[\log K]+1\big)
+1.
\end{align}$$
</em>

**Proof.**
Under the constraint $\mathbb{E}[\log K]=L$, consider the entropy maximization problem. Let $p_K(k)$ denote the pmf of $K$. We maximize
$$\begin{align}
H(K) = -\sum_{k=1}^\infty p_K(k)\log p_K(k)
\end{align}$$
subject to
$$\begin{align}
\sum_{k=1}^\infty p_K(k)=1,
\qquad
\sum_{k=1}^\infty p_K(k)\log k = L.
\end{align}$$

Introducing Lagrange multipliers $\alpha,\beta$, consider
$$\begin{align}
\mathcal{L}
=
-\sum_{k=1}^\infty p_K(k)\log p_K(k) + \alpha\Big(\sum_{k=1}^\infty p_K(k)-1\Big) + \beta\Big(\sum_{k=1}^\infty p_K(k)\log k - L\Big).
\end{align}$$

Taking derivative with respect to $p_K(k)$ and setting to zero yields
$$\begin{align}
p_K(k) = c\, k^{-\lambda},
\end{align}$$
where $c>0$ is a normalization constant and $\lambda=-\beta$. Thus, under fixed $\mathbb E[\log K]$, the maximum entropy distribution is of Zipf type.

To obtain an explicit bound, take
$$\begin{align}
q(k)=c\,k^{-\lambda},
\qquad
\lambda = 1+\frac{1}{L}.
\end{align}$$

By non-negativity of relative entropy,
\begin{align}
D(p_K\|q) = \sum_{k=1}^\infty p_K(k)\log\frac{p_K(k)}{q(k)} \ge 0,
\end{align}
which implies
\begin{align}
-H(K) - \sum_{k=1}^\infty p_K(k)\log q(k) \ge 0.
\end{align}

Substituting $q(k)$,
$$\begin{align}
H(K)
&\le -\sum_{k=1}^\infty p_K(k)\log\big(c\,k^{-\lambda}\big) \\
&= \lambda \sum_{k=1}^\infty p_K(k)\log k - \log c \\
&= \lambda L - \log c.
\end{align}$$

Next, estimate $c$. Note that $c^{-1}=\sum_{k=1}^\infty k^{-\lambda}.$ For $\lambda>1$,
$$\begin{align}
\sum_{k=1}^\infty k^{-\lambda}
\le 1+\int_1^\infty x^{-\lambda}\,dx
= 1+\frac{1}{\lambda-1}.
\end{align}$$

Thus,
$$\begin{align}
-\log c
\le \log\Big(1+\frac{1}{\lambda-1}\Big).
\end{align}$$

Substituting $\lambda = 1+\frac{1}{L}$ gives
$$\begin{align}
H(K)
\le L+1+\log(L+1).
\end{align}$$
$\blacksquare$

Substituting into the previous bounds,
$$\begin{align}
H(K)
&\le
I(X;Y)+e^{-1}\log e+2
+\log\big(I(X;Y)+e^{-1}\log e+2\big) \\
&\le
I(X;Y)+\log\big(I(X;Y)+1\big)+4.
\end{align}$$

Combining with $H(Y|Z)\le H(K)$, we finally obtain
$$\begin{align}
H(Y|Z)\le I(X;Y)+\log\big(I(X;Y)+1\big)+4.
\end{align}$$

### Poisson Functional Representation Generates the Target Conditional Distribution

We now show that the above Poisson functional representation construction can generate the target conditional distribution $Y \mid \\{X=x\\} \sim P_{Y \mid X}(\cdot \mid x).$
Fix any $x$, and assume that $P_{Y \mid X}(\cdot \mid x) \ll P_Y$. Consider the marked Poisson point process $Z = \\{(\tilde Y_i, T_i)\\}\_{i\ge 1},$ where $\tilde Y_i \overset{\text{i.i.d.}}{\sim} P_Y$, and $\\{T_i\\}$ are the arrival times of a Poisson process with rate $1$. The intensity measure of this point process on $\mathcal Y\times\mathbb R_+$ is
$$\begin{align}
    \nu(dy,dt)=P_Y(dy)\,dt.
\end{align}$$

Apply the transformation
$$\begin{align}
    (y,t)\mapsto\Big(y,\;t\cdot\frac{dP_Y}{dP_{Y|X}(\cdot|x)}(y)\Big).
\end{align}$$

By the mapping theorem of Poisson point processes, the transformed process is still a Poisson point process with intensity measure
$$\begin{align}
    \nu'(dy,dt)=P_{Y|X}(dy|x)\,dt.
\end{align}$$

We now state a basic result characterizing this structure.

**Lemma 4.**
<em>
Let $\Pi$ be a Poisson point process on $\mathcal Y\times\mathbb R_+$ with intensity measure $\nu(dy,dt)=P(dy)\,dt,$ where $P$ is a probability measure. Let $T_i$ denote the time coordinates and $Y_i$ the corresponding marks, and define
$$\begin{align}
    K := \arg\min_i T_i,\qquad Y := Y_K.
\end{align}$$
Then
$$\begin{align}
    Y \sim P.
\end{align}$$
</em>

**Proof.**
Since the intensity measure has the product form $P(dy)\,dt$, the point process can be equivalently represented as follows: generate a Poisson process $\\{T_i\\}$ with rate $1$ on the time axis, and independently generate marks $Y_i\sim P$ at each time point, independent of the time.

Thus, the index $K=\arg\min_i T_i$ depends only on the time sequence, and is therefore independent of the mark sequence $\\{Y_i\\}$. For any measurable set $A$, we have
$$\begin{align}
    \mathbb P(Y\in A\mid K=k)=P(A).
\end{align}$$

Marginalizing over $K$ yields
$$\begin{align}
    \mathbb P(Y\in A)=P(A),
\end{align}$$
hence $Y\sim P$.
$\blacksquare$

Applying this lemma to the current setting with $P=P_{Y \mid X}(\cdot \mid x)$, we obtain
$$\begin{align}
    Y_K' \sim P_{Y \mid X}(\cdot \mid x).
\end{align}$$

Since the construction defines $Y:=Y_K'$, and the above result holds under the condition $X=x$, we conclude
$$\begin{align}
    Y \mid \{X=x\} \sim P_{Y|X}(\cdot|x).
\end{align}$$

### Distribution of the Index Variable $K$

In this section, we analyze the distributional properties of the index variable $K$. Recall its definition
$$\begin{align}
K := \arg\min_i \; T_i \cdot \frac{dP_Y}{dP_{Y|X}(\cdot|x)}(\tilde Y_i).
\end{align}$$

For convenience of analysis, fix $X=x$, and consider the corresponding random variables.

We first state a basic property of Poisson point processes.

**Lemma 5 (Independent Restriction Property of Poisson Point Processes).**
<em>
Let $\Pi$ be a Poisson point process defined on a space $\mathcal S$ with intensity measure $\nu$. For any measurable set $C\subset \mathcal S$, conditioned on $\Pi\cap C$, the remaining point set $\Pi\cap C^c$ is still a Poisson point process with intensity measure equal to the restriction of $\nu$ to $C^c$, and is independent of $\Pi\cap C$.
</em>

In the current problem, the transformed point process has intensity measure $\nu'(dy,dt)=P_{Y|X}(dy|x)\,dt.$ Denote the earliest arrival time and corresponding mark as
$$\begin{align}
\Theta := \min_i T_i', \qquad Y:=Y_K'.
\end{align}$$

Conditioned on $\Theta=\theta$ and $Y=\tilde y$, by the above lemma, the remaining points form a Poisson point process on the region $\mathcal Y \times [\theta,\infty)$ with intensity measure
$$\begin{align}
P_{Y|X}(dy|x)\times \mu|_{[\theta,\infty)}.
\end{align}$$

Mapping this remaining process back to the original coordinates yields the corresponding original point process, whose intensity measure $\nu$ satisfies, for any measurable sets $A\subseteq \mathcal Y$ and $B\subseteq \mathbb R_+$,
$$\begin{align}
\nu(A\times B)
=
\int_A
\mu\left(
B\cap
\left[
\theta\cdot \frac{dP_{Y|X}}{dP_Y}(y|x),\,\infty
\right]
\right)
dP_Y(y).
\end{align}$$

From the definition, we have $\Theta = T_K\cdot \frac{dP_Y}{dP_{Y|X}(\cdot|x)}(\tilde y),$ hence
$$\begin{align}
T_K = \theta\cdot \frac{dP_{Y|X}}{dP_Y}(\tilde y|x).
\end{align}$$

Note that
$$\begin{align}
K-1 = \big|\{i:T_i<T_K\}\big|,
\end{align}$$
i.e., $K-1$ equals the number of points in the region $\mathcal Y\times [0,T_K)$ in the original coordinates. Therefore, conditioned on $\Theta=\theta$ and $Y=\tilde y$,
$$\begin{align}
K-1 \sim \mathrm{Poisson}\big(\nu(\mathcal Y\times [0,T_K))\big).
\end{align}$$

Next, compute this parameter. From the expression of the intensity measure,
$$\begin{align}
\nu(\mathcal Y\times [0,T_K))
&=
\int_{\mathcal Y}
\mu\left(
[0,T_K)\cap
\left[
\theta\cdot \frac{dP_{Y|X}}{dP_Y}(y|x),\,\infty
\right]
\right)
dP_Y(y).
\end{align}$$

Using the identity $\mu([0,a)\cap[b,\infty))=\max\\{0,a-b\\},$ and substituting $T_K=\theta\cdot \frac{dP_{Y|X}}{dP_Y}(\tilde y|x),$ we obtain
$$\begin{align}
\nu(\mathcal Y\times [0,T_K))
&=
\theta
\int_{\mathcal Y}
\max\left\{
0,\,
\frac{dP_{Y|X}}{dP_Y}(\tilde y|x)
-
\frac{dP_{Y|X}}{dP_Y}(y|x)
\right\}
dP_Y(y).
\end{align}$$

Furthermore, using the inequality $\max\\{0,u-v\\}\le u$, and noting that here $u=\frac{dP_{Y|X}}{dP_Y}(\tilde y|x)$ does not depend on $y$, we obtain
$$\begin{align}
\nu(\mathcal Y\times [0,T_K))
\le
\theta\cdot \frac{dP_{Y|X}}{dP_Y}(\tilde y|x).
\end{align}$$

Therefore, conditioned on $\Theta=\theta$ and $Y=\tilde y$,
$$\begin{align}
K-1 \sim \mathrm{Poisson}(\lambda),
\qquad
\lambda \le \theta\cdot \frac{dP_{Y|X}}{dP_Y}(\tilde y|x).
\end{align}$$

### Upper Bound on $\mathbb{E}[\log K]$

Conditioned on $\Theta=\theta$ and $Y=\tilde y$, we have
$$\begin{align}
\mathbb E[\log K \mid \Theta=\theta,\,Y=\tilde y]
=
\mathbb E[\log(1+(K-1)) \mid \Theta=\theta,\,Y=\tilde y].
\end{align}$$

Since the function $u\mapsto \log(1+u)$ is concave for $u\ge 0$, by Jensen’s inequality,
$$\begin{align}
\mathbb E[\log(1+(K-1)) \mid \Theta=\theta,\,Y=\tilde y]
\le
\log\left(
1+\mathbb E[K-1\mid \Theta=\theta,\,Y=\tilde y]
\right).
\end{align}$$

Since under this condition $K-1\sim \mathrm{Poisson}(\lambda)$ with mean $\lambda$, and $\lambda \le \theta\cdot \frac{dP_{Y|X}}{dP_Y}(\tilde y|x),$ we obtain
$$\begin{align}
\mathbb E[\log K \mid \Theta=\theta,\,Y=\tilde y]
\le
\log\left(
1+\theta\cdot \frac{dP_{Y|X}}{dP_Y}(\tilde y|x)
\right).
\end{align}$$

Taking expectation over $(\Theta,Y)$, and using $\Theta\sim \text{Exp}(1)$ and $Y\sim P_{Y|X}(\cdot|x)$, we obtain
$$\begin{align}
\mathbb E[\log K\mid X=x]
&=
\mathbb E_{Y\sim P_{Y|X}(\cdot|x)}
\left[
\int_0^\infty e^{-\theta}
\mathbb E[\log K\mid \Theta=\theta,\,Y]
\,d\theta
\right] \\
&\le
\mathbb E_{Y\sim P_{Y|X}(\cdot|x)}
\left[
\int_0^\infty e^{-\theta}
\log\left(
1+\theta\cdot \frac{dP_{Y|X}}{dP_Y}(Y|x)
\right)
d\theta
\right].
\end{align}$$

For each fixed $Y$, applying Jensen’s inequality again (noting that $e^{-\theta}d\theta$ is a probability measure), we obtain
$$\begin{align}
\int_0^\infty e^{-\theta}
\log(1+a\theta)\,d\theta
\le
\log\left(1+\int_0^\infty e^{-\theta}a\theta\,d\theta\right),
\end{align}$$
where $a=\frac{dP_{Y|X}}{dP_Y}(Y|x)$. Since $\int_0^\infty e^{-\theta}\theta\,d\theta = 1,$ we obtain
$$\begin{align}
\mathbb E[\log K\mid X=x]
\le
\mathbb E_{Y\sim P_{Y|X}(\cdot|x)}
\left[
\log\left(
1+\frac{dP_{Y|X}}{dP_Y}(Y|x)
\right)
\right].
\end{align}$$

Using the inequality $\log(1+u)\le \max\{\log u,0\}+1,\; u\ge 0,$ we obtain
$$\begin{align}
\mathbb E[\log K\mid X=x]
\le
\mathbb E_{Y\sim P_{Y|X}(\cdot|x)}
\left[
\max\left\{
\log \frac{dP_{Y|X}}{dP_Y}(Y|x),\,0
\right\}
+1
\right].
\end{align}$$

Using the identity $\max\\{a,0\\}=a-\min\\{a,0\\}$, we obtain
$$\begin{align}
\mathbb E[\log K\mid X=x]
&\le
\mathbb E_{Y\sim P_{Y|X}(\cdot|x)}
\left[
\log \frac{dP_{Y|X}}{dP_Y}(Y|x)
\right] \\
&\quad -
\mathbb E_{Y\sim P_{Y|X}(\cdot|x)}
\left[
\min\left\{
\log \frac{dP_{Y|X}}{dP_Y}(Y|x),\,0
\right\}
\right]
+1.
\end{align}$$

By the definition of relative entropy,
$$\begin{align}
D(P_{Y|X}(\cdot|x)\|P_Y)
=
\mathbb E_{Y\sim P_{Y|X}(\cdot|x)}
\left[
\log \frac{dP_{Y|X}}{dP_Y}(Y|x)
\right],
\end{align}$$
hence
$$\begin{align}
\mathbb E[\log K\mid X=x]
\le
D(P_{Y|X}(\cdot|x)\|P_Y)
-
\mathbb E_{Y\sim P_{Y|X}(\cdot|x)}
\left[
\min\left\{
\log \frac{dP_{Y|X}}{dP_Y}(Y|x),\,0
\right\}
\right]
+1.
\end{align}$$

We now give a bound on the negative part of the log-likelihood ratio.

**Lemma 6.**
<em>
\begin{align}
\mathbb E_{Y\sim P_{Y|X}(\cdot|x)}\left[\min\left\\{\log \frac{dP_{Y|X}}{dP_Y}(Y|x),\,0\right\\}\right]\le e^{-1}\log e.
\end{align}
</em>

**Proof.**
Let $L(y):=\frac{dP_{Y|X}}{dP_Y}(y|x).$ Then $-\min\{\log L(Y),0\} = (-\log L(Y))\,\mathbf 1\{L(Y)<1\}.$
Thus,
$$\begin{align}
-\mathbb E
\left[\min\{\log L(Y),0\}\right]
&=
\int (-\log L(y))\,\mathbf 1\{L(y)<1\}\, dP_{Y|X}(y|x) \\
&=
\int \big(-L(y)\log L(y)\big)\mathbf 1\{L(y)<1\}\,dP_Y(y).
\end{align}$$

Consider the function $f(u)=-u\log u,\; 0<u\le 1.$ Its derivative is $f'(u)=-\log u-\log e.$ Setting $f'(u)=0$ yields $u=e^{-1}$, hence
$$\begin{align}
\sup_{0<u\le 1}(-u\log u)=e^{-1}\log e.
\end{align}$$

Therefore,
$$\begin{align}
\big(-L(y)\log L(y)\big)\mathbf 1\{L(y)<1\}
\le e^{-1}\log e.
\end{align}$$

Integrating over $P_Y$ yields the desired result.
$\blacksquare$

Thus,
$$\begin{align}
\mathbb E[\log K\mid X=x]
\le
D(P_{Y|X}(\cdot|x)\|P_Y)+e^{-1}\log e+1.
\end{align}$$

Taking expectation over $X\sim P_X$, and using
$$\begin{align}
\mathbb E_X[D(P_{Y|X}(\cdot|X)\|P_Y)]=I(X;Y),
\end{align}$$
we obtain
$$\begin{align}
\mathbb E[\log K]
\le
I(X;Y)+e^{-1}\log e+1.
\end{align}$$

### Proof of the Cardinality Bound

Finally, we establish the cardinality bound in the discrete case. If $X,Y$ are discrete random variables with alphabets $\mathcal X,\mathcal Y$, then we can further restrict
$$\begin{align}
|\mathcal Z| \le |\mathcal X|(|\mathcal Y|-1)+2.
\end{align}$$

The proof proceeds in two steps.

First, since $Y$ is a deterministic function of $X$ and $Z$, there exists a mapping
$$\begin{align}
g:\mathcal X\times \mathcal Z \to \mathcal Y
\end{align}$$
such that
$$\begin{align}
Y=g(X,Z).
\end{align}$$

Thus, for each fixed $z\in\mathcal Z$, it induces a function
$$\begin{align}
g_z:\mathcal X\to \mathcal Y,\qquad g_z(x):=g(x,z).
\end{align}$$

If two different $z$ induce the same $g_z$, then they play identical roles in generating $Y$, and can be merged. Hence, without loss of generality, we may assume that different $z$ correspond to distinct functions $g_z$. Since the number of functions from $\mathcal X$ to $\mathcal Y$ is at most
$$\begin{align}
|\mathcal Y|^{|\mathcal X|},
\end{align}$$
we may assume that $|\mathcal Z|$ is finite.

Next, we further reduce the cardinality of $\mathcal Z$. For each $z\in\mathcal Z$, define the vector
$$\begin{align}
v(z)
:=
\Big(
H(Y|Z=z),\;
p(x,y|z):x\in\mathcal X,\; y\in\{1,\dots,|\mathcal Y|-1\}
\Big).
\end{align}$$

The dimension of this vector is
$$\begin{align}
d = |\mathcal X|(|\mathcal Y|-1)+1.
\end{align}$$

Here, $|\mathcal X|(|\mathcal Y|-1)$ corresponds to the degrees of freedom of the joint probability $p(x,y|z)$, and the additional $+1$ corresponds to $H(Y|Z=z)$. The reason for including $H(Y|Z=z)$ is that during the reduction of $\mathcal Z$, one must simultaneously preserve
$$\begin{align}
p(x,y)=\sum_z p(z)p(x,y|z),
\qquad
H(Y|Z)=\sum_z p(z)H(Y|Z=z),
\end{align}$$
so both must be treated as constraints.

Moreover, it suffices to record $y\in\\{1,\dots,|\mathcal Y|-1\\}$, since for each fixed $x$, the probabilities satisfy the normalization condition
$$\begin{align}
\sum_{y\in\mathcal Y} p(x,y|z)=p(x|z),
\end{align}$$
so the last component is uniquely determined by the others.

From the above representation, the vector $\Big(H(Y \mid Z),\;p(x,y):x\in\mathcal X,\; y\in\\{1,\dots,\|\mathcal Y\|-1\\}\Big)$ can be expressed as a convex combination of $\\{v(z):z\in\mathcal Z\\}$, i.e., it lies in their convex hull.

Applying Carathéodory’s theorem: in $\mathbb R^d$, any point in the convex hull of a set can be represented as a convex combination of at most $d+1$ points. Therefore, it suffices to use at most
$$\begin{align}
d+1 = |\mathcal X|(|\mathcal Y|-1)+2
\end{align}$$
values of $z$ to preserve $p(x,y)$ and $H(Y|Z)$.

Hence, without loss of generality, we can construct a new random variable $Z'$ such that
$$\begin{align}
|\mathcal Z'| \le |\mathcal X|(|\mathcal Y|-1)+2,
\end{align}$$
and still have
$$\begin{align}
Z' \perp X,\qquad Y=g'(X,Z'),
\end{align}$$
while preserving $P_{XY}$ and $H(Y|Z')=H(Y|Z)$. This completes the proof.

---

### References

This note is based on:
- Cheuk Ting Li and Abbas El Gamal, “Strong Functional Representation Lemma and Applications to Coding Theorems,” *IEEE Transactions on Information Theory*, vol. 64, no. 11, pp. 6967–6978, Nov. 2018. [IEEE Xplore](https://ieeexplore.ieee.org/abstract/document/8438492)
