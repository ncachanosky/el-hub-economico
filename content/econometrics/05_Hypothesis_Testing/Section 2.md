---
# Title, summary, and page position.
linktitle: "The t-test"
weight: 2

# Page metadata.
title: The $t$-test
type: book  # Do not modify.
---



---

## What does the $t$-test do?

The $t$-test is a s typical test used to test the **null hypothesis** that a coefficient is different than zero. If this is the case, then the *marginal effect* of the corresponding regressors is different than zero and, therefore, said regressor has some explanatory power over the variations of the dependent variable. If the coefficient of a regressor were to be zero $(\beta = 0)$, then said regressor is unrelated with the dependent variable. Remember that in the context of econometrics *explanatory power* means that variations of $y$ can be explains, to some extent, by variations of $x$.

A coefficient different than zero can fall in any of the three following categories (number three is unlikely, but not impossible):

1. The regressor is economically significant
2. The regressor is economically insignificant
3. The regressor adds information, but not enough to compensate the loss of degrees of freedom (for instance, $\bar{R}^2$ decreases)

In its most common specification, the $t$-test null hypothesis is that a coefficient is different than zero regardless of the sign (two-tailed test). An alternative specification would be to test if a given coefficient is positive or negative (one-tailed test).

The plot below depicts the normal distribution (black) and the $t$-student distribution for selected degrees of freedom (shades of <span style="color:blue">blue</span>).

The following `STATA` code plots four $t$-student distributions with different degrees of freedom along a standard normal distribution

```
*==============================================================================*
* HYPOTHESIS TESTING
* Create t-Student distributions
* Code sample: 4.1
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
*|Create standard normal distriubtion and t-distributions
gen z = normalden(x)
label variable z "N(0,1)"

gen t1  = tden(1, x)
gen t5  = tden(5, x)
gen t10 = tden(10, x)
gen t20 = tden(20, x)

label variable t1  "t(df=1)"
label variable t5  "t(df=5)"
label variable t10 "t(df=10)"
label variable t20 "t(df=20)"

*|CELL 4|----------------------------------------------------------------------*
*|Create plot
line t1 t2 t5 t10 t20 z x, ///
	 title("N(0,1) and t-Student with different degrees of freedom", ///
	       size(medsmall)) ///
	 lcolor(red%10 red%30 red%50 red%60 red%90 black) ///
	 legend(rows(1) size(small) region(lstyle(none))) ///
	 xlabel(,nolabels noticks) ylabel(,nolabels noticks)

```

{{< figure library="true" src="econometrics/05_Hypothesis_Testing/Fig_02.png" >}}

---

## Building the t-test

### The Student's $t$-distribution

