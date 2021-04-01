---
# Title, summary, and page position.
linktitle: "Multivariate regressions"
weight: 2

# Page metadata.
title: Multivariate regressions
type: book  # Do not modify.

---

---

## What is a multivariate regression

### Multiple regressors

It is very unlikely that a dependent variable can be properly *explained* (in the econometrics sense) by a single regressor. In most cases, regression analyses will use several regressors.

For instance, let the price of houses be the dependent variable $(y_i)$. The price of houses obviously depends on its size. But, house prices also depends on other variables such as how old the house is, distance to highways, quality of the district high-school, location of the neighborhood, safety, and so on. Let $j = 0, ..., K$ be the number of regressors; then:

1. $x_0$: the constant term
2. $x_1$: size of the house,
3. $x_2$: age of the house,
4. $x_3$: distance to highways and public transportation,
5. $x_4$: high-school quality in the area,
6. $x_5$: neighborhood location,
7. $x_6$: safety.

In this case we have six regressors, which can be used to build the following theoretical linear relationship:

$$
y_i = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \beta_3 x_3 + \beta_4 x_4 + \beta_5 x_5 + \beta_6 x_6 + \varepsilon
$$

The estimated model will be:

$$
\hat{y_i} = \hat{\beta_0} + \hat{\beta_1} x_1 + \hat{\beta_2} x_2 +
\hat{\beta_3} x_3 + \hat{\beta_4} x_4 + \hat{\beta_5} x_5 + \hat{\beta_6} x_6
$$

Now, the expected (estimated) value of the house depends on value observed in a number of variables (size, age of the house, location, and so on). As long as the regressors included in the model are relevant to explain the price of a house, then this model will be more precise than a model with only one regressor.

We now moved from a model with $N$ observations and 1 variable, to a model with $N$ observations and $K$ regressors.

### Multiple coefficients ($betas$)

Since the model includes multiple regressors, the model also has multiple coefficients. Because of this, a word of caution is needed.

The temptation to compare the *size* of the $betas$ must be avoided. The fact that one coefficient is larger than another does not mean is more important than the other regressor, nor that that variable is having a larger effect on the dependent variable. There are two reasons why this type of comparison would be problematic.

The first one is that the size of the $betas$ depends on the unit of measure of the regressor. In the above example, the size of $\beta_1$ will be different if the size of the house is measured in units of squared foots or in hundreds of square foots. If you transform the size of the house from units into hundreds, then its coefficient will be hundred times smaller (for instance, it will fall from 200 to 2). Therefore, the relative size of the coefficient depends on what unit of measure is being used in the regressors.

The second reason is that a regressor attached to a $beta$ with a high value may depict very little variability, while another regressors with more varibility is attached to a $beta$ with a lower value. In other words, a high $beta$ may not produce much of an effect on $Y$ because its regressor hardly moves, while another $beta$ with a lower value is attached to a regressor that moves more. This is why you may want to consider not just the value of the $betas$, but the $betas$ times the standard deviation of its regressor: $\beta_i \sigma_{x_1}$.

### What is the meaning of the intercept ($\beta_0$)

The mathematical interpretation of $\beta_0$ is straightforward. It is the expected value of $y$ when **all** regressors are equal to zero $(x_1 = ... = x_6 = 0)$.

The conceptual, or economic, interpretation of $\beta_0$ is a little more challenging. In the above model, if all the regressors are zero, then a house with zero size located directly over a highway will have some positive expected value. This situation, of course, does not make sense. If the constant term has no economic meaning, what is its purpose? The issue is that $\beta_0$ includes several components of the regression model. Inside $\beta_0$ we have:

1. The true value of $\beta_0$ (which may or may not be equal to zero)
2. A *constant impact* of any specification error (such as if the equation of the model is wrong).
3. The mean of $\varepsilon$ conditional on your model being correctly specified.

We can translate this into simpler terms. Remember that OLS is fitting the line that minimizes the squared residuals. This line has two components, the *slope* of the line and its *level* (or intercept). OLS is not just about finding the right *slope*, is also about finding the right *vertical location* of the best line.

If you drop from the equation the constant term because it has no clear economic meaning, you run the risk of wrongly specifying your model. Dropping the constant term is forcing the model to find the best slope when the intercept is zero: $y_i = 0 + \beta_1 x_1 + \varepsilon$.

Another way to see that $\beta_0$ is to be included for *technical* reasons more than because of its economic interpretation is that in most cases, the domain of the value of the regressors does not include zero, therefore the constant term falls outside the region of relevant data of the regression (see the plot below). For instance, we know that there are no houses of zero size.

The effect of dropping the constant can be seen in the plot below. Let's use again the automobile information from the previous section and add to the scatter plot two regression lines. One with an estimated constant, and a second one with no constant.

