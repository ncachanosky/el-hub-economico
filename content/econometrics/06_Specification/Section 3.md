---
# Title, summary, and page position.
linktitle: "Dummy regressors"
weight: 3

# Page metadata.
title: Dummy regressors
type: book  # Do not modify.
---



---

## What are dummy variables

In some occasions it can be important to capture *categorical* (non-numerical) information. For instance, it may be of relevance to know the gender of an individual, or the race, or the nationality, or any other non-numeric (categorical) characteristic. Is there, for instance, any sort of discrimination in the labor market based on gender, race, or any other category?

Dummy variable allow the inclusion of non-numerical data into a regression by coding the characteristics of the data as either 1 (true) or 0 (false).

Dummy variables work as switches that move the fit of a regression from one category to the other. These switches can be in terms of (1) levels, (2) slopes, or (3) both.

---



## Level and slope effects

### Level effect

A dummy variable can be used to change the **intercept** of the fitted line **without** changing the slope across different categories. For instance, you hypothesize that US states with high levels of oil production have higher levels of income per capita *all else equal*. A dummy with value 1 (true) for each state with high level of oil production and 0 (false) for each state with low level of oil production *switches* the fitted line between *low* and *high* level of income.

Consider the following model:

$$
y = \beta_0 + \beta_1 x + \gamma D + \varepsilon
$$

Because $D$ can be either 0 or 1:

$$
y =
\begin{cases}
    \beta_0 + \beta_1 x + \varepsilon            & \quad \text{if } D=0 \\\\
    (\beta_0 + \gamma) + \beta_1 x + \varepsilon & \quad \text{if } D=1
\end{cases}
$$

Then, the intercept will be either $\beta_0$ or $\beta_0 + \gamma$ whether the dummy variable is 0 or 1.

### Slope effect

A dummy variable can also be used to change the **slope** of the fitted **without** changing the intercept line across different categories. This is done by interacting the dummy variable with the regressor you think has a different marginal effect across the different categories.

Consider the following model:

$$
y = \beta_0 + \beta_1 x + \gamma (xD) + \varepsilon
$$

Because $D$ can be either 0 or 1:

$$
y =
\begin{cases}
    \beta_0 + \beta_1 x + \varepsilon            & \quad \text{if } D=0 \\\\
    \beta_0 + (\beta_1 + \gamma) x + \varepsilon & \quad \text{if } D=1
\end{cases}
$$

### Level and slope effect

Both, level and slope effect, can be included in a model. Combine both of the above examples.

$$
y = \beta_0 + \beta_1 x + \gamma_0 D + \gamma_1 (xD) + \varepsilon
$$

Because $D$ can be either 0 or 1:

$$
y =
\begin{cases}
    \beta_0 + \beta_1 x + \varepsilon            & \quad \text{if } D=0 \\\\
    (\beta_0 + \gamma_0) + (\beta_1 + \gamma_1) x + \varepsilon & \quad \text{if } D=1
\end{cases}
$$

Dummy effects in a graph

The plots below depict (1) level, (2) slope, and (3) the combined effects of a dummy variable in a regression. Plots are built with the following `STATA` code.

