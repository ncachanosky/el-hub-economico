---
# Title, summary, and page position.
linktitle: "The F-test"
weight: 3

# Page metadata.
title: The F-test
type: book  # Do not modify.
---



---

## What does the $F$-test do?

The $t$-test is a single significance test in the sense that evaluates the statistical significance of one coefficient only. You can evaluate all the coefficients in your model, but you have to do so one at a time.

The $F$-test is a **joint** significance test. In this case the test considers if two or more coefficients are statistically significantly together, rather than individually.

Consider two examples where an $F$-test would be particularly useful. The first one is the case where the $t$-test for all your regressors fail to reject the null hypothesis that they are zero, but happens to be that all coefficients together (jointly) are significant. In some situations is is possible to have no significance in any coefficient while having joint significance. 

The second example is when you have an hypothesis that involves more than one regressor. If you evaluating if there is any seasonality (such as quarterly) effect on a variable, then you need to jointly evaluate the coefficients for each seasonality included in the model. Looking at individual $t$-stats is not sufficient.

---

## Building the $F$-test

### The $F$ distribution

The $F$-statistic is the test-statistic of the $F$-test. If certain conditions hold, the $F$-statistic has the convenient [$F$-distribution](https://en.wikipedia.org/wiki/F-distribution) $(\chi^2)$.

The $F$-distribution typically arises when analyzing variances. More precisely, the $F$-distribution is the result of dividing two [Chi-square](https://en.wikipedia.org/wiki/Chi-square_distribution) distributions divided by their respective degrees of freedom.

A $\chi^2_n$ with $n$ degrees of freedom is the sum of $n$ squared standard normal distributions. Let $Z_i, ..., Z_n$ be $n$ standard normal distributions, then:

$$
\chi^2_n = Z_1^2 + ... + Z_n^2 = \sum_{i=1}^{n} Z_i^2 
$$

Then, the following variable $F$ has an $F$-distribution with $n_1$ and $n_2$ degrees of freedom:

$$
F = \frac{\chi^2_{n_1}/n_1}{\chi^2_{n_2}/n_2} \sim F_{n_1, n_2}
$$

Because the $F$-distribution is built with squared values, it can only take positive values. The shape of the $F$-distribution depends on both degrees of freedom.

The following `STAT` code plots a few $F$-distributions with different degrees of freedom.

```
*==============================================================================*
* HYPOTHESIS TESTING
* Create F-distributions
* Code sample: 4.3
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings
set scheme s1color  // Set plot scheme

*|CELL 2|----------------------------------------------------------------------*
*|Create required data
drop _all
set obs 201

gen   N = _n
label variable N "Observation"
tsset N

generate x = 0 in 1/201
replace  x = 10/200 + L.x in 2/201

*|CELL 3|----------------------------------------------------------------------*
*|Create F-distributions
gen F11  = Fden(  1,  1,x)
gen F21  = Fden(  2,  1,x)
gen F12  = Fden(  1,  2,x)
gen F42  = Fden(  4,  2,x)
gen F24  = Fden(  2,  4,x)
gen F10  = Fden( 10, 10,x)
gen F100 = Fden(100,100,x)

label variable F11  "F(1,1)"
label variable F21  "F(2,1)"
label variable F12  "F(1,2)"
label variable F42  "F(4,2)"
label variable F24  "F(2,4)"
label variable F10  "F(10,10)"
label variable F100 "F(100,100)"

*|CELL 4|----------------------------------------------------------------------*
*|Creat plot
line F11 F21 F12 F42 F24 F10 F100 x, ///
	 title("F-distribution (p.d.f.) with different degrees of freedom", ///
	       size(medsmall)) ///
	 legend(rows(1) size(small) region(lstyle(none))) ///
	 xlabel(,nolabels noticks) ylabel(,nolabels noticks)
```

{{< figure library="true" src="econometrics/05_Hypothesis_Testing/Fig_04.png" >}}

### The $F$-statistic

Assume we have a model with $K$ regressors.

$$
y = \beta_0 + \beta_1 x_1 + ... + \beta_K x_K + \varepsilon
$$

The $F$-test compares the $RSS$ of the unrestricted (full) model with the $RSS$ of the restricted model. The restricted model is the regression where you impose $q \leq K$ coefficients to be zero. The **null hypthesis** is that all $q$ restricted coefficients are equal to zero. The **alternative hypothesis** is that at least one coefficient is different than zero; even if the $F$-test cannot indicate which coefficient(s) is(are) different than zero.

Let's start assuming $q=K$. That is, all coefficients (excpet the constant) are assumed to be zero.

$$
\begin{align}
H_0&: \beta_1 = ... = \beta_K = 0 \\\\[10pt]
H_A&: \text{otherwise}
\end{align}
$$

Different versions of the $F$-test can be constructed where only selected coefficients are assumed to be zero. For instance, an $F$-test for coefficients 1, 4, and 5 will look the following way:

$$
\begin{align}
H_0&: \beta_1 = \beta_4 = \beta_5 = 0 \\\\[10pt]
H_A&: \text{otherwise}
\end{align}
$$

How can the **joint significance** be tested? To look at the statistical significance of more than one coefficient at the time, the $F$-test compares the $SSR$ of the unrestricted model with the $SSR$ of restricted. Because you are restricting the value of some coefficients, the $RSS$ of the restricted model $(r)$ is going to equal or larger than the $RSS$ of the unrestricted model $(u)$: $RSS_r \geq RSS_u$

Restricting coefficients to be equal to zero is the same as dropping those variables from the model. The difference between each $SSR$ is capturing the explanatory power of the variables when included in the model. The statistic question is of the difference between each $SSR$ is large enough.

In other words, as long as the coefficients are **jointly** significant, the $SSR$ of the unrestricted model should be significantly less than the $SSR$ of the restricted model.

The $F$-statistic is built following this logic. Assume you are testing if $M$ coefficients are equal to zero.

$$
F_{d_1, d_2} = \frac{(SSR_r - SSR_u)/q}{SSR_u/(N-K-1)} \sim F_{q, N-K-1}
$$

The numerator is taking the difference between the $SSr$ of each model, divided by the number of restrictions ($H_0$ assumes $q$ coefficients are equal to zero). The denominator uses $SSR_u$ as scaling factor of the difference between $SSR_r$ and $SSR_u$. The sample size $(N)$ is substracted the number of variables $(K)$ and the constant (which is the number $1$).

The reason this statistic has an $F$-distribution is because $SSR$ is the sum of squared residuals, which have a normal distribution. Therefore, $SSR$ has a $\chi^2$ distribution. As mentioned above, the ratio of two $\chi^2$ distribution divided by their respective degrees of freedom yields an $F$-distribution.

{{% callout warning %}}
**Condition for the $F$-test to have an $F$-distribution**

* The residuals must have a normal distribution with zero mean
* If the residuals do not have a normal distribution, then the $SSR$ does not have a $\chi^2$ distribution and therefore the $F$-statistic does not have an $F$-distribution
 
---

If the errors do not have a normal distribution, then the $F$-test **is invalid**
{{% /callout %}}

### The $R^2$ version of the F-test

The $F$-test has an equivalent $R^2$ representation. Using $R^2$ in an $F$-test has the advantage of dealing with numbers constrained between 0 and 1. $SSR$ can be a large number, producing computational issues in some terminals.

Since $SSR_u = TSS (1-R^2_u)$ (and likewise for the restricted model), the $F$-test becomes:

$$
\begin{align}
F(d_1, d_2) &= \frac{(SSR_r - SSR_u)/q}{SSR_u/(N-K-1)} \sim F_{q, N-K-1} \\\\[10pt]
F(d_1, d_2) &= \frac{(TSS(1-R^2_r) - TSS (1-R^2_u)/q}{TSS(1-R^2_u/(N-K-1)} \sim F_{q, N-K-1} \\\\[10pt]
F(d_1, d_2) &= \frac{TSS ((1-R^2_r) - (1-R^2_u))/q}{TSS(1-R^2_u)/(N-K-1)} \sim F_{q, N-K-1} \\\\[10pt]
F(d_1, d_2) &= \frac{(R^2_u - R^2_r)/q}{(1-R^2_u)/(N-K-1)} \sim F_{q, N-K-1}
\end{align}
$$

### Example

The following `STATA` code (1) replicates the $F$-test reported as part of a regression output and builds an $F$-test for three restrictions rather than restricting all variables' coefficients to be zero.

```
*==============================================================================*
* ORDINARLY LEAST SQUARES
* The F-test
* Code sample: 4.4
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and required data
ssc install estout, replace
set scheme s1color  // Set plot scheme
sysuse auto, clear  // Load 1978 Automobile Data from STATA


*|CELL 2|----------------------------------------------------------------------*
*|Replicate the F-test
global    regressors mpg weight length rep78 headroom trunk
summarize price $regressors

* Run the unrestricted model
quietly{
regress price $regressors
scalar N    = e(N)
scalar df1  = 6
scalar R1 = e(r2)

* Run the restricted model
regress price
scalar df2  = N - 6 - 1
scalar R2 = e(r2)

* Build and display the F-test
scalar F = ((R1-R2)/df1) / ((1-R1)/df2)
}

display "F(6, 62) = " F _newline "Prob > F = " Fden(df1, df2, F)


*|CELL 5|----------------------------------------------------------------------*
*|un F-test for three regressors

regress price mpg weight rep78
scalar df3 = 3
scalar R3  = e(r2)

scalar F = ((R1-R3)/df1) / ((1-R1)/df3)

display "F(6, 65) = " F _newline "Prob > F = " Fden(df1, df2, F)
```