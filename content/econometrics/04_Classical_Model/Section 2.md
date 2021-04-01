---
# Title, summary, and page position.
linktitle: "The Classical Model assumptions"
weight: 2

# Page metadata.
title: The Classical Model assumptions
type: book  # Do not modify.
---



---

## The Classical Model assumptions

### Assumption 1: The model is linear

This assumption requires the model to be **linear** and, of course, be correctly specified (are you forgetting any important regressors?) However, we need to be careful with what we mean by **linear** in this context.

The following is a typical linear model with an additive error term:

$$
y_i = \beta_0 + \beta_1 x_{1,i} + ... + \beta_K x_{K,i} + \varepsilon_i
$$

The expression **linear model** can be confusing. We tend to think in *math terms*, where a linear equation is one with **linear variables**, that is, elevated to the power 1: $y = a + b_1 x_1 + b_2 x_2 + b_3 x_3$.

However, the classical assumption requires the model to be linear on the **coefficients**. As long as there are independent additive terms with linear coefficients, then the model is linear. Remember that what we are estimating is the $betas$, no the regressors.

Consider two examples of a linear model with non-linear regressors. Let the first one have squared regressors $(w_i^2)$ and the second one have logarithmic regressors $(ln(w_i))$ regressors. These two examples are easy to linearize, just define $x_i = w_i^2$ in the first model and $x_i = ln(w_i)$ in the second model. Then:

$$
\begin{aligned}
y =& \beta_0 + \beta_1 \underbrace{z_1^2}\_{x_1} + ... + \beta_k \underbrace{x_K^2}\_{x_K} + \varepsilon \\\\[10pt]
y =& \beta_0 + \beta_1 \underbrace{ln(z_1)}\_{x_1} + ... + \beta_k \underbrace{ln(z_K)}\_{x_k} + \varepsilon
\end{aligned}
$$

*Econometrically speaking*, both models are identical in the sense that both are linear and with the same number of regressors. Of course, since we are looking at different data the estimated $betas$ will differ. Yet, both models are identical in the sense of how $betas$ are estimated.

Consider now a non-linear **theory** that can be linearized before running your regression. For instance, your theory may be represented by the following equation:

$$
y = e^{\beta_0} x_1^{\beta_1} ... x_k^{\beta_k} e^{\varepsilon}
$$

You can easily linearize this model by applying logs (where $y^* = ln(y)$):

$$
\begin{align}
ln(y_i) =& \beta_0 + \beta_1 x_{1,i} + ... + \beta_K x_{K,i} + \varepsilon_i \\\\[10pt]
y^*_i =& \beta_0 + \beta_1 x_{1,i} + ... + \beta_K x_{K,i} + \varepsilon_i
\end{align}
$$

In general terms, a model linear in the coefficients has the following functional form:

$$
f(y) = \beta_0 + \beta_1 f(x_1) + ... + \beta_K f(x_K) + \varepsilon
$$

An example of a model non-linear in the coefficients would be $y = \beta_0 + x_1^{\beta_1} + ... + x_k^{\beta_K}$. There is no algebraic arrangement that would make this equation linear on the $betas$.

There are two other important conditions in this assumption:

1. The model is correctly specified, meaning there is no **omitted variables**
2. The error term is additive to the model and cannot be multiplied by or divided by any other regressor(s) included in the model

{{% callout note %}}
**Assumption 1** requires that:
1. Your econometric model can be represented as a model linear *on the coefficients*, even if the regressors do not have a linear behavior or if the underlying theory is not linear: $f(y) = \beta_0 + \beta_1 f(x_1) + ... + \beta_K f(x_K) + \varepsilon$
2. All important regressors are included in the model
3. The error can be represented as an additive term independent of all regressors
{{% /callout %}}

### Assumption 2: The error term has zero population mean

The error term, which has a random or stochastic behavior, captures variations of the dependent variable unexplained by the regressors. Each observation has its own error term. Assumption 2 requires the mean of the errors to be zero (where $E[\cdot]$ denotes the expected value):

