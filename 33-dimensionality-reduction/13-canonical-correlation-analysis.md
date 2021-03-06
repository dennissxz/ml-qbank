# Canonical Correlation Analysis

Can we quantify the associations between two sets of variables?

- Do last year’s labor data relate or explain this year’s labor situation?
- Are the math science performance**s** of students related to their reading performance**s**?
- Are there associations between government policie**s** and economic
variable**s**?
- For decathlon athletes, is the track event performance**s** correlated with the performance in field event**s**?

## Objective

Hotelling (1936) extended the idea of multiple correlation to the problem of measuring linear association between two **groups** of variables, say $\boldsymbol{x}$ and $\boldsymbol{y}$. Thus we consider the simple correlation coefficient between every pair of **linear combinations** of elements of $\boldsymbol{x}$ and of $\boldsymbol{y}$ and choose the maximum.

$$
\max _{\boldsymbol{v}, \boldsymbol{w} } \, \operatorname{Corr}\left(\boldsymbol{v}^{\top} \boldsymbol{x} , \boldsymbol{w}^{\top} \boldsymbol{y} \right)
$$

This maximum, $\rho_1$, is called the first canonical correlation and the corresponding pair of linear combinations, say $(U_1, V_1)$, is called the first pair of canonical variables.


Since each group has more than one variable, one single correlation coefficient may miss significant linear association in other dimensions. So we consider the subclass of **all** pairs of linear combinations of elements of $\boldsymbol{x}$ and $\boldsymbol{y}$ whose members are **uncorrelated** with $(U_1, V_1）$. The maximum simple correlation coefficient, $\rho _2$, of such pairs is called the second canonical correlation and the pair, say $(U_2, V_2)$, achieving this maximum is called the second pair of canonical variables.

Continuing this way we shall get the $k$ canonical correlations and the corresponding pairs of canonical variables, where $k=\min(d_x, d_y)$ is the smallest dimension of $\boldsymbol{x}$ and $\boldsymbol{y}$.

Alternative formulations include

- minimizing the difference between two projected spaces, i.e. we want to predict projected $\boldsymbol{y}$ by projected $\boldsymbol{x}$.

    $$
    \begin{equation}
    \begin{array}{ll}
    \min & \left\| \boldsymbol{X} \boldsymbol{V} - \boldsymbol{Y}\boldsymbol{W} \right\|_{F}^{2} \\
    \text {s.t.} & \boldsymbol{V} ^\top \boldsymbol{\Sigma} _{xx} \boldsymbol{V} = \boldsymbol{W} ^\top \boldsymbol{\Sigma} _{y y} \boldsymbol{W} = \boldsymbol{I}_k  \\
    & \boldsymbol{V} \in \mathbb{R} ^{d_x \times k} \quad \boldsymbol{W} \in \mathbb{R} ^{d_y \times k} \\
    \end{array}
    \end{equation}
    $$

- maximizing the trace

    $$
    \begin{equation}
    \begin{array}{ll}
    \max & \operatorname{tr} \left( \boldsymbol{V} ^\top \boldsymbol{\Sigma} _{x y} \boldsymbol{W}  \right) \\
    \text {s.t.} & \boldsymbol{V} ^\top \boldsymbol{\Sigma} _{x x} \boldsymbol{V} = \boldsymbol{W} ^\top \boldsymbol{\Sigma} _{y y} \boldsymbol{W} = \boldsymbol{I}_k \\
    & \boldsymbol{V} \in \mathbb{R} ^{d_x \times k} \quad \boldsymbol{W} \in \mathbb{R} ^{d_y \times k} \\
    \end{array}
    \end{equation}
    $$



## Learning

Partition the covariance matrix of full rank in accordance with two groups of variables,

$$
\begin{equation}
\operatorname{Var}\left(\begin{array}{l}
\boldsymbol{x}  \\
\boldsymbol{y}
\end{array}\right)=\left(\begin{array}{ll}
\boldsymbol{\Sigma}_{xx} & \boldsymbol{\Sigma}_{xy} \\
\boldsymbol{\Sigma}_{yx} & \boldsymbol{\Sigma}_{yy}
\end{array}\right)
\end{equation}
$$

### Sequential Optimization

The first canonical correlation, $\rho _1$, equals the maximum correlation between all pairs of linear combinations of $\boldsymbol{x}$ and $\boldsymbol{y}$ with unit variance. That is,


$$\begin{align}
\max _{\boldsymbol{v}, \boldsymbol{w} } \operatorname{Corr}\left(\boldsymbol{v}^{\top} \boldsymbol{x} , \boldsymbol{w}^{\top} \boldsymbol{y} \right)
= \max &  _{\boldsymbol{v}, \boldsymbol{w}}  \frac{\boldsymbol{v}^{\top} \boldsymbol{\Sigma}_{xy} \boldsymbol{w}}{\sqrt{\boldsymbol{v}^{\top} \boldsymbol{\Sigma}_{xx} \boldsymbol{v} \boldsymbol{w}^{\top} \boldsymbol{\Sigma}_{yy} \boldsymbol{w}}} \\
\text{s.t.}  &  \ \quad \boldsymbol{v} ^\top \boldsymbol{\Sigma} _{xx} \boldsymbol{v} =1 \\
  &  \ \quad \boldsymbol{w} ^\top \boldsymbol{\Sigma} _{yy} \boldsymbol{w} =1 \\
\end{align}$$

If the maximum is achieved at $\boldsymbol{v} _1$ and $\boldsymbol{w} _1$, then the first pair of canonical variables are defined as


$$
U_{1}=\boldsymbol{v}_{1}^{\top} \boldsymbol{x} , \quad V_{1}=\boldsymbol{w}_{1}^{\top} \boldsymbol{y}
$$

Successively, for $i = 2, \ldots, k$, the $i$-th canonical correlation $\rho_i$ is defined as


$$\begin{align}
\rho_{i}
 =\max _{\boldsymbol{v}, \boldsymbol{w}} & \quad \operatorname{Corr}\left(\boldsymbol{v}^{\top} \boldsymbol{x} , \boldsymbol{w}^{\top} \boldsymbol{y} \right) \\
 \text{s.t.} &  \quad (\boldsymbol{v} ^\top \boldsymbol{x} , \boldsymbol{w} ^\top \boldsymbol{y} ) \text{ uncorrelated with } (U_1, V_1), \ldots, (U_{i-1}, V_{i-1}) \\
\end{align}$$

If the maximum is achieved at $\boldsymbol{v} _i$ and $\boldsymbol{w} _i$, then the first pair of canonical variables are defined as


$$
U_{i}=\boldsymbol{v}_{i}^{\top} \boldsymbol{x}_{i}, \quad V_{i}=\boldsymbol{w}_{i}^{\top} \boldsymbol{y}
$$

The uncorrelated constraint, for example, when solving for the second pair $(U_2, V_2)$, are

$$
\operatorname{Cov}\left(U_{1}, U_{2}\right)=0, \ \operatorname{Cov}\left(V_{1}, V_{2}\right)=0, \ \operatorname{Cov}\left(U_{1}, V_{2}\right)=0, \ \operatorname{Cov}\left(U_{2}, V_{1}\right)=0
$$

### Spectral Decomposition


Rather than obtaining pairs of canonical variables and canonical correlation sequentially, it can be shown that the canonical correlations $\rho$'s and hence pairs of canonical variables $(U,V)$’s can be obtained simultaneously by solving for
the eigenvalues $\rho^2$'s and eigenvectors $\boldsymbol{v}$’s from

$$
\boldsymbol{\Sigma}_{xx}^{-1} \boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx} \boldsymbol{v} = \rho^2 \boldsymbol{v}
$$