```stata
*==============================================================================*
* ORDINARLY LEAST SQUARES
* Multivariate regression
* Code sample: 2.4
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and required data
set scheme s1color  // Set plot scheme
sysuse auto, clear  // Load 1978 Automobile Data from STATA

regress mpg weight, noconst
predict y_hat, xb
label variable y_hat "No constant"

*|CELL 2|----------------------------------------------------------------------*
*|Build scatter plots
twoway scatter mpg weight, ///
       mcolor(blue%50) ///
       xlabel(0(500)5000) ///
       ylabel(0(5)40) ///
       xlabel(, grid labsize(small)) xtitle(, size(small)) ///
       ylabel(, grid labsize(small)) ytitle(, size(small)) ///
     ||lfit mpg weight, ///
       lcolor(blue%50) ///
     ||line y_hat weight, ///
       lstyle(solid) lcolor(green%50) ///
       legend(position(6) rows(1) size(vsmall))

*==============================================================================*
*|THE END|=====================================================================*
*==============================================================================*
```

{{< figure library="true" src="econometrics/03_OLS/Fig_05.png" >}}

The blue dashed line is the best estimation possible with the given data, the one that minimizes the squared residuals by estimating both the constant and the slope of the fitted line. The green solid line is the estimation that drops the constant and only estimates the slope. As mentioned above, dropping the constant is telling the model you want the constant to be zero, therefore OLS will estimate the slope that minimizes the squared errors **conditional** on the constant being zero (if you project the green line all the way to the left it will cross the $(0, 0)$ point). In this example, the effect is not just a slightly different slope, but having the opposite sign. The best line has a negative slope, but by setting the constant to be zero now the model estimates a positive relationship between weight (lbs.) and mileage (mpg).

The reason to keep the constant in your model is not because of its economic interpretation, if it has any. The reason is that by having OLS the option to also estimate the constant it has more variables at its disposal to find the best line possible. The best line is constructed with **two** variables, *slope* and *intercept*.

{{% callout warning %}}
To be correctly specified, your model must include a constant term **even if** it does not have an economic interpretation
{{% /callout %}}

---

## Why do multivariate regression

The above discussion already points to a reason for preferring a multivariate regression over a univariate regression. We can have a better estimation of the dependent variable because we can use more data related to the price of houses. Mora regressors, in principle, allow to further minimize the squared residuals of the model. In the next section we will see in more detail how to *measure* the quality of the fitted line.

However, there are other two important reasons of why multivariate regression are preferred over univariate regression:

1. The role of control variables
1. To avoid the serious problem of omitted variable bias

### Control variables

Let's assume we run a univariate regression, where the price of houses is the dependent variable and the size of the house is the regressor. The model will find the best fit using this single regressor. However, the coefficient of the size of the house **does not capture** the *ceteris paribus* relationship between the price and size of houses.

The problem is that when OLS is looking at two houses, they may differ in variables other than price and size. Maybe one house is better located than the other, or maybe is closer to a highway. In other words, the regression is *implicitly* affected by changes in all **non-included** regressors.

To avoid this issue, the model must include *all* variables we want to hold constant, just as if we were in a chemistry lab. If we add a second regressor looking at the age of the house, then OLS can look at the impact of size on price *keeping the age of the house constant*. This is why regressors are also referred as **control variables**, because they control variations on other variables allowing to read a coefficient as the effect of its regressors *maintaining all other variables constant*. For the econometric model to be able to isolate the effect of the size of the house on its price keeping other variables constant (and the other way around), it needs to be able to match different sizes with same age to different prices. If the age of the house is not included in the model, then the data is missing and the model cannot isolate both effects.

{{% callout note%}}
A **multivariate regression** estimates the change in the dependent variable when there is a **one-unit** increase in a dependent variable *holding all other **included** regressors constant*.
{{% /callout %}}

We can split the regressors into two groups. On one side, those regressors of which we are interested in estimating their marginal effects (the coefficients). On the other side, those regressors which we have no interest in the value of their coefficients *per se*, but we need them in the model to serve as control variables such that we can properly interpret the coefficient of the variables of interest. Let $x_i$ denote four variables of interest and $z_j$ denote seven control variables. Then, the model can be represented the following way.

$$
y_i = \beta_0 + \underbrace{\beta_1 x_1 + ... + \beta_4 x_4}\_{\text{variables of interest}} + \underbrace{\gamma_1 z_1 + ... + \gamma_7 z_7}\_{\text{control variables}} + \varepsilon
$$

### Avoid omitted variable bias

Another very important reason to do multivariate regressions is to avoid having an **omitted variable bias**.

If an important variable is not included in the model, then the coefficient of the included regressors can be significantly biased. Again, this is because the included coefficient cannot hold the other regressors constant when estimating its value. A graphic illustration of this problem is the graph above. By omitting the *constant* term the slope gets biased to the point that the sign of the slope changes from negative to positive. Having an omitted variable bias means that you cannot trust the interpretation of the model because you must be forcing the line to be fitted the wrong way. Non included regressors are assumed to be zero and, just as with the constant, that can bias the estimated coefficients. Remember, any variable that is not included in the model implies assuming its coefficient is zero. If an omitted variable does not have a true coefficient of zero, then its effect will be mixed in the other coefficients. Therefore, the estimated betas may be seriously biased.

---

## Algebraic solution

### Matrix notation