$$
E[\varepsilon] = 0
$$

The intuition behind this assumption is that random errors should cancel out. The following figure depicts the distribution of an hypothetical error term. You can see that the mean is zero with <span style="color:red">negative</span> and <span style="color:blue">positive</span> errors. You can also see that the majority of the errors are small (close to zero) and only a few errors are large (far away from zero). Importantly, even though the error term in the figure looks like it has a normal distribution, **Assumption 2 does not require errors to have a normal distribution**, only to have a zero mean value. However, a normal distribution of the errors is a desirable condition (wait until Assumption 7).

{{< figure library="true" src="econometrics/04_Classical_Model/Fig_01.png" >}}

To be more precise, assumption 2 builds over an asymptotic condition. In a small sample, it is possible that the mean of the error term is not exactly equal to zero. What is required is that the mean of the error term converges to zero as the sample size increases to infinity $(n \rightarrow \infty \therefore E[\varepsilon] \rightarrow 0)$

Assumption 2 is another reason to include a constant term in your model. Assume the mean of the error term has a non-zero value (positive or negative) of $\xi \neq 0$. Then you can re-write your model in the following way:

$$
\begin{aligned}
y_i =& \left(\beta_0 - \xi \right) + \beta_1 x_{1,i} + ... + \beta_K x_{k,i} + \left(\varepsilon_i + \xi \right) \\\\[10pt]
y_i =& \beta^*_0 + + \beta_1 x_{1,i} + ... + \beta_K x_{k,i} + \varepsilon^*_i
\end{aligned}
$$

where $\beta^\*\_0 = \beta_0 - \xi$ and $\varepsilon^\*\_i = \varepsilon_i + \xi$.

Therefore, your model will fulfill assumption 2 as long as it has a constant term. In other words, the constant term will move up or down as necessary to guarantee that $E[\varepsilon]=0$.

{{% callout note %}}
**Assumption 2** requires that:
1. The mean of the error term is zero: $E[\varepsilon]=0$
2. No requirement is made on the standard deviation $(\sigma)$ or type of distribution of error term
{{% /callout %}}

### Assumption 3: All regressors are uncorrelated with the error term

Let $\rho$ denote correlation, then:

$$
\rho(x_j, e) = 0 \\;\\;\\;\\; \forall j = 1, ..., K
$$

If this condition is violated, then the estimation of the coefficients of the regressors included in the model may be biased. This bias occurs because every omitted variable is part of the error term. Assume you forget to include regressor $z_i$ in your model. If the pure error term is $\varepsilon$, then the error term of your model becomes $\varepsilon^* = \varepsilon + \gamma z_i$.

$$
\begin{aligned}
y_i = \beta_0 + \beta_1 x_{1,i} + ... + \beta_K x_{K,i} + \underbrace{\left(\varepsilon_i + \gamma z_i \right)}_{\varepsilon^*} 
\end{aligned}
$$

If $\gamma \neq 0$, then you have omitted a significant variable (otherwise, if $\gamma = 0$, then $\gamma z_i = 0$). Omitting $z$ can lead to a miscalculation of the other regressors. If $\rho(x_j,z) \neq 0$ for any $j$, then $\rho (x_j, \varepsilon^*) \neq 0$.

If any of the regressor is correlated with $z$ (a likely situation in economics), then assumption 3 will be violated. Even if $\rho (x_j, \varepsilon^*) = 0$, it is still the case that in your model $\rho (x_j, \varepsilon) \neq 0$ because $\varepsilon$ includes $z$, which is correlated with one ore more of your regressors.

If $\rho (x_1, z) > 0$, then you should expect for $\hat{\beta_1}$ to capture not only the effect of $x_1$ on $y$, but also some of the effect of $z$ on $y$. Therefore your model will have an *upward* (or positive) bias when estimating $\hat{\beta_1}$. If $\rho (x_1, z) < 0$, then the situation is the opposite.

