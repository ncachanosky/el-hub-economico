---
# Title, summary, and page position.
linktitle: "Evaluating the quality of a regression"
weight: 3

# Page metadata.
title: Evaluating the quality of a regression
type: book  # Do not modify.
---



---

## Methods to evaluate the quality of a regression

To evaluate how good an econometric model represents and matches the observed data requires considering several different issues. The proper evaluation of an econometric model requires an holistic approach. As is usual in econometrics, there are objective (numbers) and subjective (interpretation) issues at stake.

A good quality econometric model should check the following boxes:

- [x] Does the model reflect sound economic theory?
- [x] Does the model include all the important regressors?
- [x] Are the estimated coefficients reasonable? Do their values contradict any economic theory or intuition?
- [x] Is the regression free of econometric problems? (later chapters)
- [x] How close to real data does are the model estimations? (this chapter)

This chapter deals with the last question. Namely, how good the *fit* of the model is. There are different ways to measure the goodness of fit of the model. We will go through the following four evaluations:

1. Normality of the residuals
2. Coefficient of determination
3. Mean squared error
4. Three information criteria

## Coefficients of determination

### Partition of sum of squares

Before building a measure of goodness of fit we need to decompose the variance of $y$ (the dependent variable) **around its mean**. The decomposition has three components.

First, the deviation of the observed data from its mean. The second one is the deviations that the model can predict of the dependent variable from its mean. And the third one is the residual, the difference between the difference between observed data and its mean and predicted data and the observed mean.