The univariate regression example shows how to obtaing the $betas$ that minimize the squared errors. In the case of a multivariate regression a similar analytical solution would be highly impractical and, therefore, prone to error. [Matrix](https://en.wikipedia.org/wiki/Matrix_(mathematics)) algebra makes OLS solution (and econometrics in general) significantly easier. First, we need to introduce some notation.

Let **$y$** denote a $(N \times 1)$ column that includes all $N$ observations of the dependent variable. Note that now $y$ does not have the $i$ subscript (a simpler notation).

The **constant** and **all** $K$ regressors (controls and variables of interest) are now included in the $X$ matrix, which has a $N \times K$ dimension. The first column is the constant term, which is represented by all ones. This way, $\beta_0$ captures the whole value of the constant term. Columns 2 to $K$ capture all the remaining regressors.

There is subtle but important difference with our treatment so far. Previously, we talked about the *constant term plus the variables*. This is because, other than the constant, the value of each regressor value can change with each observation. Then, we have *regressors* and *variables*. The former are all the columns of the $X$ matrix including the constant term. The latter are the regressors which values can change, such as $x_1, ..., x_6$ in our previous example. In this sense, the number of regressors is $1 + \text{number of variables}$.

$$
\begin{align}
y_i &= \beta_0 + \underbrace{\beta_1 x_1 + ... + \beta_K x_K}\_{\text{variables}} + \varepsilon_i \\\\[10pt]
y_i &= \underbrace{\beta_0 + \beta_1 x_1 + ... + \beta_K x_K}\_{\text{regressors}} + \varepsilon_i
\end{align}
$$

Next we have a $N \times 1$ vector that includes all the coefficient of all the regressors $(\beta)$ (recall, including the constant).

Finally, the error term is also a $N \times 1$ vector that includes the error of each of the $N$ observations.

In matrix form, a regression with $K$ regressors can be written in the following simple form:

$$
y = X\beta + \varepsilon
$$

We can open the matrices to have glance of how data looks like in matrix form. Let us use the regressors in the house example above. Be careful of the following. For notation simplicity, now the first column of the $X$ matrix are all ones: $x_{1,1} = x_{2,1} = ... =x_{N,1} = 1$.

$$
\begin{pmatrix}
    y_1     \\\\
    y_2     \\\\
    y_3     \\\\
    \vdots  \\\\
    y_N
\end{pmatrix} =
\begin{pmatrix}
    1       & x_{1,2} & x_{1,3} & x_{1,4} & \cdots & x_{1,K}  \\\\
    1       & x_{2,2} & x_{2,3} & x_{2,4} & \cdots & x_{2,K}  \\\\
    1       & x_{3,2} & x_{3,3} & x_{3,4} & \cdots & x_{3,K}  \\\\
    \vdots  & \cdots  & \cdots  & \cdots  & \ddots & \vdots   \\\\
    1       & x_{N,2} & x_{N,3} & x_{N,4} & \cdots & x_{N,K}
\end{pmatrix}
\begin{pmatrix}
    \beta_0 \\\\
    \beta_1 \\\\
    \beta_2 \\\\
    \vdots  \\\\
    \beta_{K}
\end{pmatrix} + 
\begin{pmatrix}
    \varepsilon_1   \\\\
    \varepsilon_2   \\\\
    \varepsilon_3   \\\\
    \vdots          \\\\
    \varepsilon_N
\end{pmatrix}
$$

### Finding the coefficients

To find the OLS solution to the problem of minimizing the square residuals we proceed in a similar way than we did in the univariate regression. We start with squaring the residual and then we proceed to find the optimal $betas$.

1. Step 1: Find the residuals
2. Step 2: Square the residuals
3. Step 3: Find the FOC
4. Step 4: Find the $\hat{\beta}^{*}$

**Step 1**: Find the residuals

$$
\begin{align}
e &= y - \hat{y}    \\\\
e &= y - X\hat{\beta}
\end{align}
$$

**Step 2:**: Square the residuals

$$
\begin{align}
e^2 &= \left(y - X \hat{\beta} \right)' \left(y - X\hat{\beta} \right) \\\\
e^2 &= y'y - y'X \hat{\beta} - \hat{\beta}' X' y + \beta' X'X \beta
\end{align}
$$

**Step 3:** Proceed to obtain the FOC

$$
\begin{align}
\frac{\partial e^2}{\partial \hat{\beta}} &= -y'X - X'Y + 2 X'X \hat{\beta} = 0 \\\\
\frac{\partial e^2}{\partial \hat{\beta}} &= -2 X'Y + 2 X'X \hat{\beta} = 0
\end{align}
$$

**Step 4:** Find the optimal $betas$

$$
\hat{\beta}^{*} = \left( X'X \right)^{-1} \left( X'y \right)
$$

Note how much simpler and straightforward matrix algebra is with respect to the analytical approach we used in the univariate regression. $K$ can be small or very large, and yet the calculation to obtain the $betas$ will be the same. Also, note that for the $beta$ vector to exist, the inverse of $(X'X)$ must exist. This means that the $(X'X)$ matrix must be *full-rank*; an important topic in the issue of multicollinearity.