```
*==============================================================================*
* MODEL SPECIFICATION
* Create a model misspecification
* Code sample: 5.2
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings
set scheme s1color  // Set plot scheme

*|CELL 2|----------------------------------------------------------------------*
*|Create X-axis and dummy variables
drop _all
set obs 100

gen   X = _n
label variable X "X"
tsset X

gen     D = 1
label   variable D "dummy"

*|Create dummy effects
generate Y1 = 10 + 0.5*X
label variable Y1 "Y (without dummy)"
generate Y1_dots = .
replace  Y1_dots = 10 + 0.5*X + rnormal(0,2) in 1/20
replace  Y1_dots = 10 + 0.5*X + rnormal(0,2) in 60/80

generate Y2 = (10 + 20*D) + 0.5*X
label variable Y2 "Y (with intercept dummy)"
generate Y2_dots = .
replace  Y2_dots = (10 + 20*D) + 0.5*X + rnormal(0,2) in 21/45
replace  Y2_dots = (10 + 20*D) + 0.5*X + rnormal(0,2) in 81/100

generate Y3 = 10 + (0.5 + D)*X
label variable Y3 "Y (with slope dummy)"
generate Y3_dots = .
replace  Y3_dots = 10 + (0.5 + D)*X + rnormal(0,2) in 21/45
replace  Y3_dots = 10 + (0.5 + D)*X + rnormal(0,2) in 81/100

generate Y4 = (10 + 20*D) + (0.5 + D)*X
label variable Y4 "Y (with slope and intercept dummy)"
generate Y4_dots = .
replace  Y4_dots = (10 + 20*D) + (0.5 + D)*X + rnormal(0,2) in 21/45
replace  Y4_dots = (10 + 20*D) + (0.5 + D)*X + rnormal(0,2) in 81/100

*|Create plots: Level effect
twoway line Y1 Y2 X, ///
	   title("Dummy level (intercept) effect", size(small)) ///
	   lcolor(blue%75 green%75) ///
	   xlabel(,labsize(vsmall)) ylabel(,labsize(vsmall)) ///
	   xtitle("X", size(vsmall))  ytitle("Y", size(vsmall)) ///
	   text(10 -4 "{&beta}{sub:0}", placement(w) size(vsmall) color(blue)) ///
	   text(30 -4 "{&beta}{sub:0}+{&gamma}", placement(w) size(vsmall) color(green)) ///
	   text(33 50 "slope: {&beta}{sub:1}", placement(e) size(vsmall) color(blue)) ///
	   text(53 50 "slope: {&beta}{sub:1}", placement(e) size(vsmall) color(green)) ///
	   legend(off) ///
	 ||scatter Y1_dots X, mcolor(blue%50) msize(vsmall) ///
	 ||scatter Y2_dots X, mcolor(green%50) msize(vsmall)

*|Create plots: Slope effect
twoway line Y1 Y3 X, ///
	   title("Dummy marginal (slope) effect", size(small)) ///
	   lcolor(black%75 black%75) ///
	   xlabel(,labsize(vsmall)) ylabel(,labsize(vsmall)) ///
	   xtitle("X", size(vsmall))  ytitle("Y", size(vsmall)) ///
	   text(10 -4 "{&beta}{sub:0}", placement(w) size(vsmall)) ///
	   text(33 50 "slope: {&beta}{sub:1}", placement(e) size (vsmall) color(blue)) ///
	   text(83 50 "slope: {&beta}{sub:1} + {&gamma}", placement(e) size (vsmall) color(green)) ///
	   legend(off) ///
	 ||scatter Y1_dots X, mcolor(blue%50) msize(vsmall) ///
	 ||scatter Y3_dots X, mcolor(green%50) msize(vsmall)
	   
*|Create plots: Level and slope effect
twoway line Y1 Y4 X, ///
	   title("Dummy level (intercept) and marginal (slope) effect", size(small)) ///
	   lcolor(blue%75 green%75) ///
	   xlabel(,labsize(vsmall)) ylabel(,labsize(vsmall)) ///
	   xtitle("X", size(vsmall))  ytitle("Y", size(vsmall)) ///
	   text(10 -4 "{&beta}{sub:0}", placement(w) size(vsmall) color(blue)) ///
	   text(30 -4 "{&beta}{sub:0}+{&gamma}", placement(w) size(vsmall) color(green)) ///
	   text(33 50 "slope: {&beta}{sub:1}", placement(e) size (vsmall) color(blue)) ///
	   text(103 50 "slope: {&beta}{sub:1} + {&gamma}", placement(e) size (vsmall) color(green)) ///
	   legend(off) ////
	 ||scatter Y1_dots X, mcolor(blue%50) msize(vsmall) ///
	 ||scatter Y4_dots X, mcolor(green%50) msize(vsmall) 
```


{{< figure library="true" src="econometrics/06_Specification/Fig_02.png" >}}


{{< figure library="true" src="econometrics/06_Specification/Fig_03.png" >}}


{{< figure library="true" src="econometrics/06_Specification/Fig_04.png" >}}

Each dummy variable consumes a degree of freedom, just like any other regressor. However, dummy variables allow using the information in the whole dataset rather than splitting the sample and having to run a different regression for each category with a smaller sample size.

---

## The dummy trap

The dummy trap is the accidental creation of a perfect linear combination of the constant term. If there are $n$ categories, then the model can include up to $n-1$ dummy variables.

