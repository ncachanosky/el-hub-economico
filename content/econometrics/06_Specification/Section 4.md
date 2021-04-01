---
# Title, summary, and page position.
linktitle: "The Ramsey RESET Test"
weight: 4

# Page metadata.
title: The Ramsey RESET Test
type: book  # Do not modify.
---



---

## What is the Ramsey RESET Test

The [Ramsey's Regression Specification Error Test (RESET)](https://en.wikipedia.org/wiki/Ramsey_RESET_test) evaluates the **likelihood** that a model suffers from some type of specification error.

The test cannot identify the type of the specification error, it can only point to the likelihood a specification problem is present.

---

## Building the Ramsey RESET Test

The test evaluates if non-linear combinations of $\hat{y}$ carry any explanatory power over $y$. If that is the case, then it is likely that the model has a specification problem. Intuitively, if non-linear combination of $\hat{y}$ have explanator power over $y$, then it is likely that the functional form should be revised to include one ore more polynomial terms.

Ramsey's test follows the following steps:

**First**. Estimate your original model and save $\hat{y}$.

* $\hat{y} = \hat{\beta}_0 + \hat{\beta}_1 x_1 + ... + \hat{\beta}_K x_K$

**Second**. Run your original model with powered values of $\hat{y}$. In principles you can add as many powered terms as you want, the convention is to use a polynomial of degree 4.

* $\tilde{y} = \hat{\alpha}_0 + \hat{\alpha}_1 x_1 + ... + \hat{\alpha}_K x_K + \hat{\gamma}_1 \hat{y}^2 + \hat{\gamma}_2 \hat{y}^3 + \hat{\gamma}_3 \hat{y}^3$

**Third**. Run an $F$-test for $\hat{\gamma}_1, ..., \hat{\gamma}_3$. 

If the $F$-test finds that powered terms of $\hat{y}$ are jointly significant, then the Ramsey RESET test points to a possible specification problem with the original model.

Ramsey RESET test's intuition is easier to see with matrix notation: $\hat{y} = X\hat{\beta}$. Then:

$$
\begin{aligned}
\hat{y}^2 = (X\hat{\beta})^2 \\\\[10pt]
\hat{y}^3 = (X\hat{\beta})^3 \\\\[10pt]
\hat{y}^4 = (X\hat{\beta})^4
\end{aligned}
$$

By adding powered terms of $\hat{y}$, you are indirectly testing for **the possibility** of having omitted a powered value of one or more of your regressors (the columns inside the matrix $X$).