A difficulty of this problem is that the matrix $\boldsymbol{\Sigma}_{xx}^{-1} \boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx}$ is not symmetric. Consequently, the symmetric eigenproblem

$$
\boldsymbol{\Sigma}_{xx}^{-1/2} \boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx} \boldsymbol{\Sigma}_{xx}^{-1/2} \boldsymbol{u} = \rho^2 \boldsymbol{u}
$$

is considered instead for the computational efficiency. Note that the two matrices possess the **same** eigenvalues and their eigenvectors are linearly related by $\boldsymbol{v} = \boldsymbol{\Sigma}_{{xx}}^{-1/2} \boldsymbol{u}$. Note that $\boldsymbol{v}$ need to be normalized to satisfy the constraint $\boldsymbol{v}^{\top} \boldsymbol{\Sigma}_{x x} \boldsymbol{v}=1$.

```{margin}
After normalization, we may not have $\left\| \boldsymbol{v}  \right\| =1$ and $\left\| \boldsymbol{w}  \right\| = 1$.
```

Then we can find $\boldsymbol{w} \propto \boldsymbol{\Sigma}_{y y}^{-1} \boldsymbol{\Sigma}_{y x} \boldsymbol{v}$ subject to the constraint $\boldsymbol{w}^{\top} \boldsymbol{\Sigma}_{yy} \boldsymbol{w}=1$.

Note that the maximal embedding dimension is $\max(k) = \min(d_x, d_y)$.

:::{admonition,dropdown,seealso} *Derivation*

We consider the following maximization problem:


$$\begin{align}
\max _{\boldsymbol{v}, \boldsymbol{w} } \operatorname{Corr}\left(\boldsymbol{v}^{\top} \boldsymbol{x} , \boldsymbol{w}^{\top} \boldsymbol{y} \right)
= \max &  _{\boldsymbol{v}, \boldsymbol{w}}  \frac{\boldsymbol{v}^{\top} \boldsymbol{\Sigma}_{xy} \boldsymbol{w}}{\sqrt{\boldsymbol{v}^{\top} \boldsymbol{\Sigma}_{xx} \boldsymbol{v} \boldsymbol{w}^{\top} \boldsymbol{\Sigma}_{yy} \boldsymbol{w}}} \\
\text{s.t.}  &  \ \quad \boldsymbol{v} ^\top \boldsymbol{\Sigma} _{xx} \boldsymbol{v} =1 \\
  &  \ \quad \boldsymbol{w} ^\top \boldsymbol{\Sigma} _{yy} \boldsymbol{w} =1 \\
\end{align}$$

The Lagrangian is

$$
\begin{equation}
\mathcal{L}(\boldsymbol{v}, \boldsymbol{w}, \lambda, \theta)=\boldsymbol{v}^{\top} \boldsymbol{\Sigma}_{xy} \boldsymbol{w}-\frac{\lambda_x}{2} \left(\boldsymbol{v}^{\top} \boldsymbol{\Sigma}_{xx} \boldsymbol{v}-1\right)-\frac{\lambda_y}{2} \left(\boldsymbol{w}^{\top} \boldsymbol{\Sigma}_{yy} \boldsymbol{w}-1\right)
\end{equation}
$$

The first order conditions are

$$
\begin{aligned}
\frac{\partial f}{\partial \boldsymbol{v}} &=\boldsymbol{\Sigma}_{xy} \boldsymbol{w}-\lambda_{x} \boldsymbol{\Sigma}_{xx} \boldsymbol{v}=\boldsymbol{0} \qquad (1)\\
\frac{\partial f}{\partial \boldsymbol{w}} &=\boldsymbol{\Sigma}_{yx} \boldsymbol{v}-\lambda_{y} \boldsymbol{\Sigma}_{yy} \boldsymbol{w}=\boldsymbol{0} \qquad (2)
\end{aligned}
$$

Premultiply $(1)$ by $\boldsymbol{v} ^\top$ and $(2)$ by $\boldsymbol{w} ^\top$, we have

$$
\begin{aligned}
\boldsymbol{v}^{\top} \boldsymbol{\Sigma}_{xy} \boldsymbol{w} &=\lambda_{x} \\
\boldsymbol{w}^{\top} \boldsymbol{\Sigma}_{yx} \boldsymbol{v} &= \lambda_{y} \\
\end{aligned}
$$

which implies that $\lambda_x = \lambda_y$. Let $\lambda_x = \lambda_y = \lambda$. Suppose $\boldsymbol{\Sigma} _{yy}$ is invertible, then $(2)$ gives