Assume a model that looks at the GDP per capita in each US State. The model considers the possibility that their of state-specific conditions that can affect the level of income per capita. All else equal, being in Colorado yields in average a different level of income than, say, Louisiana. The model needs to pick one state as reference, and then define 49 dummy variables, one per each state. 

The constant is a column of ones. And because each dummy has 1 for each different states, the addition of all dummy variables produce the constant: $\sum D = \text{the constant}$. If your model falls into the dummy trap, then the inverse the model cannot calculate the coefficients because the inverse $(X'X)^{-1}$ does not exist.

{{% callout warning %}}
Avoid the **Dummy trap**

---

The dummy trap occurs when all dummy categories are included in the model, which produces a perfect linear combination with the constant term.

A model with a dummy trap cannot estimate the coefficients because the data matrix $(X'X)^{-1}$ does not exist.

{{% /callout %}}

---

## Example: The Gender Wage Gap

Consider the issue of the *gender wage gap* as an example of using dummy variables. In the United States, in **average**, women are paid around 80 cents per dollar with respect to men.

There are many possible explanations of this difference. Discrimination is one of them. However, economic reasoning raises doubts about the discrimination argument for the gender wage gap. If hiring women is 20-percent cheaper than hiring men, why don't firms just hire women and increase their profits? Employing women instead of men would reduce the gender wage gap to the point where wages among women and men are equal.

The following model compares the average wage $(w)$ of men and women.

$$
w = \beta_0 + \gamma D + \varepsilon
$$

where $D = 0$ if men and $D = 1$ if women. In this equation, $\beta_0$ is the wage of men, and $\beta_0 + \gamma$ is the wage of women. 

A value of $\gamma = 0$ means that, in **average**, men and women are paid the same. A value of $\gamma < 0$ indicates that, in **average**, men are paid more than women. And a value of $\gamma > 0$ indicates that, in **average**, women are paid more than men.

This model, however, is missing something very important: control variables. It is possible that men and women have, in average, different job, therefore they will have, in average, different pay, and still be the case that all else equal, men and women are paid the same.

For instance, in average men may be more inclined than women to work in high risk jobs, such as being a fishermen in Alaska. In average, men may be more inclined to work extra hours or travel for work (spend less times with family, relatives, and friends). If you are a lawyer in a murder case, you don't get to go home until the work is done, a person's life is in your hands. If you are lawyer dealing with a multimillion lawsuit, you don't get to take a break until the case is done. These labor demands are paid extra than a job that has regular working hours with low demands outside its regular hours.

A complete model will include a list of other variables that affect the wage. As an example, consider the following list:

1. $D$: Gender (male or female)
2. $x_1$: Years of experience
3. $x_2$: Willingness to travel
4. $x_3$: Willingness to work extra hours
5. $R$: Risk level of the job
6. $I_j$: $j = 1, ..., J$ dummy variables for different industry classifications
7. $E_q$: $q = 1, ..., Q$ dummy variables for different degree fields

The above list is incomplete, but it illustrates the point. A complete model must look at **all** wage determinants before concluding that because there is a gender wage gap (in average) there is gender discrimination in the labor market. Using our example, a complete model will look like the following:

$$
w = \beta_0 + \gamma D + \underbrace{\sum_{i=1}^3 \beta_i x_i + \rho R + \sum_{j=1}^J \theta_j I_j + \sum_{q=1}^Q \eta_q E_q}_{\text{control variables}} + \varepsilon
$$

Now the estimated value of $\gamma$ is comparing pay between men and women keeping all your control variables constant. When control variables are included in the model, the gender wage gap is estimated to fall from 0.80 cents per dollar to 0.95 cents per dollar. The 5-percent difference can be to a number of reasons such as:

1. Discrimination
2. Statistical error (we can't tell whether wages are actually different)
3. An omitted variable

There is one more issue to consider from the above discussion. The gender wage gap is looking at monetary pay in exchange of work. However, there are also nonmonetary compensation. Typical compensations include benefit such as health insurance coverage or vacation time. However, a lower paid job can have the benefit of being more safe, free from having to work extra hours, and other labor-demands. In summary, high risk and high stressful job have to pay premium to compensate for less nonmonetary benefits of the job.

{{< figure library="true" src="econometrics/06_Specification/Fig_05.png" >}}