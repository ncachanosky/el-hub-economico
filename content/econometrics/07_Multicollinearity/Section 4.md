---
# Title, summary, and page position.
linktitle: "Remedies to multicollinearity"
weight: 4

# Page metadata.
title: Remedies to multicollinearity
type: book  # Do not modify.
---



---

## Do nothing

It is not clear that anything should be done with a model that has multicollinearity. The reason is, once again, that classical assumptions are not violated. The model may be imprecise, but remains unbiased. A few reasons to do nothing are:

1. Multicollinearity may not affect the standard deviation of the $betas$ enough to be considered a serious problem
2. The model is built with the intention to make a prediction of the dependent variable, not to evaluate the significance of a particular coefficient
3. Dropping a collinear regressor can produce omitted variable bias

Fixing multicollinearity faces trade-offs and, in many occasions, doing nothing may be better than worrying this issue excessively.

Assume now, however, that for a particular study there is too much presence of multicollinearity. What can be done?

---

## Drop redundant variables

If possible, drop **redundant** variables. Redundant variables are variables that are essentially measuring the same thing, *even if* they are not equal to each other. For instance, `disposable income` and `NGDP` are redundant variables. Both variables are measuring the same thing: `income`. It is likely the model does not need both of these regressors.

What is important is the **information** that a regressor brings to the model, not so much the name a variable is given. Two variables may have different names and yet have the same information.

Another reason to drop **redundant** variables is to reduce the risk of over-fitting the model.

---

## Use principal components

Condense or summarize the information an collinear regressors through [principal component analysis](https://en.wikipedia.org/wiki/Principal_component_analysis) (PCA).

PCA reduces the number of regressors (dimension of the data) maximizing the variance of the information included in the regressors. PCA will reduce the degree of multicollinearity, potentially save some degrees of freedom, but risks falling into "omitted variable bias" if the information let-behind is relevant for the accuracy of the estimation.

---

## Increase the sample size

Multicollinearity can be seen as another term for some of the problems of having a small sample. If the dataset is not large enough, then regressors can be collinear.

Increasing the sample size will reduce the degree of collinearity as long as the information in each regressor is independent to the information in other regressors.

In economics, however, increasing the sample size is not always possible.