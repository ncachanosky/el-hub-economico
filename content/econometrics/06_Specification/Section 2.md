---
# Title, summary, and page position.
linktitle: "Functional forms"
weight: 2

# Page metadata.
title: Functional forms
type: book  # Do not modify.
---



---

## Alternative functional linear forms

Remember that OLS requires that the model is linear **on the coefficients**. The relationship between $y$ and your regressors may not be linear, even if the regression is. Recall that what OLS needs is the following relationship:

$$
f(y) = \beta_0 + \beta_1 f(x_1) + ... + \beta_K x_K + \varepsilon
$$

After you identify all the relevant regressors to be included in the model, you need to decide on the functional form (relationship) between the dependent variable and the regressors. In addition, different functional forms have convenient economic interpretations as well.

Let's discuss first the most common functional forms, how to pick the correct one, and then work through a `STATA` misspecification example.

---

## Common functional forms

For simplicity assume the model has only one variable.

### Linear

The linear model: $y = \beta_0 + \beta_1 x + \varepsilon$

* If $x$ changes by 1 unit, $y$ changes $\beta$ times

This functional form assumes that the relationship between the regressor and the dependent variable is **constant**. In other words, the model assumes a constant **marginal effect** of the regressors on the dependent variable. Because the marginal effect is constant, the elasticity between the regressor and the dependent variable is **not constant**. Recall that elasticity depends on the interaction between (1) the slope between $y$ and $x$ and (2) the "position on the line" $(x/y)$.

$$
\begin{aligned}
\frac{\Delta y}{\Delta x} &= \beta_1 \\\\[10pt]
\epsilon_{(y,x)} &= \frac{\Delta y}{\Delta x} \frac{x}{y} = \beta_1 \frac{x}{y}
\end{aligned}
$$

### Double-Log or Log-Log

The log-log model: $ln(y) = \beta_0 + \beta_1 ln(x) + \varepsilon$

* If $x$ changes 1%, $y$ changes $\beta$%

The log-log-model has the convenient feature of producing a **constant** elasticity captured in the estimated coefficient. This functional form yields the opposite result than the linear model. Because the elasticity is constant, the marginal effect of $x$ on $y$ is **not constant**.

$$
\begin{aligned}
\frac{\Delta y}{\Delta x} &= \frac{y}{x} \bar{\epsilon}\_{y,x} \\\\[10pt]
\epsilon_{(y,x)} &= \frac{\Delta y}{y} \frac{x}{\Delta x} = \frac{\Delta ln(y)}{\Delta ln(x)} = \beta_1
\end{aligned}
$$

### Semi-Logs: Lin-Log and Log-Lin

The lin-log model: $y = \beta_0 + \beta_1 ln(x) + \varepsilon$.  
The log-lin model: $ln(y) = \beta_0 + \beta_1 x + \varepsilon$

* Lin-log model: If $x$ changes 1%, $y$ changes $\beta$ times
* Log-lin model: If $x$ changes 1 unit, $y$ changes $\beta$%

The **lin-log** model assumes that the effect of $x$ on $y$ increases at a decreasing rate. This is a very common relationship in economics. For example, the productivity of hours of work, or the impact of income on consumption. 

The **log-lin** models assumes assumes that $y$ makes a percent adjustment to an absolute change in $x$. For instance, a change in the absolute profit of firm results in a percent change increase in wages.

### Polynomial

A polynomial function captures a non-constant slope that depends on the value of the regressor. Consider a second-degree polynomial (quadratic) form.

The quadratic model: $y = \beta_0 + \beta_1 x + \beta_1 x^2 + \varepsilon$

* If $x$ changes by 1 unit. $y$ changes $(\beta_1 + \beta_2 x)$ times

A quadratic function can be use to model a typical cost function, where $y$ is output, $\beta_0$ is the fixed cost, and the other two terms capture variable costs of changes in inputs $(x)$.

$$
\frac{\Delta y}{\Delta x} = \beta_1 + \beta_2 x
$$

### Inverse

The inverse model: $y = \beta_0 + \beta_1 \frac{1}{x} + \varepsilon$

* The effect of $x$ on $Y$ approaches 0 when $x \rightarrow \infty$

This model captures reciprocal relationship between the variables (such as in the original treatment of the Phillips curve). The model assumes that as $x \rightarrow \infty$, $y \rightarrow \beta_0 + \varepsilon$.

$$
\frac{\Delta y}{\Delta x} = \frac{-\beta_1}{x^2}
$$

### Combining functional forms

Even if the terminology talks about "functional forms", the above discussion looks at relationship between regressors. In other words, different "functional forms" can be combined into one model. Consider the following example different functional forms.

$$
ln(y) = \beta_0 + \beta_1 x_1 + \beta_2 x_1^2 + \beta_3 ln(x_2) + \beta_4 \frac{1}{x_4} + \varepsilon
$$

In other words, picking the right "functional form" means picking the right relationship of **each** regressor with the correct representation of $y$.

### Functional forms in matrix notation

