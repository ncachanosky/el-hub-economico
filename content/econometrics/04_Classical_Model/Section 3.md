---
# Title, summary, and page position.
linktitle: "Distribution of coefficient estimates"
weight: 3

# Page metadata.
title: Distribution of coefficient estimates
type: book  # Do not modify.
---



---

## Coefficients are random variables

Recall that a regression **estimates** a value of an unobserved/unknown **true** $beta$. $\hat{\beta}$ has a probability distribution because it is an estimation with a random component.

Every different sample taken from the same population will produce different values of $\hat{\beta}$. From all the potential different samples you can get, you get to work with only one. That is, from all the potential different values of $\hat{\beta}$ you can calculate, your regression will only give you one $beta$. Therefore, it is important to understand the $\hat{\beta}$ distribution.

A good sample and a good estimation technique will increase the likelihood that the $\hat{\beta}$ you estimate will be close to the true $\beta$. To understand how this works, we need to have a closer look at the OLS coefficient estimation.

Recall that (using matrix notation):

$$
\begin{aligned}
y =& X\beta + \varepsilon \\\\[10pt]
\text{and} \\\\[10pt]
\hat{\beta} =& \left( X'X \right) ^{-1} X'y
\end{aligned}
$$

Use now the first equation into the second one (where $I$ is the identity matrix):

$$
\begin{aligned}
\hat{\beta} =& \left( X'X \right)^{-1} \left(X'X \right) \beta + \left(X'X \right)^{-1} X \varepsilon \\\\[10pt]
\hat{\beta} =& I \beta + \left(X'X \right)^{-1} X \varepsilon \\\\[10pt]
\hat{\beta} =& \beta + \left(X'X \right)^{-1} X \varepsilon
\end{aligned}
$$

You can see that because $\varepsilon$ is a random variable, so is each $\hat{\beta_i}$. Therefore, each $\hat{\beta}_i$ has a mean and a standard deviation. Mean and deviation are related to the concept of unbiased and efficiency respectively. You can also see that your $betas$ have the same distribution than $\varepsilon$ (recall  classical model assumption 7).

---

## Unbiasedness and Efficiency

### Unbiasedness

An estimation is unbiased if its expected value coincides with the true value under estimation. You have a biased estimation when the expected value of the estimation diverges from the true value under estimation.

Consider the following example. The bullseye of a target represents the true value that your are trying to estimate. The darts you through are your econometric estimations. If your darts miss but fall around the target, your estimations are unbiased. If you average all your estimations you get the true value you are trying to estimate (errors cancel out). However, if your darts fall (in average) to either side of the target, then your estimation is biased. You tend to err more to one side such that if you average all your estimations you do not get the true value under estimation.

We can represent an unbiased and biased estimation in the following way:

1. Unbiased estimation: $E[\hat{\beta}] = \beta$
2. Biased estimation: $E[\hat{\beta}] = \beta + \xi, \\; \xi \neq 0$

You already know that your estimation will probably not be just on target. It is very unlikely you will get the **true** $beta$. But, you **do not want** your estimation to be biased. You are going to miss the bullseye, but you want to aim right be as close to your target as possible. Remember, in a regression you get to through only only one dart, you want to make it count.

If assumptions 1 to 6 of the classical model hold $(\rho(X,e)=0$ and $E[\varepsilon]=0)$, then OLS produces unbiased estimators.

$$
\begin{aligned}
\hat{\beta} =& \beta + \left(X'X \right)^{-1} X' \varepsilon \\\\[10pt]
E[\hat{\beta}] =& E \left[ \beta + \left(X'X \right)^{-1} X' \varepsilon \right] \\\\[10pt]
E[\hat{\beta}] =& \beta + \left(X'X \right)^{-1} X' \underbrace{E[\varepsilon]}\_{0} \\\\[10pt]
E[\hat{\beta}] =& \beta
\end{aligned}
$$

### Efficiency

Efficiency relates to how close or far from the **true** beta estimations fall, even if in average your estimations are unbiased. The lower (higher) the variance of an estimation, the more (less) estimations will be close to the **true** value under estimation. In our above throwing-darts example, the distance between the dart represent the standard deviation of your estimation technique.

Let's assume $\beta = 0$ and you have two sets of two estimations. The **first** set of estimations yields $(\hat{\beta}\_{1,1}, \hat{\beta}\_{1,2}) = (-1, 1)$. The second **set** of estimations yields $(\hat{\beta}\_{2,1}, \hat{\beta}_{2,2}) = (-2, 2)$. Both sets of estimations give, in average, the true $\beta$. However, the first set of estimations is better in the sense that the estimated values are closer to the true $\beta$ than those of the second set of estimations.

To evaluate the efficiency of the OLS estimation we need to apply the variance $(V)$ operator.

$$
\begin{aligned}
\hat{\beta} =& \beta + \left( X'X \right)^{-1} X' \varepsilon \\\\[10pt]
V[\hat{\beta}] =& V \left[\beta + \left( X'X \right)^{-1} X' \varepsilon \right] \\\\[10pt]
V[\hat{\beta}] =& \left( X'X \right)^{-1} X' \\; V[\varepsilon] \\; X \left( X'X \right)^{-1} \\\\[10pt]
V[\hat{\beta}] =& \left( X'X \right)^{-1} X' \left(I \sigma^2_{\varepsilon} \right) X \left( X'X \right)^{-1} \\\\[10pt]
V[\hat{\beta}] =& \sigma^2_{\varepsilon} \left( X'X \right)^{-1} \\\\[10pt]
\end{aligned}
$$

The efficiency of $\hat{\beta}$ depends not only on $\left(X'X\right)$, but also on the variance of the errors $(\sigma^2\_\varepsilon)$. The efficient estimation is the one that produces the lowest possible variance of your estimated $betas$.

### The coefficient distribution: Bias and efficiency plotted

If $\varepsilon \sim N(0, \sigma_{\varepsilon})$, then the coefficients have the following distribution.

$$
\begin{aligned}
\hat{\beta} &\sim N(\hat{\beta}, \sigma^2\_{\hat{\beta}}) \\\\[10pt]
\hat{\beta} &\sim N(\hat{\beta}, \sigma^2\_{\varepsilon} (X'X)^{-1})
\end{aligned}
$$

The following plot depicts different coefficient estimations (distributions). The <span style="color:blue">blue</span> line depicts the distribution of an unbiased and efficient estimation of $\beta$. You can see that the mean of this estimation coincides with the true $\beta$. The <span style="color:green">green</span> line depicts the distribution of an unbiased but inefficient estimation of $\beta$. You can see that, with respect to the <span style="color:blue">blue</span> estimation, is less likely that you will get the true $\beta$ and more likely that you will get an estimation farther away from the true value. Finally, the <span style="color:red">red</span> line depicts the distribution of estimation that is both biased and inefficient. It is biased because its expected value has a $\xi \neq 0$ deviation from the true $\beta$. It is inefficient because it has a larger variance than the <span style="color:blue">blue</span> estimation.

{{< figure library="true" src="econometrics/04_Classical_Model/Fig_02.png" >}}

---

## The estimated standard deviation of the coefficients

There is another issue that requires attention. The standard deviation of the coefficients depends on the error term. The error term, however, is unobservable. Therefore, the standard error of the coefficients is also unobservable. This situation means that such as we have a coefficient estimation, we also need a standard deviation of the coefficient estimation.

Because $e$ is an estimation of $\varepsilon$, it is tempting to think that $\hat{\sigma_{\hat{\beta}}} = \frac{1}{N} (e'e) (X'X)^{-1}$.

However, because the coefficients are estimated, this is not a good estimator of the standard deviation of the coefficients. Look at the difference between $e$ and $\varepsilon$.

$$
\begin{aligned}
e - \varepsilon &= (y - X\hat{\beta}) - (y - X\beta) \\\\[10pt]
e - \varepsilon &= X(\beta - \hat{\beta}) \\\\[10pt]
e &= \varepsilon + X(\beta - \hat{\beta})
\end{aligned}
$$

Because of the second term in the last line, the expected value of $e$ may or may equal the expected value of $\varepsilon$. There is no guarantee that the expected value of the second term is zero.

We need an unbias estimator of $V[\hat{\beta}]$. Before finding the estimation of the standard deviation of the coefficients is convenient to define the following matrices (where $P$ is known as the [**projection matrix**](https://en.wikipedia.org/wiki/Projection_matrix)).

$$
\begin{aligned}
P & \equiv X(X'X)^{-1}X' \\\\[10pt]
M & \equiv I - P = I - X(X'X)^{-1}X'
\end{aligned}
$$

$P$ and $M$ satisfy the following properties:

1. symmetric: $P' = P, M'= M$
2. idempotent: $P\cdot P = P, M\cdot M = M$
3. orthogonal: $PM = MP = 0$
4. $PX = X, MX = 0$

Then,

$$
\begin{aligned}
\hat{y} &= Py \\\\[10pt]
e &= My = M(X \beta + \varepsilon) = M\varepsilon
\end{aligned}
$$

Using $P$, $M$ and the [trace of a matrix](https://en.wikipedia.org/wiki/Trace_(linear_algebra)) we can get an unbias estimation of the variance of the estimated coefficients[^1]. The following develops an expression of $\sigma_{\varepsilon}^2$ as a function of $SSR$ (sum of squred residuals). Let $N$ be the sample size and $K$ the number of regressors (including the constant).

$$
\begin{aligned}
SSR &= e'e \\\\[10pt]
SSR &= y'My \\\\[10pt]
SSR &= \varepsilon' M \varepsilon \\\\[10pt]
SSR &= tr(\varepsilon' M \varepsilon) \\\\[10pt]
SSR &= tr(M \varepsilon' \varepsilon) \\\\[10pt]
SSR &= tr(M \sigma_{\varepsilon}^2 I) \\\\[10pt]
SSR &= \sigma_{\varepsilon}^2 tr(M) \\\\[10pt]
SSR &= \sigma_{\varepsilon}^2 tr[I - X(X'X)^{-1}X'] \\\\[10pt]
SSR &= \sigma_{\varepsilon}^2 tr[I - (X'X)^{-1}(X'X)] \\\\[10pt]
SSR &= \sigma_{\varepsilon}^2 tr(I_N - I_K) \\\\[10pt]
SSR &= \sigma_{\varepsilon}^2 \left( tr(I_N) - tr(I_K) \right) \\\\[10pt]
SSR &= \sigma_{\varepsilon}^2 (N-K) \\\\[10pt]
\end{aligned}
$$

Let $S^2 = \frac{1}{N-K} SSE$. Then $S^2$ is an unbiased estimator of $\sigma_{\varepsilon}^2$.

$$
\begin{aligned}
E[S^2] &= E[\frac{1}{N-K} SSE] \\\\[10pt]
E[S^2] &= \frac{1}{N-K} E[SSE] \\\\[10pt]
E[S^2] &= \frac{1}{N-K} \sigma_{\varepsilon}^2 (N-K) \\\\[10pt]
E[S^2] &= \sigma_{\varepsilon}^2
\end{aligned}
$$

<!-- FOOTNOTES -->
[^1]: The trace of a **square** matrix is the sum of the diagonal components. If $A$ is a $n \times n$ matrix, then $tr(A) = a_{1,1} + ... + a_{n,n} = \sum_i^n = a_{i,i}$. 