It is possible, but unlikely, that $\gamma > 0 \wedge \rho (x_j, z) = 0 \; \forall j = 1, ..., K$. In this hypothetical case, omitting a significant variable has no effect on the estimation of the other regressor's coefficients.

Another situation likely to violate assumption 3 is when your model has an independent variable with a simultaneous relationship with at least one regressor. This means that there is a two-direction causal effect between $y$ and $x_j$. This is the problem of **endogeneity**. The regression requires that the causal effects goes from $x \to y$. But, if the relationship is mutual $(x \leftrightarrow y)$, then your model suffers from endogeneity and coefficient estimation will be biased. This **system of equations** requires a joint estimation rather than independent models. We will cover this issue at a later chapter.

{{% callout note %}}
**Assumption 3** requires that:
1. All regressors are uncorrelated with the error term: $\rho (x_i, \varepsilon) = 0 \\;\\;\\;\\; \forall j = 1, ..., K$  
---
This assumption is usually violated in two situations:
   * You omit a significant variable, which is correlated with at least one regressor included in the model
   * Your model has a bi-directional causal effect (endogeneity) between the independent variable and at least one of the regressors
{{% /callout %}}

### Assumption 4: Observations of the error term are uncorrelated with each other (no serial correlation)

Your model should be free of **serial correlation**. This means that errors are uncorrelated with each other: $\rho(\varepsilon_i, \varepsilon_j) = 0 \\; \\; \\; \\; \forall i \neq j$.

In **cross-section** data this means that the observation error of the United States has no effect on the observation error of any other country. Since in cross-section data there is no order of data that must be followed, it can be difficult to spot serial correlation (for instance, it does not matter if you order your country-level observations alphabetically or randomly). A positive (negative) error in any given observation should have no effect on whether any other observation has a positive (negative) error.

Serial correlation is a more intuitive concept in the case of **time-series**. In this case, assumption 4 requires that the error in period $t$ has no effect on future period errors. For instance, an unexpected monetary shock (or natural disaster) in year $t$ should have no effect on the errors in the following years. A positive (negative) error in observation $t$ should have no effect on whether the errors of future observations are positive (negative).

This assumption is important because if errors are serially correlated, then the standard deviation of the $betas$ can be inflated, leading to inefficient coefficient estimations. The assumption of no serial correlation builds on the idea that errors are $iid$, independently and identically distributed. Each observation is an independent random draw from the same probability distribution.

Serial correlation is particularly important in the case of time-series data. In this context, serial correlation can lead to biased estimations of the coefficients, and not only to an inefficient estimation of the coefficients.

{{% callout note %}}
**Assumption 4** requires that:
1. Observations of the error term are uncorrleated: $\rho(\varepsilon_i, \varepsilon_j) = 0 \\;\\;\\;\\; \forall i \neq j $  
{{% /callout %}}

### Assumption 5: The error term has a constant variance (homoskedasticity)

If the standard deviation $(\sigma)$ of the errors is constant across the sample, then the errors are **homoskedastic**. If, on the contrary, the standard deviation of the errors is not constant across the sample, then the errors are **heteroskedastic**.

For instance, it is very likely you will have heteroskedasticity if you are looking at income levels from countries around the world. Some countries have low income and other countries have high income. Therefore, it is to be expected that the errors of the former will be smaller than the errors of the latter.

If the errors are heteroskedastic, then the $\sigma$ of each observation will be different. If the standard deviation of the errors is constant, then there is no need to use the observation subscriot (such as $i$) because the value of $\sigma_\varepsilon$ is the same for all errors:

$$
\sigma_{\varepsilon,i} = \sigma_\varepsilon \; (\text{or} \; \bar{\sigma_\varepsilon})
$$

If the errors are heteroskedastic, then the standard deviation of the estimated $betas$ will be inflated. That is, your model will produce an inefficient estimation of the coefficients.