$$
\boldsymbol{w}=\frac{\boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx} \boldsymbol{v}}{\lambda} \qquad (3)
$$

Substituting this into $(1)$ gives

$$
\frac{\boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx} \boldsymbol{v}}{\lambda}-\lambda \boldsymbol{\Sigma}_{xx}\boldsymbol{v}=0
$$

i.e.,

$$
\boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx} \boldsymbol{v}=\lambda^{2} \boldsymbol{\Sigma}_{{xx}} \boldsymbol{v}
$$

Suppose $\boldsymbol{\Sigma} _{xx}$ is invertible, then it becomes an eigenproblem

$$
\boldsymbol{\Sigma}_{{xx}} ^{-1} \boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx} \boldsymbol{v}=\lambda^{2}  \boldsymbol{v}
$$

Once the solution for $\boldsymbol{v}$  is obtained, the solution for $\boldsymbol{w}$  can be obtained by $(3)$

$$
\begin{equation}
\boldsymbol{w} \propto \boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx} \boldsymbol{v}
\end{equation}
$$

with the normalized condition

$$
\begin{equation}
\boldsymbol{w}^{\top} \boldsymbol{\Sigma}_{yy} \boldsymbol{w}=1
\end{equation}
$$

To convert the eigenproblem to be symmetric for computational efficiency, we can write $\boldsymbol{\Sigma} _{xx} = (\boldsymbol{\Sigma} _{xx} ^{1/2}) (\boldsymbol{\Sigma} _{xx} ^{1/2})$ and let $\boldsymbol{u} = \boldsymbol{\Sigma} _{xx} ^{1/2} \boldsymbol{v}$ or $\boldsymbol{\Sigma} _{xx} ^{-1/2} \boldsymbol{u} = \boldsymbol{v}$. Substituting this into

$$
\boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx} \boldsymbol{v}=\lambda^{2} \boldsymbol{\Sigma}_{{xx}} \boldsymbol{v}
$$

gives


$$\begin{aligned}
\boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx} \boldsymbol{\Sigma}_{{xx}}^{-1/2} \boldsymbol{u} &=\lambda^{2} \boldsymbol{\Sigma}_{{xx}}^{1/2} \boldsymbol{u}  \\
\boldsymbol{\Sigma}_{{xx}}^{-1/2}\boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx} \boldsymbol{\Sigma}_{{xx}}^{-1/2} \boldsymbol{u} &=\lambda^{2} \boldsymbol{u}  \\
\end{aligned}$$

Then the eigenproblem becomes symmetric and easier to solve. We can find $\boldsymbol{u}$ and then find $\boldsymbol{v} = \boldsymbol{\Sigma} _{xx} ^{-1/2} \boldsymbol{u}$, and then find $\boldsymbol{w} \propto \boldsymbol{\Sigma}_{y y}^{-1} \boldsymbol{\Sigma}_{y x} \boldsymbol{v}$.

:::

## Properties

- $\operatorname{Var}\left(U_{k}\right) = \operatorname{Var}\left(V_{k}\right)=1$
- $0 = \operatorname{Cov}\left(U_{k}, U_{\ell}\right) = \operatorname{Cov}\left(V_{k}, V_{\ell}\right)=\operatorname{Cov}\left(U_{k}, V_{\ell}\right) = \operatorname{Cov}\left(U_{\ell}, V_{k}\right)\text { for } k \neq \ell$
- $\operatorname{Cov}\left(U_{i}, V_{i}\right)=\rho_{i}$, where $\rho_i^2$ is the $i$-th largest eigenvalue of the following matrices
  - $d_x \times d_x \quad \boldsymbol{C} \boldsymbol{C}^{\top}=\boldsymbol{\Sigma}_{xx}^{-1 / 2} \boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx} \boldsymbol{\Sigma}_{xx}^{-1 / 2}$ where $\boldsymbol{C} =\boldsymbol{\Sigma}_{xx}^{-1 / 2} \boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1/2}$
  - $d_y \times d_y \quad \boldsymbol{C}^{\top} \boldsymbol{C}=\boldsymbol{\Sigma}_{yy}^{-1 / 2} \boldsymbol{\Sigma}_{yx} \boldsymbol{\Sigma}_{xx}^{-1} \boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1 / 2}$
  - $d_x \times d_x \quad \boldsymbol{A}=\boldsymbol{\Sigma}_{xx}^{-1} \boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx}=\boldsymbol{\Sigma}_{xx}^{-1 / 2} \boldsymbol{C} \boldsymbol{C}^{\top} \boldsymbol{\Sigma}_{xx}^{1 / 2}$
  - $d_y \times d_y \quad \boldsymbol{B}=\boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx} \boldsymbol{\Sigma}_{xx}^{-1} \boldsymbol{\Sigma}_{xy}=\boldsymbol{\Sigma}_{yy}^{-1 / 2} \boldsymbol{C}^{\top} \boldsymbol{C} \boldsymbol{\Sigma}_{yy}^{1 / 2}$
  - In fact, they are [similar](similar-matrix) $\boldsymbol{A} \sim \boldsymbol{C} \boldsymbol{C} ^{\top}$, $\boldsymbol{B} \sim \boldsymbol{C} ^{\top} \boldsymbol{C}$, and $\boldsymbol{C} \boldsymbol{C} ^{\top}$ share the same nonzero eigenvalues with $\boldsymbol{C} ^{\top} \boldsymbol{C}$ (hint: SVD).
- The above identities can be summarized as

  $$
  \operatorname{Cov}\left([U_{1}, \cdots, U_{k}, V_{1}, \cdots, V_{k}]\right)=\left[\begin{array}{cc}
  \boldsymbol{I}_{k} & \boldsymbol{R}_{k} \\
  \boldsymbol{R}_{k} & \boldsymbol{I}_{k}
  \end{array}\right], \quad \boldsymbol{R}_{k}=\operatorname{diag}\left[\rho_{1}^{*}, \cdots, \rho_{k}^{*}\right]
  $$

  If sort in canonical variate pairs,

  $$
  \operatorname{Cov}\left([U_{1}, V_{1}, \cdots, U_{k}, V_{k}]\right)=\operatorname{diag}\left[\boldsymbol{D}_{1}, \cdots, \boldsymbol{D}_{k}\right], \quad \boldsymbol{D}_{i}=\left[\begin{array}{cc}
  1 & \rho_{i}^{*} \\
  \rho_{i}^{*} & 1
  \end{array}\right]
  $$

