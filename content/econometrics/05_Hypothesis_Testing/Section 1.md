---
# Title, summary, and page position.
linktitle: "What is hypothesis testing"
weight: 1

# Page metadata.
title: What is hypothesis testing
type: book  # Do not modify.
---



---

## The structure and components of hypothesis testing

In econometrics, most [hypotheses tests](https://en.wikipedia.org/wiki/Statistical_hypothesis_testing) consist of a statistical method to estimate the likelihood that an assumed value is **different** from its real (true) value. In other words, an hypothesis test typically looks at the likelihood that a given estimation is **different** from an assumed value, rather than testing if a given estimation is **equal** to an assumed value.

A reason for this setting is that it is not possible to prove an hypothesis, but only to reject or falsify it with certain probability or likelihood. For instance, we cannot prove that a given $\beta$ is equal to zero, we can only show the likelihood that, being zero, we would get the estimated value in front of us.

A typical hypothesis test usually has four components:

1. The assumed value (the hypothesis)
2. The estimated value (such as a $\hat{\beta})$
3. The probability distribution of the estimation
4. A decision rule to decide whether the hypothesis is rejected

The hypothesis under evaluation is presented the following way. The **null hypothesis** $(H_0)$ is the assumption being tested. The **alternative assumption** $(H_A)$ captures all the alternative values the estimation can have.

It is important how you define the null and alternative hypothesis. The alternative hypothesis represents what you expect to find, but is the null hypothesis what you put under test.

Let $\hat{\phi}$ be the estimation of the unobserved value $\phi$.

**Example 1**

>You think the true value of $\phi$ is positive:
>
>1. $H_0: \phi \leq 0$
>2. $H_A: \phi > 0$
>
>You can see that the alternative hypothesis captures your *guess*, and that the null hypothesis plus the alternative hypothesis capture all potential values that $\phi$ can have. 
>
>The null and alternative hypothesis will look the opposite if you think the true value of $\phi$ is negative.

**Example 2**
>
>You think that the true value of $\phi$ is different than zero, but you don't have any particular insight about its sign.
>
>1. $H_0: \phi = 0$
>2. $H_A: \phi \neq 0$
>
>If you can, with some confidence, reject $H_0$, then it has to be the case that there is a likelihood that the true $\phi$ is different than zero.

We can now put together the general structure that most hypothesis testing follows one way or another.

The **first** component is the distance or deviation between the estimated value and the null hypothesis. Consider example 2. Even if it is the case that $\phi = 0$, it is very likely the estimated value will not be exactly zero.

The first component of an hypothesis test is: $\hat{\phi} - H_0$.

However, looking this difference is not enough to reach a decision., we need to decide if the difference between the estimated value and $H_0$ is **enough** to conclude that is unlikely that the true value of $\phi$ is actually zero.

The **second** component of an hypothesis test is a measure of variation of the estimated value. Assume the difference between the estimated value and $H_0$ is 10. This can be small if the standard deviation of $\hat{\phi}$ is 1,000 and it can be big if the standard deviation of $\hat{\phi}$ is 0.1.

The second component component of an hypothesis test is: $\sigma_{\hat{\phi}}$

This second component is used to scale the difference between $\hat{\phi}$ and $H_0$ to a meaningful measure, usually in the form of $\frac{Z}{S}$, where $Z$ is some measure of challenge to $H_0$ (for instance how different your observation is from your assumption) and $S$ is a scaling factor (such as the standard deviation of your estimation).

The **third** components (probability distribution of $\hat{\phi}$) is used along the **fourth** component (decision rule). The probability distribution is used to get the likelihood that $\hat{\phi} \neq H_0$. At which value of probability we decide that $H_0$ is rejected is the decision rule. We sill see this in more detail below and in the next two sections (*t*-test and F-test).

Components one to three are used to obtain a **test-statistic**. This number has a probability distribution that is used to decide (with a level of certainty), whether or not to reject $H_0$.

---

## Type I and Type II errors

Two things can happen when you do an hypothesis test to reject or not $H_0$. You can either get the **right** answer or you can get the **wrong** answer. However, there are two types of errors than can yield to a wrong outcome: [Type I error and Type II error](https://en.wikipedia.org/wiki/Type_I_and_type_II_errors)

* **Type I error** is the rejection of a true null hypothesis (false positive)
* **Type II error** is the failure to reject a false null hypothesis (false negative)

The issue is that it is not possible to minimized both types of errors simultaneously. Reducing the probability of having a Type I error increases the probability of having a Type II error (and the other way around).

It can be of importance which error you want to minimize. Assume a Jury must decide if a person accused of homicide is guilty or innocent. It is unlikely that the Jury will know with 100% certainty whether or not the accused is guilty or innocent. Therefore, the judicial procedure needs to decide if it is going to prioritize the error of (1) sending an innocent person to jail (Type I error: false positive) or (2) letting a guilty person free (Type II error: false negative). Because preference is given to let a guilty person walk over incarcerating an innocent person, a Jury typically must come to an unanimous decision **beyond any reasonable doubt** and the burden of proof falls on the prosecutor, not on the defense.

The following table depicts the possible outcomes of a hypothesis test, including Type I and Type II errors.

{{< figure library="true" src="econometrics/05_Hypothesis_Testing/Table_01.png" >}}

The **crossover error rate** (CER) is the the point at which the probability of committing each error type are equal. The lower (higher) CER is, the more (less) accurate the hypothesis test is.

---

## Decision rules in hypothesis testing

### Test-statistics and critical values

The hypothesis test produces a value that is compared with a threshold that serves as the decision rule of whether to accept or reject the null hypothesis. For instance, let the threshold to reject the null that $\phi = 0$ is 10. Then, if the difference (in absolute value) between $\hat{\phi}$ and $\phi$ is more than 10, we reject the null and assume that $\phi \neq 0$. But, if the difference is 10 or less, then according to our decision rule the difference is not enough to conclude, with a degree of confidence, that $\phi \neq 0$. In this case we **fail to reject $H_0$**.

How is the threshold level decided? In two steps. The **first** one is the desired probability of having a Type I error; this probability is usually denoted as $\alpha$. The **second** one is obtaining the value of the threshold from the probability distribution of the estimation. Use the chosen value of $\alpha$ to get the value that, in the probability distribution of $\hat{\phi}$, would produce a probability of $\alpha$. Let $f(\hat{\phi})$ denote the probability distribution of $\hat{\phi}$ and $\phi_C$ the critical (threshold) value. Then: $f(|\phi|>|\phi_C|) = \alpha$. 

The following figure depicts a typical hypothesis testing. The <span style="color:blue">blue</span> line represents the probability distribution of $\hat{\phi}$ assuming that $H_0$ is true. The <span style="color:red">red</span> denotes the critical values that delimit the rejection and fail to reject ("acceptance") regions of $H_0$. Any $\hat{\phi}$ that falls in between $(-\phi_C, \phi_C)$ means that the difference $\hat{\phi} - H_0$ is not enough to reject $H_0$. Alternatively, any $\hat{\phi}$ that falls outside the range $(-\phi_C, \phi_C)$ means that the difference $\hat{\phi} - H_0$ is large enough to reject $H_0$. You can also see that the specific values of $-\phi_C$ and $\phi_C$ depend on the chosen value of $\alpha$ (the probability of having a Type I error).


{{< figure library="true" src="econometrics/05_Hypothesis_Testing/Fig_01.png" >}}

How is $\alpha$ chosen? The easiest way is to follow already stablished conventions. In economics is typical to use 1%, 5%, and 10%, being 5% probably the most common. A different route would be to consider in more detail the nature of the problem and distribution of the data. If the cost of a Type I error is large, you may want to use a smaller value of $alpha$ (sending astronauts to the moon, or clearing a new vaccine to the general population).

### p-values

An alternative to comparing estimations with critical values given a probability distribution, is using a probability measure. The **[p-value](https://en.wikipedia.org/wiki/P-value)** is the probability that the observed estimation will be larger (in absolute values) than the chosen critical value. In the above graph, the p-value is the area under the curve for the rejection (<span style="color:green">green</span>) area. Because the p-value is a probability measure, its value is between 0 and 1.

The p-value is closely connected to the critical value. In some sense, they are two sides of the same coin. On one side is the critical value, on the other side the probability of the rejection as defined by the critical value.

The p-value has an advantage over the use of critical values in deciding whether to reject $H_0$. Each hypothesis testing has a different algebraic construction, even if general approach is similar among most of them. This means for the same confidence level each test will produce different critical value. It also means we need to be familiar with **how** the test statistic is calculated. On the contrary, p-values are homogeneous and, in this sense, easier to read. And, all that is needed, is to compare the p-value of the test-statistic with our own desired confidence level.

Let's say we chose a 5% confidence level $(\alpha = 0.05)$. Look at the above figure. This 5% defines the location of the critical values. We reject $H_0$ if:

1. The test-statistic (in absolute value) is larger than the critical value at the 5% confidence level
2. The p-value of the test-statistic is more than the 5% confidence level

You can see that the larger (in absolute values) the test-statistic is, the lower the p-value will be. This should make sense. The farther away the estimation is from your $H_0$, the less likely $H_0$ is true.

Even though the p-value is very useful and convenient, it is also subject to [misinterpretations](https://en.wikipedia.org/wiki/Misuse_of_p-values). Probably, the most important misconception is to think that the p-value is a measure of the likelihood that $H_0$ is true. Actually, the p-value is a measure of the likelihood that $H_0$ can produce extreme values at least as the ones produced by your estimation.

{{% callout warning %}}
The p-value measures the probability that $H_0$ can produce your observation, not the probability that $H_0$ is true given your observation.

---

$$
\underbrace{pr(\hat{\theta}|H_0)}_{p-value} \neq pr(H_0|\hat{\theta})
$$
{{% /callout %}}

As illustrated by the [prosecutor's fallacy](https://en.wikipedia.org/wiki/Prosecutor%27s_fallacy), this confusion can be important. The fallacy consists in concluding that the low likelihood that damning evidence (such as a DNA test result) would show up if the accused is innocent implies a low likelihood that the accused is innocent in the presence of damning evidence. How so? The fallacy is easy to see making use of [Bayes' theorem](https://en.wikipedia.org/wiki/Bayes%27_theorem).

Let $P(E)$ represent the probability of finding damning evidence $(E)$ independent of the innocence o the accused; $P(I)$ by the probability of innocence regardless of the presence of damning evidence, $P(E|I)$ be the probability of finding damning evidence conditional on the accused being innocent, and $P(I|E)$ by the probability of the accused being innocent conditional on the presence of damning evidence. Then:

$$
P(I|E) = P(E|I) \frac{P(I)}{P(E)}
$$

The fact that $P(E|I)$ is low does not necessarily mean that P(I|E) is low because $\frac{P(I)}{P(E)}$ can be high. Consider the following example. A prosecutor commits a fallacy when accusing a lottery winner of cheating given the low probability of winning the lotter. This prosecutor oversaw that probability of **anyone** winning the lottery given the total number of people that play the game.

### False positives

A decision rule (the value of $\alpha$) is chosen by deciding the maximum probability of having a Type I error (false positive). Yet, the more tests are run, the more likely there will be at least one Type I error. This is called the family-wise-error rate (FWER):

$$
FWER = 1 - (1 - \alpha)^j
$$

where $j$ denotes the number of tests.

---

## Statistical versus economic significance

The p-value is a measure of the likelihood of finding your observation assuming the null hypothesis is true, it is not a measure of how relevant the regressor is in the real world.

You may have a very low p-value of a very small number. You feel very confident in rejecting the null hypothesis that the coefficient is different than zero, even if by a small amount. It is very unlikely that you would run into your estimated $\hat{\beta}$ if the true $\beta$ were zero. But, your estimation has a very small value in the sense that the impact of your regressor on the dependent variable is negligent in **economic terms**.

You can be **statistically** very confident that a change in taxes has some effect on inflation, however, such effect is **very small** and only correlates with a very low effect on the inflation rate.

It is very important to remember the difference between **statistical** and **economic** significance. Regression results talk about statistical effects, not economic relevance.