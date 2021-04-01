---
# Title, summary, and page position.
linktitle: "Example"
weight: 5

# Page metadata.
title: Example
type: book  # Do not modify.
---



---

## Model and data

Let's look at how multicollinearity looks like using the `auto` dataset in `STATA`. Assume the following model:

$$
price = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \beta_3 x_3 + \beta_4 x_4 + \beta_5 x_5 + \beta_6 x_6 + \varepsilon
$$

where:

1. $x_1$: mpg
2. $x_2$: headroom
3. $x_3$: trunk size
4. $x_4$: weight
5. $x_5$: length
6. $x_6$: foreign dummy

The example will diagnose the presence of multicollinearity following the same steps discussed in the previous section. All the tables are produced by the following code.

```
*==============================================================================*
* MODEL SPECIFICATION
* Multicollinearity
* Code sample: 6.1
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and data
set scheme s1color  // Set plot scheme
sysuse auto, clear

*|CELL 2|----------------------------------------------------------------------
*|Correlation matrix
correl price mpg rep78 headroom trunk weight length foreign

*|Regressions
regress price mpg rep78 headroom trunk weight length foreign
estimates store M1, title (Model 1)
vif // To be used later

quietly{
regress price mpg headroom trunk weight length foreign
estimates store M2, title (Model 2)

regress price mpg rep78 trunk weight length foreign
estimates store M3, title (Model 3)

regress price mpg rep78 headroom weight length foreign
estimates store M4, title (Model 4)

regress price mpg rep78 headroom trunk length foreign
estimates store M5, title (Model 5)

regress price mpg rep78 headroom trunk weight foreign
estimates store M6, title (Model 6)
}

*|Build table and look for coefficient sensitivity
estout M1 M2 M3 M4 M5 M6, title(Coefficient sensitivity) ///
	collabels(none) ///
	mlabels(, titles) ///
	cells(b(star fmt(3)) se(par fmt(2))) legend ///
	label varlabels(_cons Constant) ///
	stats(df_r r2 aic bic, fmt(0 3 3 3) label(DF Adj-R2 AIC BIC))
```

---

### Detecting multicollinearity

## Simple correlation

Let's start looking at the correlation matrix shown below.

{{< figure library="true" src="econometrics/07_Multicollinearity/Fig_02.png" >}}

Some regressors are, as expected, highly correlated. In particular, look at the following correlations:

1. $\rho(mpg, weight) = -0.8055$
2. $\rho(mpg, length) = -0.8037$
3. $\rho(weight, length) = 0.9478$

Understanding the natural relationship between length and weight as well as correlation so close to 1 suggest that these may be **redundant** variables. Different approaches to measure the same *information*. It is probably unnecessary to include both variables in the model.

## Low $t$-scores with high joint significance

The next step is to look at the output of the base model, as shown below.

{{< figure library="true" src="econometrics/07_Multicollinearity/Fig_03.png" >}}

There are three regressors that are statistically significant different than zero: (1) $weight$, (2), $length$, and (3) $foreign$ at the typical p-values convention. The model also depicts a high level of joint significance according to the $F$-test.

In this example, the evidence of the presence of multicollinearity is not clear-cut. It is possible that this variables are statistically relevant *even with* inflated standard deviations of the coefficients. Or, it may be the case that there is no multicollinearity.

This situation exemplifies that diagnosing econometric conditions are not always obvious.

## High sensitive coefficients

Let's look now at what happens to the coefficients when we vary the model specification.

{{< figure library="true" src="econometrics/07_Multicollinearity/Fig_04.png" >}}

In this case, the reason to vary the model specification is to observe how robust the estimation is to changes in data, it is no intended to find the *best* model possible. Looking for multicollinearity and finding the best fit are two different motivations to play with different versions of the base model.

Models 1, 3, and 4 show more or less similar coefficients. However, models 5 and 6 show some large difference in coefficients, particularly in $mpg$, $trunk$, $length$, $car type$ (foreign dummy), and the $constant$. In some cases even the sign of the coefficient changes. For instance, according to model 6, the more trunk space the car has, the lower the price. 

## VIF analysis

Finally, let's look at the $VIF$ for each coefficient.

{{< figure library="true" src="econometrics/07_Multicollinearity/Fig_05.png" >}}

Using the rule of thumb that multicollinearity is highly present with a $VIF>5$ or $TOL<0.20$ we see that $length$ and $weight$ are two variables with a high degree of multicollinearity. These results shows that these two variables can be replicated to a large extent as a linear combination of the other regressors.

Are these *redundant* variables? Look again at the six models in the above table. Removing either one of these variables (models 5 and 6) decreases the quality of the model with respect to any of the other four models. Either measured by $\bar{R}^2$, $AIC$, or $BIC$, any of models 1 to 4 is produces a better fit to the data than either models 5 or 6. These models have multicollinearity, but removing either one of these variables carries a significant risk of falling into omitted variable bias.