---
# Title, summary, and page position.
linktitle: "The Gauss-Markov theorem"
weight: 4

# Page metadata.
title: The Gauss-Markov theorem
type: book  # Do not modify.
---



---

## The Gauss-Markov theorem

The [Gauss-Markov Theorem](https://en.wikipedia.org/wiki/Gauss%E2%80%93Markov_theorem#Remarks_on_the_proof) formally proves important conditions of OLS coefficient estimation. The exact nature of these conditions depend on whether **assumptions 1 to 6** or **assumptions 1 to 7** are met.

### BLUE coefficients

If **assumptions 1 to 6** hold (everything except the normal distribution of the errors), then the estimated $betas$ are the **B**est **L**inear **U**nbiased **E**stimator (BLUE). They key word in BLUE is *best*, which means that the variance of the estimated $betas$ is the minimum possible. Any linear estimation method other than OLS will produce $betas$ with a similar or larger variance.

Let $\hat{\beta}$ denote the OLS estimation and $\tilde{\beta}$ denote an alternative (not OLS) estimation. Then, if assumptions 1 to 6 hold, the Gauss-Markov theorem states that OLS coefficients are (see proofs in the appendix):

| Condition  | Mathematical expression  |
|------------|--------------------------|
| Unbiased   | $E[\hat{\beta}] = \beta$ |
| Efficient  | $\sigma^2_{\hat{\beta}} \leq \sigma^2_{\tilde{\beta}}$ |
| Consistent | $\lim\limits_{N \to \infty} V[\hat{\beta}] \to plim (\hat{\beta}) \to \beta$ |

You are already familiar with the concepts of **unbiased** and **efficient** estimator from the previous section. Here we introduce a new concept, that of **consistency**, which states that as the sample size increases the probability of your estimation converging to the true value converges to one. This occurs because the variance of your estimation converges to zero around the true value under estimation.

The Gauss-Markov theorem shows in more detail the significance of the classical model assumptions. As long as your data conforms with these assumptions, your OLS estimation will be the best among all possible linear estimations and will be consistent (it improves in precision the larger the dataset is).

There are two important issues to keep in mind:
1. The Gauss-Markov theorem **is not** saying that your estimation is a *good* one, the theorem is saying that if the classical model conditions hold, your estimation is the *best among all linear estimations* as good or bad as it may be
2. The Gauss-Markov theorem **does not** need the errors to have a normal distribution.

### BUE Coefficients

If **the errors have a normal distribution** (assumption 7), then the OLS estimation is not just BLUE, it is also the **B**est **U**nbiased **Estimator** (BUE). Now your OLS coefficients are the best among all linear and non-linear estimation.

If errors are normally distributed, then the Gauss-Markov theorem implies that:

| Condition  | Mathematical expression  |
|------------|--------------------------|
| Unbiased   | $E[\hat{\beta}] = \beta$ |
| Efficient  | $\sigma^2_{\hat{\beta}} \leq \sigma^2_{\tilde{\beta}}$ |
| Consistent | $\lim\limits_{N \to \infty} V[\hat{\beta}] \to plim (\hat{\beta}) \to \beta$ |
| Coefficients are normally distributed | $\hat{\beta} \sim N\left(\beta, V(\hat{\beta})\right)$ |

Condition 4 states that if errors have a normal distribution, then the distribution of your estimated coefficients is also normal. This is very important for hypothesis testing (next chapter).

---

## Appendix

### Proof of unbiasedness

Let $\tilde{\beta} = By$ represent **any** linear estimation. The multiplication of matrix $B$ times the vector $y$ produces the vector $\tilde{\beta}$ of linear estimators.

In the case of OLS, $B = \left( X'X \right)^{-1} X'$.

Let $D = B - \left(X'X \right)^{-1} X'$ denote any deviation from the OLS estimation. For any method other than OLS $D \neq0$.

We can now apply the expectation operator to $\tilde{\beta}$.

$$
\begin{aligned}
E[\tilde{\beta}] =& E[By] \\\\[10pt]
E[\tilde{\beta}] =& E[B(X \beta + \varepsilon)] \\\\[10pt]
E[\tilde{\beta}] =& BX \beta + B \underbrace{E[\varepsilon]}_{0} \\\\[10pt]
E[\tilde{\beta}] =& BX \beta
\end{aligned}
$$

You can see that $E[\tilde{\beta}] = \beta \iff BX = I$.

In the case of OLS estimation:

$$
\begin{aligned}
E[\hat{\beta}] =& \underbrace{\left( X'X \right)^{-1} X'}_{B} X \beta \\\\[10pt]
E[\hat{\beta}] =& I \beta \\\\[10pt]
E[\hat{\beta}] =& \beta
\end{aligned}
$$

However, if $BX \neq I \to E[\tilde{\beta}] \neq \beta$

$$
\begin{aligned}
E[\tilde{\beta}] =& \left( (X'X )^{-1} X' + D \right) X \beta \\\\[10pt]
E[\tilde{\beta}] =& (X'X)^{-1} (X'X) \beta + DX \beta \\\\[10pt]
E[\tilde{\beta}] =& \beta + \underbrace{DX \beta}\_{\xi} \\\\[10pt]
E[\tilde{\beta}] \neq& \beta
\end{aligned}
$$

The above excercise means that the condition for the coefficient to be unbiased is that the deviation from the OLS estimation $(D)$ multiplied with your data $(X)$ is zero ($D$ and $X$ are orthogonal).

### Proof of efficiency

Let $\tilde{\beta}$ be an unbiased non-OLS estimation. Because $\tilde{\beta}$ is unbiased $DX=X'D'=0$.

$$
\begin{aligned}
\tilde{\beta} =& \beta + \left[ (X'X)^{-1} X' + D \right]\varepsilon \\\\[10pt]
V[\tilde{\beta}] =& \left[(X'X)^{-1} + D \right] \sigma^{2}\_{\varepsilon} \left[(X'X)^{-1} X' + D \right]' \\\\[10pt]
V[\tilde{\beta}] =& \left[(X'X)^{-1} (X'X) (X'X)^{-1} + (X'X)^{-1} X'D' + DX (X'X)^{-1} + DD'\right] \sigma^{2}\_{\varepsilon} \\\\[10pt]
V[\tilde{\beta}] =& \left[(X'X)^{-1} +DD' \right] \sigma^{2}\_{\varepsilon} > V[\hat{\beta}]
\end{aligned}
$$

Because $DD'$ is [positive-semi-definite](https://en.wikipedia.org/wiki/Definite_symmetric_matrix) ($psd$)[^1], $V[\tilde{\beta}] > V[\hat{\beta}]$. This result shows that **even if** $\tilde{\beta}$ is unbiased, it is still less efficient than the OLS estimation.

### Proof of consistency

Let $\hat{\beta}$ be the OLS estimation. We need to show that as the sample size increases, (1) $V[\hat{\beta}]$ converges to zero and (2) that $\hat{\beta}$ converges to $\beta$ (the true value).

Let's start with the variance of $\hat{\beta}$. We are going to multiply and divide the variance by $N$ and apply the limit operator.

$$
\begin{aligned}
V[\hat{\beta}] =& \sigma^{2}\_{\varepsilon} (X'X)^{-1} \\\\[10pt]
V[\hat{\beta}] =& \sigma^{2}\_{\varepsilon} \frac{1}{N} \left(\frac{1}{N} X'X \right)^{-1} \\\\[10pt]
\lim\limits_{N \to \infty} V[\hat{\beta}] =& \sigma^{2}\_{\varepsilon} \cdot 0 \cdot \lim\limits_{N \to \infty} \left(\frac{1}{N} X'X \right)^{-1} \\\\[10pt]
\lim\limits_{N \to \infty} V[\hat{\beta}] \to& 0
\end{aligned}
$$

This condition holds because, according to the classical assumptions, $\left(\frac{1}{N} X'X \right)^{-1}$ is finite.

We can proceed to check the second condition, that $\hat{\beta} \to \beta$ as $N \to \infty$. We can also proceed by multiplying and dividing by the sample size $(N)$ and apply the limit operator. Recall that under the classical model assumption $\rho(X' \varepsilon) = 0$.

$$
\begin{aligned}
\hat{\beta} =& \beta + (X'X)^{-1} X' \varepsilon \\\\[10pt]
\hat{\beta} =& \beta + \left(\frac{1}{N} X'X \right)^{-1} \frac{1}{N} X' \varepsilon \\\\[10pt]
\lim\limits_{N \to \infty} \hat{\beta} =& \beta + \left(\lim\limits_{N \to \infty} \frac{1}{N} X'X \right)^{-1} \cdot \lim\limits_{N \to \infty} E[X' \varepsilon] \\\\[10pt]
\lim\limits_{N \to \infty} \hat{\beta} =& \beta + \left(\lim\limits_{N \to \infty} \frac{1}{N} X'X \right)^{-1} \cdot 0\\\\[10pt]
\lim\limits_{N \to \infty} \hat{\beta} \to& \beta
\end{aligned}
$$

This second result complements the first one. As the variance of the estimation approaches zero, the value of the estimation approaches the true value under estimation.

<!-- FOOTNOTES -->
[^1]: A symmetric matrix $M$ is positive definite if $v'Mv$ produces a strictly positive scalar (where $v$ is a vector). A matrix $M$ is positive-semi-definite if $v'Mv$ produces a non-negative scalar (zero or positive). Matrix $M$ would be negative-definite or negative-semi-definite under the opposite conditions.
