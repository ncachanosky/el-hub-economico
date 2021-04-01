---
# Title, summary, and page position.
linktitle: "Perfect and imperfect multicollinearity"
weight: 1

# Page metadata.
title: Perfect and imperfect multicollinearity
type: book  # Do not modify.
---

---

## What is multicollinearity (and collinearity)

**Multicollinearity** is the degree to which one regressor can be represented as a [linear combination](https://en.wikipedia.org/wiki/Linear_combination) of the other regressors. There is some degree of superposition of data and information across the regressors in the model. **Collinearity** is the simpler case where one regressor is colinear with one other regressor. 

Assume a simple model: $y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \varepsilon$. The figure below captures the issue of multicollinearity graphically. A model can have *low* or *high* explanatory power over the dependent variable and also have *low* or *high* multicollinearity between $x_1$ and $x_2$.

{{< figure library="true" src="econometrics/07_Multicollinearity/Fig_01.png" >}}

---

## Perfect multicollinearity

In the case of perfect multicollinearity a regressor can be completely replicated by a linear combination of other regressors. Assume you can represent $x_K$ as a linear combination of the other $K-1$ regressors.

$$
x_K = \omega_1 x_1 + \omega_2 x_2 + ... + \omega_{K-1} x_{K-1}
$$

If a linear combination exists for $x_K$, then it also exists for any other regressor. You can just re-arrange terms and get a similar expression for $x_1$ or any other regressor:

$$
x_1 = -\frac{\omega_2}{\omega_1} x_2 - ... - \frac{\omega_{K-1}}{\omega_1} x_{K-1} + \frac{1}{\omega_1} x_K
$$

You can now see that collinearity is a particular (simple) case of multicollinearity (when there is only one $\omega \neq 0$.

If the model has two or more regressors that behave similarly, then you have repeated information. The movements of one variable are matched (correlated) with the movements of some combination of other regressors. When this happens, OLS estimation is unable to distinguish the movements in one regressor from the movements in another regressors. In some occasions, this can be problematic.

**Perfect** multicollinearity typically occurs when an identity is accidentally included in the model. For instance, have GDP and all its components in the model at the same time $(GDP \equiv C + I + G + NX)$. Or when a variable is included twice with different units of measurement (temperature in Celsius and Fahrenheits).

---

## Imperfect multicollinearity

In the case of **imperfect** multicollinearity a regressor is cannot be totally represented by a linear combination of other regressors. There is an $error$ between the regressor and the linear combination.

$$
x_K = (\omega_1 x_1 + \omega_2 x_2 + ... + \omega_{K-1} x_{K-1}) + \mu
$$

The mode "independent" $x_K$ is from the other regressors, the larger $\mu$ will be and the les weight the linear combination will overlap with the information included in $x_K$.

Imperfect multicollinearity is more common that perfect multicollinearity (typically a human error in building the model). It is also more difficulty to deal with. This is the situation where two or more variables are correlated **without** being the same information represented in "different units of accounts".