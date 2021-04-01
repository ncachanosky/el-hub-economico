---
# Title, summary, and page position.
linktitle: "What is the Classical Model"
weight: 1

# Page metadata.
title: What is the Classical Model
type: book  # Do not modify.
---



---

## The Classical Model

In econometrics, the **classical model** refers to a set of basic assumptions. If these **ideal conditions** hold, then OLS is the **best** method to estimate unknown coefficients. If one or more of the classical assumptions do not hold, then it is possible that a different estimation technique would yield better estimations than OLS. For instance, *generalized least squares* may be a better choice than *ordinary least squares*.

Before drawing conclusions from a regression output, it is important to check if the classical assumptions are present in your data and model. If this is not the case, then adjustments may be needed in order to avoid potential bias in the regression results or using a different estimation technique may be a best choice.

We already used some of this assumptions in our previous examples. Therefore, some of the **classical assumptions** will be somehow familiar, even if in this chapter we will go through a more careful and detailed discussion than we did so far.

In this chapter we will go through two important implications of the **classical assumptions**:

1. The distribution of $\hat{\beta}$
2. The Gauss-Markov Theorem

The seven classical assumptions are:

1. The model is linear
2. The error term has zero population mean
3. All regressors are uncorrelated with the error term
4. Observations of the error term are uncorrelated with each other (no serial correlation)
5. The error term has a constant variance (homoskedasticity)
6. No explanatory variable is a perfect linear combination of other(s) explanatory variable(s) (multicollinearity)
7. The error term is normally distributed