- Invariance property: Canonical correlations $\rho_i$'s between $\boldsymbol{x}$ and $\boldsymbol{y}$ are the same as those between $\boldsymbol{A} _1 \boldsymbol{x}  + \boldsymbol{c}_1$ and $\boldsymbol{A} _2 \boldsymbol{y}  + \boldsymbol{c} _2$, where both $\boldsymbol{A} _1$ and $\boldsymbol{A} _2$ are non-singular square matrices and their computation can be based on either the partitioned covariance matrix or the partitioned correlation matrix. However, the canonical coefficients contained in $\boldsymbol{v} _k$ and $\boldsymbol{w} _k$ are **not** invariant under the same transform, nor their estimates.


## Model Selection

Given a sample of data matrix $\boldsymbol{X}$ and $\boldsymbol{Y}$, let $\boldsymbol{S} _{xx}, \boldsymbol{S} _{12}, \boldsymbol{S} _{yy}$ and $\boldsymbol{S} _{yx}$ be the corresponding sub-matrices of the sample covariance matrix $\boldsymbol{S}$. For $i = 1, 2, \ldots, k$, let $r_i ^2, \boldsymbol{a} _i$ and $\boldsymbol{b} _i$ be respectively the sample estimators of $\rho_i^2, \boldsymbol{v} _i$ and $\boldsymbol{w} _i$, all based on

$$\boldsymbol{S}_{xx}^{-1 / 2} \boldsymbol{S}_{12} \boldsymbol{S}_{yy}^{-1} \boldsymbol{S}_{yx} \boldsymbol{S}_{xx}^{-1 / 2}$$

in parallel to $\boldsymbol{\Sigma}_{xx}^{-1/2} \boldsymbol{\Sigma}_{xy} \boldsymbol{\Sigma}_{yy}^{-1} \boldsymbol{\Sigma}_{yx} \boldsymbol{\Sigma}_{xx}^{-1/2}$. Then the $i$-th pair of sample canonical variables $\widehat{U}_i, \widehat{V}_i$ is


