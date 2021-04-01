---
# Title, summary, and page position.
linktitle: "Univariate regressions"
weight: 1

# Page metadata.
title: Univariate regressions
type: book  # Do not modify.
---



---

## What is Ordinary Least Squares (OLS)?

[OLS](https://en.wikipedia.org/wiki/Ordinary_least_squares) is the most common method to estimate the *parameters* of a **linear** regression such that the sum of the **squared errors** is minimized. In more general terms, OLS is one application of a group of [*linear least squares*](https://en.wikipedia.org/wiki/Linear_least_squares) methods.

Assume we want to estimate the linear relationship between mileage (mpg) $(y)$ of automobiles with respect to its weight $(x)$. The dependent variable is $y$ and $x$ is the regressor. Then, we are assuming that $y$ has a linear relationship with respect to its weight. Let $i = 1,...,N$ be the number of observations; that is, how many mileage and weight observations we have at our disposal. The theoretical representation of this relationship is the following:

$$
\begin{align}
mpg_n &= \beta_0 + \beta_1 weight_i + \varepsilon_i \\\\[10pt]
y_n   &= \beta_0 + \beta_1 x_i + \varepsilon_i
\end{align}
$$

The error term $(\varepsilon)$ is capturing random situations that would affect the mileage of the car, such as weather conditions, altitude, or roads with different inclinations. The error term is purely random and captures the variations of $y$ that cannot be explained by $x$. We can then split an econometric regression in two parts. A **deterministic** component (the constant plus the regressors) and a **stochastic** component (the error term). Because $y$ is modeled as a function of a deterministic and a random variable, $y$ is also a random variable: $y = f(x, e)$. There is an assymmetry in how variables are treated; while the dependent variable is assumed to be *stochastic*, the regressors are assumed to be *deterministic*.[^1]

We can also see that $\beta_1$ is the **marginal effect** of $x$ on $Y$: $\frac{\partial y}{\partial x} = \beta_1$.

Let's use the 1978 automobile dataset in `STATA` to illustrate how OLS works. The code below produces a [scatter plot](https://en.wikipedia.org/wiki/Scatter_plot) between mileage (mpg) and weight (lbs.) The dataset has 74 observations, therefore the scatter plot has 74 points as well (mileage-weight relationships).

```stata
*==============================================================================*
* ORDINARLY LEAST SQUARES
* Univariate regression
* Code sample: 2.1
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and required data
set scheme s1color  // Set plot scheme
sysuse auto, clear  // Load 1978 Automobile Data from STATA

*|CELL 2|----------------------------------------------------------------------*
*|Build scatter plots
twoway scatter mpg weight, ///
       mcolor(blue%50) ///
       xlabel(, grid labsize(small)) xtitle(, size(small)) ///
       ylabel(, grid labsize(small)) ytitle(, size(small))

*==============================================================================*
*|THE END|=====================================================================*
*==============================================================================*
```

{{< figure library="true" src="econometrics/03_OLS/Fig_01.png" >}}  

Looking at the scatter plot, we can imagine an infinite number of lines that can go through all those points. But, we are not looking for *any* line, we are looking for the line that would minimize deviations between a predicted mileage and the observed mileage when looking at the weight of a car. OLS is a method to find such line.

---

## The OLS method

### What is OLS doing

We need to find the values of $\beta_0$ and $\beta_1$ that would minimize prediction mistakes. Once we have estimated values for our $betas$, we can use the $weight$ data to predict $mileage$ with the smaller errors possible. The following equation shows the notation of the econometric model using the estimated parameter to predict values of the dependent variables (note the absence of $\varepsilon$).

$$ \hat{y_i} = \hat{\beta_0} + \hat{\beta_1} x_i $$

Before proceeding, is important to distinguish betweeen the **error (or disturbance)** term $(\varepsilon)$ and the **residual** $(e).$[^2]

{{% callout warning %}}
Do not confuse the [**error term** with the **residual**](https://en.wikipedia.org/wiki/Errors_and_residuals).

---
**The error $(\varepsilon)$ term**  
The *error* is the difference between the **expected** value of the dependent variable $(E[y])$ and a random observation $(y_i)$ taken from the sample: $\varepsilon_i = E[y] - y_i$. If the mean mileage of a car is 27 mpg and a randomly observed car has an mpg of 25, then the error is 2 mpg. A regression assumes these errors are random and make the dependent variable deviate from its mean (for instance random measurement errors).

**The residual $(e)$**  
The residual (or fitting deviation) is the difference between an observed value $(y_i)$ and a model's prediction $(\hat{y_i})$: $e_i = y_i - \hat{y_i}$. For instance, the observed mileage of a car is 27 mpg and the model predicts 23 mpg, then the residual is 4 mpg (the unexplained residue of the model). In this sense, the *residual* is an estimation of the unobservable *error*.
{{% /callout %}}

Our example has 74 observations. Given that the model can predict one $mpg$ for each car $weight$, there is one *residual* for each observation. Because $\hat{y_i} = \hat{\beta_0} + \hat{\beta_1} x_i$, we can see that

$$
\begin{align}
e_i &= y_i - \hat{y_i} \\\\[10pt]
e_i &= y_i - (\hat{\beta_0} + \hat{\beta_1} x_i)
\end{align}
$$

Yet, there is still a situation that requires a workaround. We can fit an infinite number of lines that will make the summation of all the *residuals* equal to zero $(\sum^{74}_{i=1} e_i = 0)$ (residuals cancel out). Canceling the residuals is not enough because only one of those infinite number of lines is the one we are looking for. To find the line we are looking for, OLS minimizes the **squared** residuals. We can now state the OLS problem in more precise terms:

$$
\operatorname*{min}_{\beta_{0},\beta_{1}} \sum_i e_i^2 = \operatorname*{min}_{\beta_{0},\beta_{1}} \sum_n (y_i - \hat{\beta_0} - \hat{\beta_1} x_i)^2
$$

Squaring the residuals has the following two attributes:

1. Allows to find a unique solution to the OLS problem.
2. It penalizes at a higher rate larger than smaller residuals.

The OLS estimation fits the *best* line through the points in the scatter plot. Where *best* is defined as minimizing the squared residuals constrained on the prediction being a straight line. The following `STATA` code adds the regression result to the scatter plot.

```stata
*==============================================================================*
* ORDINARLY LEAST SQUARES
* Univariate regression
* Code sample: 2.2
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and required data
set scheme s1color  // Set plot scheme
sysuse auto, clear  // Load 1978 Automobile Data from STATA

*|CELL 2|----------------------------------------------------------------------*
*|Build scatter plots
twoway scatter mpg weight, ///
       mcolor(blue%50) ///
       xlabel(2000(500)5000) ///
       ylabel(10(5)40) ///
       xlabel(, grid labsize(small)) xtitle(, size(small)) ///
       ylabel(, grid labsize(small)) ytitle(, size(small)) ///
     ||lfit mpg weight, ///
       lcolor(blue%50) ///
       legend(position(6) rows(1) size(vsmall))

*==============================================================================*
*|THE END|=====================================================================*
*==============================================================================*
```

{{< figure library="true" src="econometrics/03_OLS/Fig_02.png" >}}  

The dashed line plots the fitted line, that is, all the $\hat{y}$ values estimated by the regression. This line can be interpreted as the expected value of $y$ conditional on a given value of $x$. Because $e$ is random with zero mean $(E[\varepsilon]=0$), $E[y|x] = \hat{y}$.

We can use the same dataset to illustrate the importance of having a large and representative sample. The `STATA` code below splits the 74 observations in two random groups of 37 each. The figure shows how each sample, taken the same population, can lead to different regression results (because the code uses random values, your own result will not coincide with the one shown below)

```stata
*==============================================================================*
* ORDINARLY LEAST SQUARES
* Univariate regression
* Code sample: 2.3
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and required data
set scheme s1color  // Set plot scheme
sysuse auto, clear  // Load 1978 Automobile Data from STATA

*|CELL 2|----------------------------------------------------------------------*
*|Sort the dataset randomly
generate random = runiform()
sort random

generate id = _n <= 74/2

*|CELL 3|----------------------------------------------------------------------*
*|Build scatter plots
twoway scatter mpg weight if id==0, ///
	   mcolor(red%50) ///
	   xlabel(2000(500)5000) ///
	   ylabel(10(5)40) ///
	   xlabel(, grid labsize(small)) xtitle(, size(small)) ///
	   ylabel(, grid labsize(small)) ytitle(, size(small)) ///
	 ||lfit mpg weight if id==0, ///
	   lcolor(red%50) ///
	 ||scatter mpg weight if id==1, ///
	   mcolor(green%50) msymbol(O) ///
	 ||lfit mpg weight if id==1, ///
	   lcolor(green%50) ///
	   legend(off)
	   
*==============================================================================*
*|THE END|=====================================================================*
*==============================================================================*
```

{{< figure library="true" src="econometrics/03_OLS/Fig_03.png" numbered="true" title=" Scatter plot: Mileage versus Weight">}}  

The *true* relationship between the dependent variable and the regressors is unobservable. We must come up with an estimation. If our sample is large enough and of good quality then it is likely that we will have a good approximation to the true line. The figure below illustrates this situation. Color blue denotes the observable data. That is, the *sample* and the regression we can estimate from those data point. The green line shows the true and unobservable relationship in the whole *population*.

{{< figure library="true" src="econometrics/03_OLS/Fig_04.png" numbered="true" title=" Scatter plot: Mileage versus Weight and fitted line">}}  

### Algebraic solution

To find the $betas$ that minimize the sum of the squared residuals we proceed in a typical way:

1. Set the optimization problem.
2. Find the first order conditions (FOCs).
3. Solve the system of equations defined by the FOCs.
4. Confirm the silution is a minimum by checking the second order conditions (SOCs) (not included in this example)

**Step 1:** Set the optimization problem
$$ \operatorname*{min}_{{\beta_{0},\beta_{1}}} \sum_i (y_i - \hat{\beta_0} - \hat{\beta_1} x_i)^2 $$

**Step 2:** Find the FOCs
$$
\begin{align}
FOC_0: \frac{\partial \sum e^2}{\partial \hat{\beta_0}} &= -2 \sum (y_i - \hat{\beta_0} - \hat{\beta_1} x_i) = 0 \\\\[10pt]
FOC_1: \frac{\partial \sum e^2}{\partial \hat{\beta_1}} &= -2 \sum(y_i - \hat{\beta_0} - \hat{\beta_1} x_i) x_i = 0
\end{align}
$$

Note that the FOCs imply that the solution will also make the residuals cancel out $(\sum e = 0)$ (the term in parenthesis is $e$).

**Part 3:** Solve the system of equations defined by the FOCs.  
Get $\hat{\beta_0}$ from the first equation. Use the following property: $\sum x = N\bar{x}$ where $\bar{x} = \frac{1}{N} \sum x$.

$$
\begin{align}
-2 \sum (y_i - \hat{\beta_0} - \hat{\beta_1} x_i) &= 0 \\\\[10pt]
\sum (y_i - \hat{\beta_0} - \hat{\beta_1} x_i) &= 0 \\\\[10pt]
N \bar{y} - N \hat{\beta_0} - \hat{\beta_1} N \bar{x} &= 0 \\\\[10pt]
\hat{\beta_0} &= \bar{y} - \hat{\beta_1} \bar{x}
\end{align}
$$

Now replace $\hat{\beta_0}$ into the second equation.

$$
\begin{align}
-2 \sum (y_i - \hat{\beta_0} - \hat{\beta_1} x_i) x_i &= 0 \\\\[10pt]
\sum (y_i - \bar{y} + \hat{\beta_1} \bar{x} - \hat{\beta_1} x_i) x_i &=0 \\\\[10pt]
\sum y_i x_i - \sum \bar{y} x_i + \hat{\beta_1} \sum \bar{x} x_i - \hat{\beta_1} \sum x_i^2 &=0 \\\\[10pt]
\sum y_i x_i - \sum \bar{y} x_i + \hat{\beta_1} \left( \bar{x} x_i - \sum x_i^2 \right) &=0 \\\\[10pt]
\hat{\beta_1} &= \frac{\sum y_i x_i - \sum \bar{y} x_i}{\sum x_i^2 - \sum \bar{x} x_i} \\\\[10pt]
\hat{\beta_1} &= \frac{\sum y_i x_i - \bar{y} \sum x_i}{\sum x_i^2 - \bar{x} \sum x_i} \\\\[10pt]
\hat{\beta_1} &= \frac{\sum y_i x_i - N \bar{y} \bar{x}}{\sum x_i^2 - N \bar{x}^2} \\\\[10pt]
\hat{\beta_1}^* &= \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sum (x_i - \bar{x})^2}
\end{align}
$$

Now use the value of $\hat{\beta_1}$ to get the value of $\hat{\beta_0}$:

$$ \hat{\beta_{0}^{*}} = \bar{y} - \hat{\beta_{1}^{*}} \bar{x} $$

If we now replace $\hat{\beta_0}$ into the equation, we can express $\hat{y}$ as deviations from its mean when $x_i$ deviates from its own mean:

$$
\begin{align}
\hat{y}_i &= \hat{\beta_0} + \hat{\beta_1} x_i \\\\[10pt]
\hat{y}_i &= \left( \bar{Y} - \hat{\beta_1} \bar{x} \right) + \hat{\beta_1} x_i \\\\[10pt]
\hat{y}_i &= \bar{y} + \hat{\beta_1} (x_i - \bar{x})
\end{align}
$$

This last representation helps to understand that in econometrics, the word *explain* means how much of the change in the dependent variable is correlated with a change in a regressor. Meaning, how much of the dependent variable deviation from its own mean can be explained by a deviation of a regressor from its own mean.

This method has the following properties.:

1. Makes all residuals cancel out $(\sum e = 0)$.
1. Minimizes the squared residuals $(\sum e_n^2)$.
1. The fitted line passes through the sample means $(\bar{y}, \bar{x})$.
1. The mean value of $y$ equals the mean value of $\hat{y}$ (because $\sum (x_i - \bar{x}) =0$).

There is one more lesson to get from this excercise. As you can probably imagine, finding the optimal $betas$ can become increasingly complicated very fast as we add more regressors to the model. Matrix algebra (very common in econometrics) can make the mathematics of econometrics much simpler. An example of this simpler approach is included in the next section, where we solve the same problem for a regression with multiple regressors.

{{<icon name="file-excel" pack="fas" >}} {{% staticref "media/econometrics/03_OLS/OLS (simple example).xlsx" %}}Download OLS simple example.{{% /staticref %}}

---

## How useful are univariate regressions

Using a single regressor has very limited *practical* applications. Most regressions use several regressors in order to (1) achieve a better estimation of the dependent variable and (2) obtain a more accurate interpretation of the $betas$.

However, a univariate regression is very useful *pedagogically* because it offers a simple way to understand what a statistical software is doing behind the scenes when you run a regression. The most important lesson of this section is to understand what OLS is doing, and how it is doing it.

<!-- FOOTNOTES -->
[^1]: Of course, the regressors may also be stochastic variables. However, a regression **assumes** they are deterministic.

[^2]: A more precise exposition of the *error* and *residual* would be in conditional terms. For instance, the average mileage (mpg) of a car conditional on having a specific weight. Cars with different weights will have a random distribution of different mileage around their mean. The error term would be $Y_i - E[Y|x_i]$.
