---
# Title, summary, and page position.
linktitle: "Regressors"
weight: 1

# Page metadata.
title: Regressors
type: book  # Do not modify.
---



---

## Omitted variable bias

Remember, coefficients show the marginal the effect of their regressors assuming constant **only** the other regressors **included** in the model. Therefore, omitting a variable can produce some bias in the coefficients of the included regressors **if** the included and omitted regressors are correlated.

We can divide regressors in two groups

* Relevant regressors: Those with $\beta \neq 0$
* Irrelevant regressors: Those with $\beta = 0$

### Simple example

Consider the following example. There is a true model with two regressors, but your model only includes one of them:

1. True model: $y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \varepsilon$
2. Your model: $y = \beta_0^* + \beta_1^* x_1 + \varepsilon ^*$

All non-included regressors fall into the error term. Therefore, the error term of **your** model includes the pure classical error plus any omitted variable: $\varepsilon^* = \varepsilon + \beta_2 x_2$.

**Irrelevant** omitted variable have no effect on the error term because their coefficients are zero. However, if $\beta_2 \neq0$, then $E[\varepsilon^\*] = \beta_2 x_2 \neq0$.

If $x_1$ and $x_2$ are correlated, then $x_1$ will be correlated with $\varepsilon^\*$: $\rho(x_1, \varepsilon) \neq 0 \rightarrow \rho(x_1, x_2) \neq 0.$

### General case: Matrix algebra

Let $X$ and $\beta$ be the matrix and coefficient-vector of the included regressors (including the constant). Let $Z$ and $\gamma$ be the matrix and vector-coefficient of the omitted variables, and $\xi$ by the vector-bias of each $beta$ included in the model. Then:

$$
\begin{align}
\hat{\beta}^*    &= \beta + (X'X)^{-1} X' \varepsilon^* \\\\[10pt]
\hat{\beta}^*    &= \beta + (X'X)^{-1} X' (\varepsilon + Z\gamma) \\\\[10pt]
E[\hat{\beta}^*] &= E \left[ \beta + (X'X)^{-1} X' (\varepsilon + Z\gamma) \right] \\\\[10pt]
E[\hat{\beta}^*] &= \beta + (X'X)^{-1} \underbrace{E[X'\varepsilon]}\_{\text{0}} + \underbrace{E[(X'X)^{-1} X'Z \gamma]}\_{\xi} \\\\[10pt]
E[\hat{\beta}^*] &= \beta + \underbrace{(X'X)^{-1} X'Z}\_{P_{X,Z}} \gamma \\\\[10pt]
E[\hat{\beta}^*] &= \beta + \xi; \qquad (\xi = P_{X,Z}\cdot\gamma)
\end{align}
$$

Unless $\gamma=0$ (irrelevant variables) or $(X'Z)=0$ ("uncorrelation" between the included and omitted regressors), $\hat{\beta}$ will be biased. The bias of each $beta$ depends on the coefficients of the omitted variables $(\gamma)$ and on the interaction between the included and omitted variables.

Each column in $P_{X,Z}$ includes the OLS slope between each included and excluded regressor: $X_i  = \alpha_0 + p_{i,j} Z_j + u$.

> {{<icon name="file-excel" pack="fas" >}} {{% staticref "media/econometrics/06_Specification/Omitted variable bias.xlsx" %}}Download Excel sample file.{{% /staticref %}}

---

## Irrelevant variable inefficiency

An irrelevant variable has a coefficient of zero. The inclusion of irrelevant variables in the model is the converse problem of omitted variable bias. You are adding unnecessary regressors to the model. This **does not** bias your coefficients, but, it does make them **inefficient**. This is easy to see.

Assume the following (where $K_1, K_2$ are the number of regressors in $X_1$ and $X_2$):

1. True model: $y = \beta_0 + \beta_1 X_1 + \varepsilon$
2. Your model: $y = \beta_0^* + \beta_1^* X_1 + \beta_2^* X_2 + \varepsilon^*$

First, look at the **unbiasedness** of the OLS estimation

$$
\begin{aligned}
E\begin{bmatrix}
        \beta_1 \\\\
        \beta_2
 \end{bmatrix} &= 
 \begin{pmatrix}
        \beta_1 \\\\
        0
 \end{pmatrix} + 
\left(
    \begin{pmatrix}
    X_1 & X_2
 \end{pmatrix}'
 \begin{pmatrix} 
    X_1 & X_2
 \end{pmatrix}
 \right)^{-1}
 \begin{pmatrix} 
    X_1 & X_2
 \end{pmatrix}' E[\varepsilon] \\\\[10pt]
 E\begin{bmatrix}
        \beta_1 \\\\
        \beta_2
 \end{bmatrix} &= 
 \begin{pmatrix}
        \beta_1 \\\\
        0
 \end{pmatrix}
\end{aligned}
$$

Second, look at the **efficiency** of the OLS estimation. You can see that adding irrelevant variables *inflates* the estimated standard deviation of the coefficients.

$$
\begin{aligned}
S^2 = \frac{SSR}{N - K_1 - K_2} > \frac{SSR}{N - K_1}
\end{aligned}
$$