$$
\begin{equation}
\left\{\begin{array}{l}
\widehat{U}_{i}=\boldsymbol{a} _{i}^{\top} \boldsymbol{x}  \\
\widehat{V}_{i}=\boldsymbol{b}_{i}^{\top} \boldsymbol{y} , \text { where } \boldsymbol{b}_{i}=\boldsymbol{S}_{yy}^{-1} \boldsymbol{S}_{yx} \boldsymbol{a}_{i}
\end{array}\right.
\end{equation}
$$

How to choose $k$?

### Hypothesis Testing

Since these are not the population quantities and we don’t know whether some $\rho_i$ are zero, or equivalently how many pairs of the canonical variables based on the sample to be retained. This can be answered by testing a sequence of null hypotheses of the form

$$
H_{0}(k): \rho_{k+1}=\cdots=\rho_{k}=0, k=0,1, \cdots, k
$$


until we accept one of them. Note that the first hypothesis of retaining no pair,

$$
H_{0}(k=0): \rho_{1}=\cdots=\rho_{k}=0
$$

is equivalent to independence between $\boldsymbol{x} 1$ and $\boldsymbol{y}$, or $H_0: \boldsymbol{\Sigma} _{12} = 0$. \boldsymbol{I}f it is rejected, test

$$H_{0}(k=1): \rho_{2}=\cdots=\rho_{k}=0$$

i.e., retain only the first pair; if rejected, test

$$
H_{0}(k=2): \rho_{3}=\cdots=\rho_{k}=0
$$

i.e., retain only the first two pairs, etc., until we obtain $k$ such that

$$
H_{0}(k): \rho_{k+1}=\cdots=\rho_{k}=0
$$

is accepted. Then we shall retain only the first $k$ pairs of canonical variables to describe the linear association between $\boldsymbol{x}$ and $\boldsymbol{y}$.


## Interpretation


The meanings of the canonical variables are to be interpreted either
- in terms of the relative weighting of the coefficients associated with the original variables, or
- by comparison of the correlations of a canonical variable with original variables.

It is an art to provide a good name to a canonical variable that represents the interpretation and often requires subject-matter knowledge in the field.


## Pros and Cons


### Discriminative Power

Unlike PCA, CCA has discriminative power in some cases. \boldsymbol{I}n the comparison below, in the first scatter-plot, the principal direction is the discriminative direction, while in the second plot it is not. The 3rd (same as the 2nd) and the 4th plots corresponds to $\boldsymbol{x} \in \mathbb{R} ^2$ and $\boldsymbol{y} \in \mathbb{R} ^2$. The two colors means two kinds of data points in the $n\times 4$ data set, but the color labels are shown to CCA. The CCA solutions to $\boldsymbol{x}$ (3rd plot) is the direction $(-1,1)$ and to $\boldsymbol{y}$ (4th plot) is the direction $(-1,-1)$. Because they are the highest correlation pair of directions.

:::{figure,myclass} cca-has-disc-power
<img src="../imgs/cca-has-disc-power.png" width = "90%" alt=""/>

CCA has discriminative power [Livescu 2021]
:::


### Overfitting

CCA tends to overfit, i.e. find spurious correlations in the training data. Solutions:

- regularize CCA
- do an initial dimensionality reduction via PCA to filter the tiny signals that are correlated.


## Regularized CCA

To regularize CCA, we can add small constant $r$ (noise) to the covariance matrices of $\boldsymbol{x}$ and $\boldsymbol{y}$.

$$
\begin{equation}
\boldsymbol{v}_{1}, \boldsymbol{w}_{1}=\underset{\boldsymbol{v}, \boldsymbol{w}}{\operatorname{argmax}} \frac{\boldsymbol{v} ^\top  \boldsymbol{\Sigma}_{x y} \boldsymbol{w}}{\sqrt{\boldsymbol{v} ^\top \left(\boldsymbol{\Sigma}_{x x}+r_{x} \boldsymbol{I}\right) \boldsymbol{v} \boldsymbol{w} ^\top \left(\boldsymbol{\Sigma}_{y y}+r_{y} \boldsymbol{I}\right) \boldsymbol{w}}}
\end{equation}
$$

Then we solve for the eigenvalues's and eigenvectors’s of the new matrix

$$
\begin{equation}
\left(\boldsymbol{\Sigma}_{x x}+r_{x} \boldsymbol{I}\right)^{-1} \boldsymbol{\Sigma}_{x y}\left(\boldsymbol{\Sigma}_{y y}+r_{y} \boldsymbol{I}\right)^{-1} \boldsymbol{\Sigma}_{y x}
\end{equation}
$$

## Kernel CCA

Like Kernel PCA, we can generalize CCA with kernels.

Ref
- A kernel method for canonical correlation analysis. Shotaro Akaho 2001.
- Canonical correlation analysis; An overview with application to learning methods. David R. Hardoon 2003.

### Kernelization

Recall the original optimization problem of CCA

$$\begin{align}
\max _{\boldsymbol{v}, \boldsymbol{w} } \operatorname{Corr}\left(\boldsymbol{v}^{\top} \boldsymbol{x} , \boldsymbol{w}^{\top} \boldsymbol{y} \right)
= \max &  _{\boldsymbol{v}, \boldsymbol{w}}  \frac{\boldsymbol{v}^{\top} \boldsymbol{\Sigma}_{xy} \boldsymbol{w}}{\sqrt{\boldsymbol{v}^{\top} \boldsymbol{\Sigma}_{xx} \boldsymbol{v} \boldsymbol{w}^{\top} \boldsymbol{\Sigma}_{yy} \boldsymbol{w}}} \\
\text{s.t.}  &  \ \quad \boldsymbol{v} ^\top \boldsymbol{\Sigma} _{xx} \boldsymbol{v} =1 \\
  &  \ \quad \boldsymbol{w} ^\top \boldsymbol{\Sigma} _{yy} \boldsymbol{w} =1 \\
\end{align}$$

Consider two feature transformations, $\boldsymbol{\phi} _x: \mathbb{R} ^{d_x} \rightarrow \mathbb{R} ^{p_x}$ and $\boldsymbol{\phi} _x: \mathbb{R} ^{d_y} \rightarrow \mathbb{R} ^{p_y}$. Let

- $\boldsymbol{\Phi} _x$ and $\boldsymbol{\Phi} _y$ be the transformed data matrix.
- $\boldsymbol{C}_x = \frac{1}{n} \boldsymbol{\Phi} _x ^\top \boldsymbol{\Phi} _x, \boldsymbol{C}_y = \frac{1}{n} \boldsymbol{\Phi} _y ^\top \boldsymbol{\Phi} _y, \boldsymbol{C}_{xy} = \frac{1}{n} \boldsymbol{\Phi} _x ^\top \boldsymbol{\Phi} _y, \boldsymbol{C}_{yx} = \frac{1}{n} \boldsymbol{\Phi} _y ^\top \boldsymbol{\Phi} _x$ be the corresponding variance-covariance matrices.

Then the problem is to solve $\boldsymbol{v}, \boldsymbol{w}$ in

$$\begin{align}
\max _{\boldsymbol{v} , \boldsymbol{w}} \operatorname{Corr}\left(\boldsymbol{v}^{\top} \boldsymbol{\phi}_x ( \boldsymbol{x}), \boldsymbol{w}^{\top} \boldsymbol{\phi}_y (\boldsymbol{y})\right)= \max &  _{\boldsymbol{v}, \boldsymbol{w}}  \frac{\boldsymbol{v}^{\top} \boldsymbol{C}_{xy} \boldsymbol{w}}{\sqrt{\boldsymbol{v}^{\top} \boldsymbol{C}_{xx} \boldsymbol{v} \boldsymbol{w}^{\top} \boldsymbol{C}_{yy} \boldsymbol{w}}} \\
\text{s.t.}  &  \ \quad \boldsymbol{v} ^\top \boldsymbol{C} _{xx} \boldsymbol{v} =1 \\
  &  \ \quad \boldsymbol{w} ^\top \boldsymbol{C} _{yy} \boldsymbol{w} =1 \\
\end{align}$$


It can be shown that, the solution vectors $\boldsymbol{v}$ and $\boldsymbol{w}$ are linear combinations of the data vectors $\boldsymbol{\phi} _x(\boldsymbol{x} _i)$ and $\boldsymbol{\phi} _y (\boldsymbol{y} _i)$, i.e.

$$\begin{aligned}
\boldsymbol{v} &= \boldsymbol{\Phi} _x ^\top \boldsymbol{\alpha}\\
\boldsymbol{w} &= \boldsymbol{\Phi} _y ^\top \boldsymbol{\beta} \\
\end{aligned}$$

:::{admonition,dropdown,seealso} *Derivation??*

$$\begin{aligned}
\boldsymbol{C} ^{-1}  _x \boldsymbol{C} _{xy} \boldsymbol{C} _y ^{-1} \boldsymbol{C} _{yx} \boldsymbol{v}  &= \lambda \boldsymbol{v}  \\
\Rightarrow\quad \frac{1}{n} \boldsymbol{\Phi} _x ^\top \boldsymbol{\Phi} _y \boldsymbol{C} _y ^{-1}
\frac{1}{n} \boldsymbol{\Phi} _y ^\top \boldsymbol{\Phi} _x  \boldsymbol{v}  &= \lambda \boldsymbol{C} _x \boldsymbol{v}  \\
\Rightarrow\quad \boldsymbol{\Phi} _x  ^\top \boldsymbol{\alpha}  &= \lambda \boldsymbol{C} _x\boldsymbol{v} \\
...&= \\
\end{aligned}$$

:::

Substituting them back to the objective function, we have


$$\begin{aligned}
\rho&=\max _{\boldsymbol{\boldsymbol{\alpha}} , \boldsymbol{\boldsymbol{\beta}} } \frac{\boldsymbol{\alpha}^{\top} \boldsymbol{\Phi}_x \boldsymbol{\Phi}_x^{\top} \boldsymbol{\Phi}_y \boldsymbol{\Phi}_y^{\top} \boldsymbol{\beta}}{\sqrt{\boldsymbol{\alpha}^{\top} \boldsymbol{\Phi}_x \boldsymbol{\Phi}_x^{\top} \boldsymbol{\Phi}_x \boldsymbol{\Phi}_x^{\top} \boldsymbol{\alpha} \cdot \boldsymbol{\beta}^{\top} \boldsymbol{\Phi}_y \boldsymbol{\Phi}_y^{\top} \boldsymbol{\Phi}_y \boldsymbol{\Phi}_y^{\top} \boldsymbol{\beta}}} \\
&=\max _{\boldsymbol{\boldsymbol{\alpha}} , \boldsymbol{\boldsymbol{\beta}} } \frac{\boldsymbol{\alpha}^{\top} \boldsymbol{K}_x \boldsymbol{K}_y   \boldsymbol{\beta}}{\sqrt{\boldsymbol{\alpha}^\top \boldsymbol{K}_x^2  \boldsymbol{\alpha} \cdot \boldsymbol{\beta}^{\top} \boldsymbol{K}_y^2 \boldsymbol{\beta}}} \\
\end{aligned}$$

which is the **dual form**.

Note that the value if not affected by re-scaling of $\boldsymbol{\alpha}$ and $\boldsymbol{\beta}$ either together or independently. Hence the KCCA optimization problem is equivalent to

$$\begin{align}
\max  _{\boldsymbol{\alpha}, \boldsymbol{\beta}} &&  \boldsymbol{\alpha} ^\top \boldsymbol{K}_x \boldsymbol{K} _y \boldsymbol{\beta} \\
\text{s.t.} &&  \boldsymbol{\alpha} ^\top \boldsymbol{K} _x ^2 \boldsymbol{\alpha} = 1\\
&& \boldsymbol{\beta} ^\top \boldsymbol{K} _y ^2 \boldsymbol{\beta} =1\\
\end{align}$$


The corresponding Lagrangian is


$$
\mathcal{L}(\lambda, \boldsymbol{\alpha}, \boldsymbol{\beta})=\boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x} \boldsymbol{K}_{y} \boldsymbol{\beta}-\frac{\lambda_{\boldsymbol{\alpha}}}{2}\left(\boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x}^{2} \boldsymbol{\alpha}-1\right)-\frac{\lambda_{\boldsymbol{\beta}}}{2}\left(\boldsymbol{\beta}^{\top} \boldsymbol{K}_{y}^{2} \boldsymbol{\beta}-1\right)
$$