Since we are looking at **[variances](https://en.wikipedia.org/wiki/Variance)**[^1], these three measures squared. Therefore, we have (1) the total sum of squares (TTS), (2) the explained sum of squares (ESS), and (3) the residual sum of squares (ESS). Then, the partition of sum squares is:

$$
\begin{align}
\overbrace{\sum_i (y_i - \bar{y})^2}^{\text{TSS}} &= \overbrace{\sum_i (\hat{y}_i - \bar{y})^2}^{\text{ESS}} + \overbrace{\sum_i (y_i - \hat{y}_i)^2}^{\text{RSS}} \\\\[10pt]
\sum_i (y_i - \bar{y})^2 &= \sum_i (\hat{y}_i - \bar{y})^2 + \sum_i e_i^2
\end{align}
$$

This expression separates the total variance of the observed data between the explained and residual (non-explained) variance produced by the model. It is easier to understand the relationship between $TSS$, $ESS$, and $RSS$ in a scatter plot. The figure below shows this relationship. See how the regression line goes through the mean of $y$ and $x$ and what the estimation is doing is measuring deviation from the mean of the dependent variable for each $x_i$.We can now build the $R^2$. 

{{< figure library="true" src="econometrics/03_OLS/Fig_06.png" >}}  

### The $R^2$ (R-squared)

$R^2$, the *[coefficient of determination](https://en.wikipedia.org/wiki/Coefficient_of_determination)*, is the simplest and most common measure of goodness of fit. In simple terms, $R^2$ is the **ratio of the explained variations over total variations** of the dependent variable.

$$
\begin{aligned}
R^2 &= \frac{ESS}{TSS} \\\\
R^2 &= 1 - \frac{RSS}{TSS} \\\\
R^2 &= 1 - \frac{\sum e_i^2}{\sum (y_i - \bar{y})^2}, \in [0, 1]
\end{aligned}
$$ 

{{% callout note%}}
$\bar{R}^2$ measures the percent of the variations of $y$ arounds its mean that is explained by a regression.
{{% /callout %}}

The higher $R^2$ is, the closer the estimation $(\hat{y}_i)$ is to the real and observed data $(y_i)$. In plain words, $R^2$ measures the *percentage* of the variance of $y$ that the model can explain and has the following properties.

* Since $TSS = ESS + RSS$ and all three terms are positive, $R^2$ is between zero and one.
* Since OLS is minimizing $e^2$, your regression is getting the maximum $R^2$ possible given your data.

However, $R^2$ also has the following limitations:

* It does not inform if an important variable has been omitted
* It does not inform if the correct model (linear or otherwise) has been used
* It does not inform if the model is using the appropriate set of regressors
* It does not inform if you have enough data points to obtain an accurate estimation

Yet, there is another important shortcoming of $R^2$. The inclusion of a relevant regressors adds explanatory power to the model and makes $R^2$ increase (residuals are smaller). The addition of an irrelevant variables does not add, but neither subtracts, explanatory power from the model. In this case, $R^2$ does not change. Because of how it is calculated, the addition of regressors can only increase (or do nothing) to the value of $R^2$.

This behavior of $R^2$ with respect to the number of regressors is a problem because the more regressors are included in the model, the more coefficients the model must estimate. The ratio of data (information) to coefficients fall, reducing the amount of data that can be used *per* coefficient. This implies a loss in the [degrees of freedom](https://en.wikipedia.org/wiki/Degrees_of_freedom_(statistics)#:~:text=not%20present%20%20%20Continuous%20data%20%20,Biplot%20Box%20plot%20Control%20chart%20%20...%20) of the model. Degrees of freedom are the number of independent variables free to vary without affecting imposed constraints. More formally, degrees of freedom is the *minimum number of independent coordinates that can specify the position of the system completely*.

In econometrics, degrees of freedom are important as a measure of how much data is being used to produce an accurate estimation of the $betas$. Assume $N=10$ and your model needs to estimate 3 coefficients, then you have 7 observations to make such estimation. If you add three more regressors, now you have 6 coefficients but only 4 observations to calculate your model. The more data points you have *per* coefficient, the more accurate the estimation will be. Each regressor *substracts* one observation from your sample. You cannot have negative degrees of freedom, therefore the number of coefficients must be less than the sample size $(K<N)$

Adding regressors to a model is not free. Each regressor brings new explanatory power to the model at the cost of loosing a degree of freedom and accuracy. $R^2$ ignores the cost of adding regressors. Because adding more regressors to the model can never decrease $R^2$, you run the risk of *[overfitting](https://en.wikipedia.org/wiki/Overfitting)* your model. In short, overfitting occurs when the model tracks the data too close but spuriously, that is the model uses residual data *as if* it were real data. This occurs when the model tries to specify more coefficients than can be justified with the data at hand.

Consider the regression where the mileage (mpg) of a car is predicted by its weight. We can add other relevent regressors such as the manufacturer, year of the car, type of car (sedan, SUV, sports car, and so on). We can also add an irrelevant variable, such as the first letter of name of their owners. This addition can bring some random (spourious) correlation with the mileage of the cars. $R^2$ will increase even if the *true* explanatory power of the model has not increased, you just added noise that is confused with *explanatory* power. The statistical confusion occurs because there are not enough degrees of freedom to filter this noise out.

The objective of a good econometric model is not to maximize $R^2$. That can be easily done by adding a large number of regressors. Yet, this will be a bad model because it may be overfitted and with inaccurate coefficients.

The role of the model is to find the **right** value of $R^2$. Ideally, the model will give a precise estimation of how much of the variations of $y$ can be explained with your regressors. An accurate estimation of what the **model does not explain** is valuable information as well that can lead to further research questions. Different subjects have different $R^2$. For instance, is likely to get a high $R^2$ with time-series because of correlation in time-trends. On the other hand, cross-sectional data looking at different countries may have a low $R^2$ because there are important differences across countries that are not easy to quantify.

This *inflation* of the $R^2$ is particularly problematic when comparing different models that have different number of regressors. The adjusted R-square, adj-$R^2$, or $\bar{R}^2$ is an extended version of $R^2$ that takes into account differences in degrees of freedom.

{{% callout alert%}}
In some books:
$SSE$: Error Sum of Squares ($RSS$ above)
$SSR$: Regression Sum of Squares ($ESS$ above)
{{% /callout %}}

### The $\bar{R}^2$ (adjusted R-squared)

The $\bar{R}^2$ includes the trade-off between adding explanatory power (information) and loss of freedom. $\bar{R}^2$ only increases **if** the new regressors adds more information that the cost of loosing a degree of freedom. Assuming there are $K$ variables plus the constnat, then the degree of freedom adjustment works the following way

$$
\bar{R}^2 = 1- \frac{N-K-1}{N-1} \frac{RSS}{TSS}
$$

{{% callout note%}}
$\bar{R}^2$ measures the percent of the variations of $y$ arounds its mean that is explained by a regression, **adjusted by the degrees of freedom**.
{{% /callout %}}

Adding an irrelevant variable (no explanatory power) makes $\bar{R}^2$ decrease. The new regressor adds little information but harms the esimtation of the other regressors by reducing the amount of information (datapoints) availabe to estimate the $betas$.

{{<icon name="file-excel" pack="fas" >}} {{% staticref "media/econometrics/03_OLS/OLS (simple example) with R-square.xlsx" %}}Download OLS simple example with R-square.{{% /staticref %}}

---

## Root Mean Squared Error (RMSE)

The [Root Mean Squared Error (RMSE)](https://en.wikipedia.org/wiki/Root-mean-square_deviation) measures the average of the squared errors of the regression.

By construct, RMSE is always positive (the negative result of the square root is ignored), with a value of zero only in the case of a perfect fit. Differently to $R^2$ and $\hat{R}^2$, RMSA has a unit of measure which coincides with the unit of measure of the dependent variable. For instance, if the dependent variable is miles per gallon $(mpg)$, then RMSE is also measured in $mpg$.

RMSE is calculated the following way:

$$
\begin{align}
RMSE &= \sqrt{\frac{1}{N} \sum_{i=1}^N \left(y_i - \hat{y}_i \right)^2} \\\\[10pt]
RMSE &= \sqrt{\frac{1}{N} \sum_{i=1}^N e_i^2}
\end{align}
$$

---

## Information criteria

There are three popular **information criteria** measures that evaluate the quality of regression by accounting for the trade-off between new information added to the model and information lost. In other words, these measures try to balance the risk of *overfitting* as well as the risk of *underfitting*.

The three information criteria are:

1. The Akaike Information Criterion (AIC)
2. The Bayesian Information Criterion (BIC)
3. The Hannan-Quinn Information Criterion (HQC)

However, before looking at these measures into more detail, we need to make stop at one of their main components, the **maximun likelihood**.

### Maximum likelihood

Assume you have a sample of $N$ random observations. The randonmess of this information means that it was originated from a probability function. It is possible that even if we know that our sample comes from a probability distribution, we don't which probability function is producing our observed data.

The maximum likelihood is the probability distribution that is more likely to have produced the data in your sample. For instance, you know that your sample comes from a normal distribution, but you don't know the mean, standard deviation, skeweness, and kurtosis of the function. A maximum likelihood estimatino (MLE) would use the data in the sample to estimate the mean, standard deviation, skewness, and kurtosis of the normal distribion more likely to produce your sample.

The [likelihood function](https://en.wikipedia.org/wiki/Likelihood_function) measures the likelihood of a probability function with respect to its parameters. If the function has a peak, then the parameters that produces that maximum define the probability function with a maximum likelihood. The stability of the MLE depends of the curvature of the likelihood function around the peak.

For computational simiplicity, the solution to this problem is done with a log-transformatio of the probability function, and therefore it is somestimes reported as the *log-likelihood*.

Let $\mathfrak{L(\theta)}$ by the likelihood function, where $\theta$ is the probability function parameters. MLE finds the $\theta^\*$ that maximizies $\mathfrak{L}(\theta^*)$. The simple example below illustrates how MLE works.

#### A simple example

Assume you have a coin which you flip three times. You get two *heads* (H) and one *tail* (T). That is, you observe ${HHT}$. If you know for sure this is a fair coin, then you know that the probability of heads is $1/2$ and the probability of tails is $1/2$. Knowing for sure this is a fair coin means that we already know the probability distribution of *heads* and *tails* in this coin.

However, we do not know if this is a fair coin or not. The MLE question is what are the probabilities of *heads* and *tails* more likely to produce $\{HHT\}$.

Let $0 \leq p_H \leq 1$ be the probability of *heads* and $1-p_H$ be the probability of *tails*. Since we got two *heads* and one *tail*, we need to find the value of $p_H$ that maximizes $p_H^2 (1-p_H)$.

$$
\operatorname*{max}_{p_H} \mathfrak{L}(p_H) = {p_H}^2 (1 - p_H)
$$

This example allows for an easy analytical solution. Take the first derivative and solve for $p_H$.

$$
\begin{aligned}
\mathfrak{L}(p_H) &= {p_H}^2 (1 - p_H) \\\\[10pt]
\frac{\mathfrak{L}(p_H)}{\partial p_H} &= 2p_H - 3{p_H}^2 = 0 \\\\[10pt]
{p_H}^* &= \frac{2}{3}
\end{aligned}
$$

The second order condition confirms this is a maximum.

$$
\begin{aligned}
\frac{\partial ^2 \mathfrak{L}(p_H)}{\partial {p_H}^2} = -3 < 0
\end{aligned}
$$

We can now use $p_H^*$ to get the value maximum likelihood value:

$$
\begin{aligned}
\mathfrak{L}(p_H^*) &= \left( \frac{2}{3} \right)^2 \left( 1 - \frac{2}{3} \right) \\\\[10pt]
\mathfrak{L}(p_H) &\approx 0.14
\end{aligned}
$$

This means that an unfair coin with $2/3$ probability of producing a *heads* (and therefore a $1/3$ probability of producing a *tail*) is the more likely coin to produce the observed $\{HHT\}$. The plot below depicts the MLE problem we just solved analytically.

{{< figure library="true" src="econometrics/03_OLS/Fig_07.png" >}}  

Finally, note that the likelihood function **is not** a probability distribution. This means that the integral of $\mathfrak{L}$ may not equal 1.

$$
\begin{aligned}
\int_0^1 \left(p_H^2 (1-p_h)\right) dp_H &= \int_0^1 \left(p_H^2 - p_H^3\right) dp_H \\\\[10pt]
&= \frac{1}{3} p_H^3 - \frac{1}{4}p_H^4 + C |_0^1 \\\\[10pt]
&= \left(\frac{1}{3} - \frac{1}{4} +C \right) - \left(\frac{1}{3} \cdot 0 - \frac{1}{4} \cdot 0 + C \right) \\\\[10pt]
&= \frac{1}{12}
\end{aligned}
$$

### AIC: Akaike Information Criterion

[AIC](https://en.wikipedia.org/wiki/Akaike_information_criterion) is an estimation of *out-of-sample* prediction errors. The AIC is a *relative* statistic, meaning it is only informative when compared with the AIC of other models. Different to, for instance, $R^2$ which provides information about one particular regression, AIC is used to compare *different models*. For instance, AIC will not tell you if all your models are bad fits. If all your models are bad, then AIC will rank them from worse to less worse without signaling how bad they are.

The maximum likelihood is the way AIC rewards goodness of fit. The higher the likelihood of the probability function producing the observed data, the more accurate predictions should be. AIC penalizes loss of information and the risk of overfitting by counting the number estimated parameters.

Let the model have $K$ parameters to be estimated (this includes the constant) and let $\mathfrak{L^*}$ be the value of the maximum likelihood function. Then, AIC is calculated the following way

$$
AIC = 2K - 2ln(\mathfrak{L^*})
$$

Note that the goodness of fit has a negative sign and that the number of regressors of positive signs. This means that the *more negative* the number is, the better. An AIC of 10 is better than an AIC of 100. And an AIC of -100 is better than an AIC of -10.

{{< figure library="true" src="econometrics/03_OLS/Fig_08.png" >}}

AIC is an asymptotic measure, which means that it requires a large sample size to offer reliable estimations to make relative comparisons. If the sample size is small, then AIC can selected models that have too many parameters (risk of overfitting).[^2]

### BIC: Bayesian Information Criterion (or Schwarz Information Criterion -SIC)

[BIC](https://en.wikipedia.org/wiki/Bayesian_information_criterion) (or SIC) follows a similar approach to that of AIC. The main difference between BIC and AIC is the penalty measure of how many coefficients are being estimated. The BIC formula is:

$$
BIC = K \cdot ln(N) - 2ln(\mathfrak{L^*})
$$

Similar to AIC, BIC works better with a large sample size (with respect to $K$) and the *more negative* the value of BIC the better.

Even though AIC and BIC look very similar, their different foundations suggest they are better fit for different tasks. BIC is more appropriate to select the *true model* **if** the true model is included among the candidates. Put it differently, BIC tends to choose the true model with probability one as the sample size increases $(N \rightarrow \infty)$. AIC, however, offers a probability less than one of choosing the right model under similar conditions. BIC is asymptotically efficient, while AIC is not.

On the other hand, it is very unlikely that the true model will be one of the candidates. AIC offers a better selection mechanism to pick the model that minimizes least mean squared errors. Put it differently, AIC is more useful to find an approximation model assuming the true model is not included among the candidates. 

Look at the AIC and BIC formulas. AIC includes a linear penalty term with respect to the number of coefficients to estimate. BIC penalty term is increasing with respect to the sample size. Therefore, a large sample can produce a high penalty and a low likelihood value if the data is used in a bad model.

### HQC: Hannan-Quinn Information Criterion

Finally. [HQC](https://en.wikipedia.org/wiki/Hannan%E2%80%93Quinn_information_criterion) offers an alternative information criterion to AIC and BIC. HQC is calculated in the following way:

$$
HQC = 2K \cdot ln \left(ln(N) \right) - 2 ln (\mathfrak{L^*})
$$

Like AIC and BIC, the *more negative* HQC is, the better. Unlike AIC, but like BIC, HQC is asymptotically effiicient (tends to chose the true model when $N \rightarrow \infty)$.

---

## The normality of the residuals

Finally, residuals can also help diagnose if anything is wrong with the regression. As suggested so far, and we will see in more detail in the next chapters, a good regression will produce normally distributed residuals. Therefore, an indication that something may be wrong with the model is when residuals deviate from a normal distribution.

As we move forward, we will see how to formally test for residuals having a normal distribution and what other tests can be done to assess the quality of the regression. Right now, the important message is that residuals are a very important source of information regarding the quality and characteristics of the regression model.

---

## How to use all this information

We have gone through the more common, but not all, tools of model selection among different candidates.

In principle you want to look at all of them, but remain careful in how you interpret them. For instance, the R-squared measures goodness of fit in-sample, while the information criteria are looking out-of-sample expected fit. 

It would be ideal if all the selection criteria methods point out to the same model. But this is not always the case. The fact that you are running a regression does not mean you stop being an economist. Besides looking at all these measures, you should also ask yourself which model makes more economic sense. None of these methods is perfect, and the risk remains that a variable would accidentally improve $\bar{R}^2$. This may produce an unexpected sign, such an upward sloping demand. This should tell you that the model with the higher $\bar{R}^2$ is probably not the best one. However, another problem is that such model would produce biased estimations *even if* it has a higher $\bar{R}^2$ than an alternative model. This is an example of overfitting.

---

## Appendix

### Proof: $TSS = ESS + RSS$

$$
\begin{align}
\sum_i (y_i - \bar{y})^2 &= \sum_i (y_i - \bar{y} + \hat{y}_i - \hat{y}_i)^2 \\\\[10pt]
&= \sum_i \left( (\hat{y}_i - \bar{y}) + (y_i - \hat{y}_i) \right)^2 \\\\[10pt]
&= \sum_i \left( (\hat{y}_i - \bar{y}) + e_i \right)^2 \\\\[10pt]
&= \sum_i \left( (\hat{y}_i - \bar{y})^2 + e_i^2 + 2 \sum_i (y_i - \bar{y}) e_i \right) \\\\[10pt]
&= \sum_i (\hat{y}_i - \bar{y})^2 + \sum_i e_i^2 + 2 \sum_i e_i (\hat{\beta}_0 + \hat{\beta}_1 x\_{1,i} + ... + \hat{\beta}_K x\_{K,i} - \bar{y}) \\\\[10pt]
&= \sum_i (y_i - \hat{y})^2 + \sum_i e_i^2 + 2 (\hat{\beta}_0 - \bar{y}) \overbrace{\sum_i e_i}^{0} + 2 \hat{\beta}_1 \overbrace{\sum_i e_i x\_{1,i}}^{0} + ... + 2 \hat{\beta}_K \overbrace{\sum_i e_i x\_{K,i}}^{0} \\\\[10pt]
\underbrace{\sum_i (y_i - \bar{y})^2}\_{\text{TSS}} &= \underbrace{\sum_i (y_i - \hat{y})^2}\_{\text{ESS}} + \underbrace{\sum_i e_i^2}\_{\text{RSS}} \\\\[10pt]
\end{align}
$$

<!-- FOOTNOTES -->
[^1]: Recall that the variance of a **random** variable $x$ is: $\sum_i = p_i (x_i - \bar{x})^2$ (where $0 < p_i< 1$). If all values of $x$ have the same probability and there are $n$ observations, then $p_i = \frac{1}{n}$.

[^2]: AIC is an asymptotic measure, which means that it requires a large sample size to offer reliable estimations to make relative comparisons. If the sample size is small, then AIC can selected models that have too many parameters (risk of overfitting). Let $AICc$ be the AIC corrected for small samples, then: $AICc = AIC \frac{2K^2 + 2K}{N - K - 1}$.