{{% callout note %}}
**Assumption 5** requires that:
1. The variance of the errors is constant: $\sigma (\varepsilon_i) = \bar{\sigma}_\varepsilon$  
{{% /callout %}}

### Assumption 6: No explanatory variable is a perfect linear combination of other explanatory variable(s) (multicollinearity)

The idea behind assumption 6 is that each regressor should have information that is independent of the information included in other regressors. Once again, remember than an econometric model is explaining *variations* of $y$ with *variations* of $x_i$. 

Two regressors are perfectly **collinear** if their behavior looks exactly the same, even if they have different absolute values. For instance, you include two regressors for income, one in hundreds and other one in thousands. These two regressors have different levels even if the carry the exact same information. There is no point in including these two regressors, one is enough because there is nothing new the second regressor will add to the model.

An intuitive examples of collinearity is when one regressor is a multiple of another regressor or equals another regressor plus a constant.

1. $x_1 = \omega x_2 \\; (\omega \neq 0)$
2. $x_1 = x_2 \pm c \\;(c \neq 0)$

**Multicollinearity** is collinearity with more than one regressor. The classical assumption is violated if you can perfectly write any regressor as linear combination of other regressors.

$$
x_K = \omega_1 x_1 + ... + \omega_{K-1} x_{K-1}
$$

If this situation happens, OLS **cannot** estimate the coefficients of the model. This is because the inverse of $(X'X)^{-1}$ does not exist. 

{{% callout note %}}
**Assumption 6** requires that:
1. No regressor is a **perfect** linear combination of any other regressor(s): $\nexists \\; \omega_j \\; \text{s.t.} \\; x_i = \sum_{j} \omega_j x_j \\; \forall j \neq i$
{{% /callout %}}

### Assumption 7: The error term is normally distributed

Assumption 2 states the error term should have a zero mean, and assumption 5 states that the standard deviation of the errors is constant. There is no requirement, however, that the error terms must have a [**normal** distribution](https://en.wikipedia.org/wiki/Normal_distribution). Assumption 7 requires the errors to have a normal distribution: $\varepsilon \sim N(0, \sigma_{\varepsilon})$

It is important to be careful about the normality distribution of the errors:

1. OLS estimation **does not need** the errors to have a normal distribution
2. Errors normality is important for hypothesis testing (next chapter), not for OLS coefficient estimation

To be precise, assumption 7 is **not needed** to run an efficient OLS regression. However, it is very convenient when moving from regression estimation to hypothesis testing. If errors are not normally distributed, then the typical strategy of hypothesis testing is invalid (specially if working with small samples).

{{% callout note %}}
**Assumption 7** requires that:
1. Errors have a normal distribution: $\varepsilon \sim N(0, \sigma_{\varepsilon})$
---
This assumption usually holds when:
   * Errors are random
   * You have a large sample size $(N \rightarrow \infty)$
{{% /callout %}}

---

## Summary

The following table summarizes the seven assumptions of the classical model.

| Assumption # | Description | Mathematical condition |
|--------------|-------------|------------------------|
| Assumption 1 | The model is linear | $f(y) = \beta_0 + \beta_1 f(x_1) + ... + \beta_K f(x_K)$ |
| Assumption 2 | The error has a zero mean | $E[\varepsilon] = 0$ |
| Assumption 3 | Regressors and errors are uncorreleated | $\rho(x, \varepsilon) = 0$|
| Assumption 4 | No serial correlation | $\rho(\varepsilon_i, \varepsilon_j) = 0 \; \forall i \neq j$|
| Assumption 5 | Errors are homoskedastic | $\sigma_{\varepsilon, i} = \bar{\sigma_{\varepsilon}}$ |
| Assumption 6 | No multicollinearity | $\nexists \\; \omega_j \\; \text{s.t.} \\; x_i = \sum_{j} \omega_j x_j \\; \forall j \neq i$|
| Assumption 7 | Errors have a normal distribution | $\varepsilon \sim N(0, \bar{\sigma_{\varepsilon}})$ |