Taking derivatives w.r.t. $\boldsymbol{\boldsymbol{\alpha}}$ and $\boldsymbol{\boldsymbol{\beta}}$ gives

$$
\begin{array}{l}
\frac{\partial f}{\partial \boldsymbol{\alpha}}=\boldsymbol{K}_{x} \boldsymbol{K}_{y} \boldsymbol{\beta}-\lambda_{\boldsymbol{\alpha}} \boldsymbol{K}_{x}^{2} \boldsymbol{\alpha}=\mathbf{0} \\
\frac{\partial f}{\partial \boldsymbol{\beta}}=\boldsymbol{K}_{y} \boldsymbol{K}_{x} \boldsymbol{\alpha}-\lambda_{\boldsymbol{\beta}} \boldsymbol{K}_{y}^{2} \boldsymbol{\beta}=\mathbf{0}
\end{array}
$$

Subtracting $\boldsymbol{\boldsymbol{\beta}} ^\top$ times the second equation from $\boldsymbol{\boldsymbol{\alpha}} ^\top$ times the first we have

$$
\begin{aligned}
0 &=\boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x} \boldsymbol{K}_{y} \boldsymbol{\beta}-\boldsymbol{\alpha}^{\top} \lambda_{\boldsymbol{\alpha}} \boldsymbol{K}_{x}^{2} \boldsymbol{\alpha}-\boldsymbol{\beta}^{\top} \boldsymbol{K}_{y} \boldsymbol{K}_{x} \boldsymbol{\alpha}+\boldsymbol{\beta}^{\top} \lambda_{\boldsymbol{\beta}} \boldsymbol{K}_{y}^{2} \boldsymbol{\beta} \\
&=\lambda_{\boldsymbol{\beta}} \boldsymbol{\beta}^{\top} \boldsymbol{K}_{y}^{2} \boldsymbol{\beta}-\lambda_{\boldsymbol{\alpha}} \boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x}^{2} \boldsymbol{\alpha}
\end{aligned}
$$

which together with the constraints implies $\lambda_\alpha - \lambda_\beta =0$. Let them be $\lambda$. Suppose $\boldsymbol{\boldsymbol{K}} _x$ and $\boldsymbol{\boldsymbol{K}} _y$ are invertible (usually the case), then the system of equations given by the derivatives yields

$$
\begin{aligned}
\boldsymbol{\beta} &=\frac{\boldsymbol{K}_{y}^{-1} \boldsymbol{K}_{y}^{-1} \boldsymbol{K}_{y} \boldsymbol{K}_{x} \boldsymbol{\alpha}}{\lambda} \\
&=\frac{\boldsymbol{K}_{y}^{-1} \boldsymbol{K}_{x} \boldsymbol{\alpha}}{\lambda}
\end{aligned}
$$

and hence

$$
\boldsymbol{K}_{x} \boldsymbol{K}_{y} \boldsymbol{K}_{v}^{-1} \boldsymbol{K}_{x} \boldsymbol{\alpha}-\lambda^{2} \boldsymbol{K}_{x} \boldsymbol{K}_{x} \boldsymbol{\alpha}=0
$$

or

