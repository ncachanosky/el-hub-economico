---
# Title, summary, and page position.
linktitle: "The consequences of multicollinearity"
weight: 2

# Page metadata.
title: The consequences of multicollinearity
type: book  # Do not modify.
---



---

## Perfect multicollinearity: Impossible estimation

The consequence of perfect multicollinearity is the impossibility of estimating the coefficients of the model.

Recall that $\hat{\beta} = (X'X)^{-1} X'y$. If the model suffers from perfect multicollinearity (a perfect linear combination in the regressors), then the matrix $(X'X)$ is not full-rank. If the matrix is not full-rank then the inverse is undefined. And if the inverse of $(X'X)$ is undefined, then $\hat{\beta}$ cannot be estimated.

Some statistical software will drop a regressor in order to estimate the model. Other statistical software will produce an error message. Either way, the original model cannot is not calculated.

Because perfect multicollinearity is usually a matter of accidentally including the same information twice, this issue can be solved by dropping from the model the redundant(s) variable(s) without affecting the nature of the estimation. For instance, a model that includes distance both in `miles` and `kilometers` (perfect multicollinearity) is unaffected if either one of these regressors is dropped from the estimation.

---

## Imperfect multicollinearity: Inefficient estimation

Even though the estimation of a model with imperfect multicollinearity is possible, the **interpretation** of the coefficients is problematic.

It is important to emphasize that $\hat{y}$ **is not** biased. However, the coefficients are *noisy* in the sense that the model estimation cannot fully separate the effects of the regressors on $y$. The *ceteris paribus* condition is faulty. A coefficient captures the effect of one regressor on $y$ keeping the other ones constant. However, because of multicollinearity in the regressors, this is not fully possible. Assume $x_1$ and $x_2$ have some degree of collinearity. Then, it is possible that each regressor coefficient mistakenly captures some of the effect on $y$ of the **other** regressor. However, the whole model does not produce biased estimations of $y$.

What occurs is that the variance of the estimated coefficients gets inflated. Even though the estimated coefficients remain unbiased, they come from a much wider distribution. 

Assume for simplicity a simple model with two regressors, $y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \varepsilon$. Then,

$$
V[\hat{\beta}\_1] = \frac{\sigma^2\_{\varepsilon}}{\sum x\_1^2} \frac{1}{(1-R^2\_{1,2})}
$$

where $R^2_{1,2}$ is the $R^2$ if the regression of $x_2$ on $x_1$. If there is no multicollinearity, then $R^2_{1,2}=0$. If there is perfect multicollinearity, then $R^2_{1,2}=1$ and the variance of the estimated coefficient is $\infty$.

The second fraction is called the **variance inflation factor** (VIF). Each estimated coefficient has its own VIF. For any regressor $k = 1,...,K$:

$$
VIF_j = \frac{1}{1-\bar{R}^2_{j}} = \frac{1}{TOL}
$$

Where $R^2_{j}$ is the $R^2$ of regression of regressor $k$ with *all** other regressors in the original model and $TOL$ refers to *tolerance*.

The effects of imperfect multicollinearity can be summarized in the following list:

1. Estimated $betas$ remain unbiased
2. The overall fit of the model remains largely unaffected
3. The variance of the estimated $betas$ are inflated
   1. $t$-stats (p-values) well be biased down (up): The likelihood of a false negative (Type II error) will increase
   2. Coefficient estimation becomes *very* sensitive to *small* changes in data or when dropping a regressor from the model
   3. Coefficient estimation has large confidence intervals

---

## How problematic is multicollinearity

AS mentioned above, **perfect** multicollinearity is problematic because it violates assumption 6 in the classical model. Ideal conditions do not hold anymore, to the point where the model cannot be calculated.

However, the problems produced by **imperfect** multicollinearity are found to be ambiguous by most textbooks. There are a few reasons for this. In particular:

1. Classical assumptions are not violated
2. The estimation is unbiased

The classical model requires that there is not **perfect** multicollinearity, **imperfect** multicollinearity is not a violation of the classical model. In addition, model estimation remains unbiased, even if the estimation of the $betas$ is "imprecise" (inefficient).

Multicollinearity is more of an issue in two instances:

1. When trying to read the value of one specific coefficient
2. When doing $t$-stat significance evaluation of individual coefficients

Yet, multicollinearity is not much of an issue in terms of biases and overall fit of the model.

{{% callout warning %}}
**Imperfect** multicollinearity does not violate the assumptions (ideal conditions) of the classical model.
{{% /callout %}}