The **t-statistic** is the test-statistic of the $t$-test. If certain conditions hold, the t-statistic has the convenient [Student's t-distribution](https://en.wikipedia.org/wiki/Student%27s_t-distribution).

The t-distribution captures the probability distribution when estimating the mean of a normally-distributed population in the presence of (1) a sample size is small and (2) an unknown standard deviation. Visually, the t-distribution looks like a normal distribution with higher tails.

The exact shape of the t-student distribution depends on the degrees of freedom of your model. The larger the degrees of freedom, the more similar to the standard normal distribution the t-distribution looks like.

{{% callout warning %}}
**Condition for the $t$-test to have a Student's t-distribution**

* $\hat{\beta}$ must have a normal distribution
* For $\hat{\beta}$ to have a norma distirbution, the errors must have a normal distribution (see [The Sample Distribution of the beta](../04_Classical_Model/Section%203.md))
 
---

If the errors do not have a normal distribution, then the t-test **is invalid**
{{% /callout %}}

### The t-statistic

If your model has a constant and $K$ regressors, then you will have $K+1$ t-tests, one **independent** test for each coefficient including the constant term.

Let the null hypothesis be $\beta_j = 0$ $(j = 0, ..., K)$, $t_j$ be the t-statistic of each test, $t_C$ be the critical (threshold) value, and $DF$ be the degrees of freedom. Then:

$$
\begin{aligned}
H_0 :& \beta_j = 0 \\\\[10pt]
H_A :& \beta_j \neq 0 
\\\\[10pt]
t_j =& \frac{\hat{\beta}\_{j} - 0}{\hat{\sigma}\_{\hat{\beta}}} \sim t_{DF}
\end{aligned}
$$

If you look at the denominator, you will see that the t-statistic is built with the **estimation** of the standard deviation of the estimated coefficient.

As discussed in the previous section, there are two ways we can *solve* the hypothesis test:

* Compare each $t_j$ with $t_C$
  * $H_0$ is **rejected** if $|t_j| > |t_C$
  * The value of $t_C$ depends on (a) your chosen value of $\alpha$ (confidence level) and (b) the degrees of freedom in your test
* Compare the p-value of each $t_j$ with your chosen value of $\alpha$
  * $H_0$ is **rejected** if p-value $> \alpha$

It is important to be careful about the alternative outcome. If the conditions to **reject** $H_0$ are not met, then we **fail to reject** $H_0$. We **do not confirm** $H_0$.

{{% callout warning %}}
An hypothesis test either **rejects** or **fails to reject** the null hypothesis. Hypothesis testing **does not confirm** the null nor the alternative hypotheses.
{{% /callout %}}

### Example

Let's look again at our first regression.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 06.png" >}}

We can now make sense of the data to the right of **each** coefficient. From right to left, next to the value of each coefficient we have:

1. The standard error of the estimated coefficient
2. The $t$-statistic
3. The p-value of the $t$-statistic
4. The lower and upper limits of a 95% [confidence interval](https://en.wikipedia.org/wiki/Confidence_interval)

Let's now see the table that includes 5 regression models next to each other.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 07.png" >}}

In this case each coefficient has its estimated standard deviation below in parenthesis. However, there is no information about the $t$-statistic or p-value of each coefficent. Instead, there are asterisks (*). The asterisks provide the following information:

* Statistically different than zero at $\alpha = 10%$: *
* Statistically different than zero at $\alpha = 05%$: **
* Statistically different than zero at $\alpha = 01%$: ***

We can also plot the coefficients with their respective confidence intervals to see how far or close they are to the null hypothesis ($\beta_j = 0)$. For scaling purposes we drop the constant. Compare the figure below with the econometric results above.

```
*==============================================================================*
* HYPOTHESIS TESTING
* Plot coefficient intervals
* Code sample: 4.2
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and required data
ssc install coefplot, replace
set scheme s1color  // Set plot scheme
sysuse auto, clear  // Load 1978 Automobile Data from STATA


*|CELL 2|----------------------------------------------------------------------*
*|Run the model and plot coefficients

global    regressors mpg weight length rep78 headroom trunk
regress price $regressors

coefplot, ///
    xline(0, lcolor("green")) ///
    drop(_cons)

*==============================================================================*
*|THE END|=====================================================================*
*==============================================================================*
```

{{< figure library="true" src="econometrics/05_Hypothesis_Testing/Fig_03.png" >}}

---

## What to do with $t$-test results

What you do with the result of your $t$-tests depends on what you are trying to do with your model and your subjective interpretation of the results.

An intuitive reaction is to use the $t$-tests results to adjust your model to maximize $\bar{R}^2$ or the information criteria. Find the *best* model according to these goodness of fit measures. An alternative is to keep regressors to show that they are not statistically different than zero. An absence of *asterisks* is also information. In other words, it is not the same if you want just predictions or add empirical context to an economic theory.

Yet, not matter what your are looking for, remember to check that the errors have a normal distribution before reading the $t$-tests included in the regression output.

{{% callout note %}}
By default, most econometric software automatically provide $t$-test results. Those results **assume** that the errors have a normal distribution.

If the errors do not have a normal distribution, the $t$-test information provided by the software is invalid.
{{% /callout %}}