$$
I \boldsymbol{\alpha}=\lambda^{2} \boldsymbol{\alpha}
$$

Therefore, $\boldsymbol{\alpha}$ can be any unit vector $\boldsymbol{e} _j$, and we can find the corresponding $\boldsymbol{\beta}$ be the $j$-th column of $\boldsymbol{K}_{y}^{-1} \boldsymbol{K}_{x}$. Substituting back to the objective function, we found $\rho = 1$. The corresponding weights are $\boldsymbol{v} = \boldsymbol{\Phi} _x ^\top \boldsymbol{\alpha} = \boldsymbol{\phi} (\boldsymbol{x} _j)$, and $\boldsymbol{w} = \boldsymbol{\Phi} _y ^\top \boldsymbol{\beta}$.

This is a trivial solution. It is therefore clear that a naive application of CCA in kernel defined feature space will not provide useful results. Regularization is necessary.

### Regularization

To obtain non-trivial solution, we add regularization term, which is typically the norm of the weights $\boldsymbol{v}$ and $\boldsymbol{w}$.

$$
\begin{aligned}
\rho &=\max _{\boldsymbol{\alpha}, \boldsymbol{\beta}} \frac{\boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x} \boldsymbol{K}_{y} \boldsymbol{\beta}}{\sqrt{\left.\left(\boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x}^{2} \boldsymbol{\alpha}+r\left\|\boldsymbol{v} \right\|^{2}\right) \cdot\left(\boldsymbol{\beta}^{\top} \boldsymbol{K}_{y}^{2} \boldsymbol{\beta}+r\left\|\boldsymbol{w} \right\|^{2}\right)\right)}} \\
&=\max _{\boldsymbol{\alpha}, \boldsymbol{\beta}} \frac{\boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x} \boldsymbol{K}_{y} \boldsymbol{\beta}}{\sqrt{\left(\boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x}^{2} \boldsymbol{\alpha}+r \boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x} \boldsymbol{\alpha}\right) \cdot\left(\boldsymbol{\beta}^{\top} \boldsymbol{K}_{y}^{2} \boldsymbol{\beta}+r \boldsymbol{\beta}^{\top} \boldsymbol{K}_{y} \boldsymbol{\beta}\right)}}
\end{aligned}
$$

Likewise, we observe that the new regularized equation is not affected by re-scaling of $\boldsymbol{\alpha}$ or $\boldsymbol{\beta}$, hence the optimization problem is subject to

$$
\begin{aligned}
\left(\boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x}^{2} \boldsymbol{\alpha}+r \boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x} \boldsymbol{\alpha}\right) &=1 \\
\left(\boldsymbol{\beta}^{\top} \boldsymbol{K}_{y}^{2} \boldsymbol{\beta}+r \boldsymbol{\beta}^{\top} \boldsymbol{K}_{y} \boldsymbol{\beta}\right) &=1
\end{aligned}
$$

The resulting Lagrangian is

$$
\begin{aligned}
\mathcal{L}\left(\lambda_{\boldsymbol{\alpha}}, \lambda_{\boldsymbol{\beta}}, \boldsymbol{\alpha}, \boldsymbol{\beta}\right)=& \boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x} \boldsymbol{K}_{y} \boldsymbol{\beta} \\
&-\frac{\lambda_{\boldsymbol{\alpha}}}{2}\left(\boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x}^{2} \boldsymbol{\alpha}+r \boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x} \boldsymbol{\alpha}-1\right) \\
&-\frac{\lambda_{\boldsymbol{\beta}}}{2}\left(\boldsymbol{\beta}^{\top} \boldsymbol{K}_{y}^{2} \boldsymbol{\beta}+r \boldsymbol{\beta}^{\top} \boldsymbol{K}_{y} \boldsymbol{\beta}-1\right)
\end{aligned}
$$

The derivatives are

$$
\begin{aligned}
&\frac{\partial f}{\partial \boldsymbol{\alpha}}=\boldsymbol{K}_{x} \boldsymbol{K}_{y} \boldsymbol{\beta}-\lambda_{\boldsymbol{\alpha}}\left(\boldsymbol{K}_{x}^{2} \boldsymbol{\alpha}+r \boldsymbol{K}_{x} \boldsymbol{\alpha}\right)\\
&\frac{\partial f}{\partial \boldsymbol{\beta}}=\boldsymbol{K}_{y} \boldsymbol{K}_{x} \boldsymbol{\alpha}-\lambda_{\boldsymbol{\beta}}\left(\boldsymbol{K}_{y}^{2} \boldsymbol{\beta}+r \boldsymbol{K}_{y} \boldsymbol{\beta}\right)
\end{aligned}
$$

By the same trick, we have

$$
\begin{aligned}
0 &=\boldsymbol{\alpha}^{\top} \boldsymbol{K}_{x} \boldsymbol{K}_{y} \boldsymbol{\beta}-\lambda_{\boldsymbol{\alpha}} \boldsymbol{\alpha}^{\top}\left(\boldsymbol{K}_{x}^{2} \boldsymbol{\alpha}+r \boldsymbol{K}_{x} \boldsymbol{\alpha}\right)-\boldsymbol{\beta}^{\top} \boldsymbol{K}_{y} \boldsymbol{K}_{x} \boldsymbol{\alpha}+\lambda_{\boldsymbol{\beta}} \boldsymbol{\beta}^{\top}\left(\boldsymbol{K}_{y}^{2} \boldsymbol{\beta}+r \boldsymbol{K}_{y} \boldsymbol{\beta}\right) \\
&=\lambda_{\boldsymbol{\beta}} \boldsymbol{\beta}^{\top}\left(\boldsymbol{K}_{y}^{2} \boldsymbol{\beta}+r \boldsymbol{K}_{y} \boldsymbol{\beta}\right)-\lambda_{\boldsymbol{\alpha}} \boldsymbol{\alpha}^{\top}\left(\boldsymbol{K}_{x}^{2} \boldsymbol{\alpha}+r \boldsymbol{K}_{x} \boldsymbol{\alpha}\right)
\end{aligned}
$$

