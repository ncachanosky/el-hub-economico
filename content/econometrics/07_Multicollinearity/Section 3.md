---
# Title, summary, and page position.
linktitle: "The detection of multicollinearity"
weight: 3

# Page metadata.
title: The detection of multicollinearity
type: book  # Do not modify.
---



---

## Simple correlation

A first approach to detecting multicollinearity is by looking at the simple correlation between regressors. A chosen arbitrary value (say 0.80) can be used as the threshold value to conclude the model has multicollinearity.

This approach is simple and quick, but suffers from two shortcomings.

**First**. The *unacceptable* inflated standard deviations may occur at different correlation values. What matters the most if the inflated variance, not the correlation value in itself.


**Second**. A model with more than two regressors can have low correlation values and yet suffer from a high level multicollinearity. A regressor may have low correlation with any other regressor on a one-to-one basis and yet by highly collinear with a linear combination of other regressors.

---

## Low $t$-scores with high joint significance

Because multicollinearity increases the standard deviation of the estimated coefficients, one symptom of potential multicollinearity is one all (or most of) regressors **are not**, statistically, different than zero but the model depicts a clear presence of joint significance.

For example. A model may depict low $t$-scores (high p-values) and at the same time have a high $\bar{R}^2$ and a high $F$-statistic (low p-value). 

How is it possible that we can't reject the null that any coefficient is different than zero and yet have a strong result in support of joint significance? One explanation is that the $t$-test is biased because the variance of the coefficients are inflated. This produces lower $t$-scores and higher p-values.

---

## High sensitive coefficients

Another symptom of collinearity is when the coefficients are highly sensitive to (1) change in model specification or (2) small change in the sample size.

Removing a collinear regressor can have a large impact on the model estimation by significantly improving the efficiency of the estimation. Since "noise" is removed from the model, coefficients become more precise.

A base model can be estimated several times. In each occasion a different regressor is dropped from the model. If coefficients start to "jump" from one specification to the other, it is possible that the regressors are collinear. However, some of bias due to omitted variable bias can also be taking place.

---

## VIF analysis

A third way to detect multicollinearity is to calculate the $VIF$ of each regressor. A model with $K$ regressors will have $K$ number of $VIF$.

There is no strict $VIF$ value that distinguishes between presence and absence of a significant level of multicollinearity. The convention, or rule of thumb, is that a $VIF>5$ or $TOL<0.20$ indicates presence of a significant level of multicollinearity.

Yet, it is possible that two regressors can have a high degree of correlation and a low VIF (less than 5).

---

## No multicollinearity test

There is no formal statistical test of multicollinearity. To assess its presence requires an overall evaluation of the data and regression and the subjective knowledge and intuition of the researcher.

All models have to some extent some multicollinearity. Whether its presence is problematic or not depends on (1) what is the model going to be used for and (2) how much inflation of the standard deviation is the researcher willing to tolerate.