Different functional forms have no effect on the OLS matrix notations. This is another reason why matrix notation is so convenient in econometrics. It helps keeping notation simple and consistent. Consider the above example in matrix notation.

$$
\underbrace{
\begin{pmatrix}
    y_1     \\\\
    y_2     \\\\
    y_3     \\\\
    \vdots  \\\\
    y_N
\end{pmatrix}}\_{y} =
\underbrace{
\begin{pmatrix}
    1       & x_{1,1} & x_{1,1}^2 & ln(x_{1,2}) & \frac{1}{x_{1,3}}  \\\\
    1       & x_{2,1} & x_{2,1}^2 & ln(x_{2,2}) & \frac{1}{x_{2,3}}  \\\\
    1       & x_{3,1} & x_{3,1}^2 & ln(x_{3,2}) & \frac{1}{x_{3,3}}  \\\\
    \vdots  & \cdots  & \cdots    & \cdots      & \vdots   \\\\
    1       & x_{N,2} & x_{N,1}^2 & ln(x_{N,2}) & \frac{1}{x_{N,3}}
\end{pmatrix}}\_{X}
\underbrace{
\begin{pmatrix}
    \beta_0 \\\\
    \beta_1 \\\\
    \beta_2 \\\\
    \beta_3 \\\\
    \beta_4
\end{pmatrix}}\_{\beta} + 
\underbrace{
\begin{pmatrix}
    \varepsilon_1 \\\\
    \varepsilon_2 \\\\
    \varepsilon_3 \\\\
    \vdots        \\\\
    \varepsilon_N
\end{pmatrix}}\_{\varepsilon}
$$

---

## Choosing the right functional form

If your model is trying to capture the relationship between variables according to a theory, then the model functional form should match the theoretical functional forms. If you deviate from the theoretical relationship, then the coefficients may not be a good representation of the theory.

| Functional form | Equation                                        | Effect of $x$ on $y$ (theory) |
|-----------------|-------------------------------------------------|------------------|
| Linear          | $y = \beta_0 + \beta_1 x + \varepsilon$         | If $\Delta x = 1 \rightarrow \Delta y = 1$ |
| Log-Log         | $ln(y) = \beta_0 + \beta_1 ln(x) + \varepsilon$ | If $\Delta x = 1$% $\rightarrow \Delta y = \beta_1$% |
| Lin-Log         | $y = \beta_0 + \beta_1 ln(x) + \varepsilon$     | If $\Delta x = 1$% $\rightarrow \Delta y = \beta_1$ |
| Log-Lin         | $\ln(y) = \beta_0 + \beta_1 x$                  | If $\Delta x = 1 \rightarrow \Delta y \approx \beta_1$%|
| Quadratic      | $y = \beta_0 + \beta_1 x + \beta_2 x^2 + \varepsilon$ | If $\Delta x = 1 \rightarrow \Delta y = (\beta_1 + \beta_2 x)$ |
| Inverse         | $y = \beta_0 + \beta_1 \frac{1}{x}$             | If $x \rightarrow \infty \rightarrow \frac{\Delta y}{\Delta x} \rightarrow 0$ |
---

## Example

Using a wrong functional from can likely show up as incorrect looking residuals. If the model is correctly specified, then the residuals should look random with a normal-type of distribution. 

Because what is not included in the model falls into the residuals, residuals provide diagnosis information.

The following `STATA` code builds a quadratic functional form and then fits a correct and incorrect (linear) models. Residuals from both models are compared.

```
*==============================================================================*
* MODEL SPECIFICATION
* Create a model misspecification
* Code sample: 5.1
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings
set scheme s1color  // Set plot scheme

*|CELL 2|----------------------------------------------------------------------*
*|Create required data
drop _all
set obs 100

gen   X = _n
label variable X "X"
tsset X

generate Y = 5000 - 80*X + X^2 + rnormal(0, 250)
label variable Y "Y"

*|Create incorrect fit: Keep y_hat and residuals
regress Y X
predict Y_hat1, xb
predict resid1, residuals

*|Create correct fit: Keep y_hat and residuals
gen X2 = X^2
regress Y X X2
predict Y_hat2, xb
predict resid2, residuals

*|Creat plots
twoway scatter Y X, nodraw saving(plot1, replace) ///
	   mcolor(green%75) msize(vsmall) ///
	 ||lfit Y X, ///
	   lcolor(red%75) ///
	 ||line Y_hat2 X, ///
	   lcolor(green%75) ///
	   legend(off)
	   
twoway scatter resid1 X, nodraw saving(plot2, replace) ///
	   mcolor(red%75) lcolor(red) msize(vsmall) ///
	   yline(0, lcolor(black))

twoway scatter resid2 X, nodraw saving(plot3, replace) ///
	   mcolor(green%75) lcolor(green%75) msize(vsmall) ///
	   yline(0, lcolor(black))

graph combine plot1.gph plot2.gph plot3.gph, ///
	  cols(1) rows (3) ysize(20) xsize(10) ///
	  title("Correct versus incorrect model specification", size(small))
```

{{< figure library="true" src="econometrics/06_Specification/Fig_01.png" >}}