which gives $\lambda_\alpha = \lambda_\beta =0$. Let them be $\lambda$, and suppose $\boldsymbol{K}_x$ and $\boldsymbol{K}_y$ are invertible, we have

$$
\begin{aligned}
\boldsymbol{\beta} &=\frac{\left(\boldsymbol{K}_{y}+r \boldsymbol{I} \right)^{-1} \boldsymbol{K}_{y}^{-1} \boldsymbol{K}_{y} \boldsymbol{K}_{x} \boldsymbol{\alpha}}{\lambda} \\
&=\frac{\left(\boldsymbol{K}_{y}+r \boldsymbol{I} \right)^{-1} \boldsymbol{K}_{x} \boldsymbol{\alpha}}{\lambda}
\end{aligned}
$$

and hence

$$
\begin{aligned}
\boldsymbol{K}_{x} \boldsymbol{K}_{y}\left(\boldsymbol{K}_{y}+r \boldsymbol{I}\right)^{-1} \boldsymbol{K}_{x} \boldsymbol{\alpha} &=\lambda^{2} \boldsymbol{K}_{x}\left(\boldsymbol{K}_{x}+r \boldsymbol{I}\right) \boldsymbol{\alpha} \\
\boldsymbol{K}_{y}\left(\boldsymbol{K}_{y}+r \boldsymbol{I}\right)^{-1} \boldsymbol{K}_{x} \boldsymbol{\alpha} &=\lambda^{2}\left(\boldsymbol{K}_{x}+r \boldsymbol{I}\right) \boldsymbol{\alpha} \\
\left(\boldsymbol{K}_{x}+r \boldsymbol{I}\right)^{-1} \boldsymbol{K}_{y}\left(\boldsymbol{K}_{y}+r \boldsymbol{I}\right)^{-1} \boldsymbol{K}_{x} \boldsymbol{\alpha} &=\lambda^{2} \boldsymbol{\alpha}
\end{aligned}
$$

Therefore, we just solve the above eigenproblem to get meaningful $\boldsymbol{\alpha}$, and then compute $\boldsymbol{\beta}$.

### Learning

From the analysis above, the steps to train a kernel CCA are

1. Choose a kernel function $k(\cdot, \cdot)$.
2. Compute the centered kernel matrix $\boldsymbol{K} ^c _x = (\boldsymbol{I} - \boldsymbol{u} \boldsymbol{u} ^\top )\boldsymbol{K}_x(\boldsymbol{I} - \boldsymbol{u} \boldsymbol{u} ^\top)$ and $\boldsymbol{K} _y ^c$
3. Find the first $k$ eigenvectors of $\left(\boldsymbol{K} ^c_{x}+r \boldsymbol{I}\right)^{-1} \boldsymbol{K} ^\prime_{y}\left(\boldsymbol{K} ^c_{y}+r \boldsymbol{I}\right)^{-1} \boldsymbol{K} ^c_{x}$, store in $\boldsymbol{A}$.

Then

- to project a new data vector $\boldsymbol{x}$, note that

    $$
    \boldsymbol{w} _ {x,j} = \boldsymbol{\Phi} _x ^\top  \boldsymbol{\alpha}_{j}
    $$

    Hence, the embeddings $\boldsymbol{z}$ of a vector $\boldsymbol{x}$ is

    $$
    \boldsymbol{z} _x
    = \left[\begin{array}{c}
    \boldsymbol{w} _{x, 1} ^\top \boldsymbol{\phi}(\boldsymbol{x}) \\
    \boldsymbol{w} _{x, 2} ^\top \boldsymbol{\phi}(\boldsymbol{x}) \\
    \vdots \\
    \boldsymbol{w} _{x, k} ^\top \boldsymbol{\phi}(\boldsymbol{x}) \\
    \end{array}\right]
    = \left[\begin{array}{c}
    \boldsymbol{\alpha} _1 ^\top  \boldsymbol{\Phi}_x  \\
    \boldsymbol{\alpha} _2 ^\top  \boldsymbol{\Phi}_x  \\
    \vdots \\
    \boldsymbol{\alpha} _k ^\top  \boldsymbol{\Phi}_x  \\
    \end{array}\right] \boldsymbol{\phi}(\boldsymbol{x})
    = \boldsymbol{A} ^\top \boldsymbol{\Phi}_x \boldsymbol{\phi}(\boldsymbol{x})
    = \boldsymbol{A} ^\top \left[\begin{array}{c}
    k(\boldsymbol{x} _1, \boldsymbol{x}) \\
    k(\boldsymbol{x} _2, \boldsymbol{x}) \\
    \vdots \\
    k(\boldsymbol{x} _n, \boldsymbol{x}) \\
    \end{array}\right]\\
    $$

    where $\boldsymbol{A} _{n\times k}$ are the first $k$ eigenvectors $\boldsymbol{\alpha}$.


- to project the training data $\boldsymbol{X}$,

    $$\boldsymbol{Z} ^\top  = \boldsymbol{A} ^\top \boldsymbol{K}_x \text{ or } \boldsymbol{Z} = \boldsymbol{K}_x \boldsymbol{A} $$


- to project a new data matrix $\boldsymbol{X} ^\prime _{m \times d}$,

    $$
    \boldsymbol{Z} _{x ^\prime} ^\top = \boldsymbol{A} ^\top \left[\begin{array}{ccc}
    k(\boldsymbol{x} _1, \boldsymbol{x ^\prime_1}) & \ldots  &k(\boldsymbol{x} _1, \boldsymbol{x ^\prime_m}) \\
    k(\boldsymbol{x} _2, \boldsymbol{x ^\prime_1}) & \ldots  &k(\boldsymbol{x} _2, \boldsymbol{x ^\prime_m}) \\
    \vdots &&\vdots \\
    k(\boldsymbol{x} _n, \boldsymbol{x ^\prime_1}) & \ldots  &k(\boldsymbol{x} _n, \boldsymbol{x ^\prime_m}) \\
    \end{array}\right]\\
    $$

### Model Selection

Hyperparameters/settings include number of components $k$, choice of kernel, and the regularization coefficient $r$.
