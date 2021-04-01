---
# Title, summary, and page position.
linktitle: "Pure and impure heteroskedasticity"
weight: 1

# Page metadata.
title: Pure and impure heteroskedasticity
type: book  # Do not modify.
---

---

## What is heteroskedasticity

There is **heteroskedasticity** of the variance of the errors is not constant. Alternatively, there is **homoskedasticity** of the variance of the errors is constant.

* Homoskedasticity: $V[\varepsilon] = \sigma^2_{\varepsilon}$
* Heteroskedasticity: $V[\varepsilon] = \sigma^2_{\varepsilon, i}$

It the errors have the same variance regardless of the values of the regressors, then you have homoskedasticity. But, if the variance of the error **is not** independent of the values of the regressors, then your model has heteroskedasticity. Note the different notation above. The heteroskedastic errors have a subscript $i$ (number of observation) to denote that $\sigma%2_\varepsilon$ cs not constant.

If errors are homoskedastic, then their variance can be captured with a single number (a scalar) such as $\sigma^2_{\varepsilon}$. Heteroskedasticity means the model has a nonscalar variance matrix of errors. 

Consider each case below. Let $\Omega$ be a $N\times N$ variance of errors matrix.

> **Homoskedasticity**  
> $\Omega = \sigma^2_{\varepsilon} \mathcal{I}_{(N \times N)}$
>
> **Heteroskedasticity**  
> $\Omega =
>   \begin{pmatrix}
>       \sigma^2_{\varepsilon, 1} & & & \\\\
>       & \sigma^2_{\varepsilon, 2} & & \\\\
>       & & \ddots & \\\\
>       & & & \sigma^2_{\varepsilon, N}
>   \end{pmatrix}$

It is easier to see how heteroskedasticity looks like in a plot. The following `STATA` code builds four hypothetical heteroskedasticity scenarios, shown in <span style="color:red"> red</span>. Homoskedastic errors are shown in <span style="color:blue"> blue</span>.

```
* HETEROSKEDASTICITY
* Create homoskedastic and heteroskedastic errors
* Code sample: 7.1
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings
set scheme s1color  // Set plot scheme

*|CELL 2|----------------------------------------------------------------------*
*|Create X-axis and error variances
drop _all
set obs 100

gen   X = _n
label variable X "observation"
tsset X

gen var0 = 1
gen var1 = 1 + 0.05*X
gen var2 = 5 - 0.05*X
gen var3 = -(4/2500)*X^2 + (4/25)*X + 1
gen var4 =  (4/2500)*X^2 - (4/25)*X + 5

// Homoskedastic errors
gen errors00 = rnormal(0, var0)
gen errors01 = rnormal(0, var0)

// Heteroskedastic errors
gen errors11 = rnormal(0, var1)
gen errors12 = rnormal(0, var1)
gen errors21 = rnormal(0, var2)
gen errors22 = rnormal(0, var2)
gen errors31 = rnormal(0, var3)
gen errors32 = rnormal(0, var3)
gen errors41 = rnormal(0, var4)
gen errors42 = rnormal(0, var4)


*|CELL 3|----------------------------------------------------------------------*
*|Plot homoskedastic and heteroskedastic errors
   
twoway scatter errors00 errors01 errors11 errors12 X, ///
	   title("Homoskedastic and heteroskedastic errors", size(small)) ///
	   mcolor(blue%50 blue%50 red%50 red%50) ///
	   lcolor(blue%50 blue%50 red%50 red%50) ///
	   msize(vsmall vsmall vsmall vsmall) ///
	   ytitle("Errors", size(small)) ylabel(-10(2)10, labsize(small) grid) ///
	   xtitle("Observations", size(small)) xlabel(,labsize(small) grid) ///
	   yline(0, lcolor(black)) ///
	   legend(off)
	   
twoway scatter errors00 errors01 errors21 errors22 X, ///
	   title("Homoskedastic and heteroskedastic errors", size(small)) ///
	   mcolor(blue%50 blue%50 red%50 red%50) ///
	   lcolor(blue%50 blue%50 red%50 red%50) ///
	   msize(vsmall vsmall vsmall vsmall) ///
	   ytitle("Errors", size(small)) ylabel(-10(2)10, labsize(small) grid) ///
	   xtitle("Observations", size(small)) xlabel(,labsize(small) grid) ///
	   yline(0, lcolor(black)) ///
	   legend(off)

twoway scatter errors00 errors01 errors31 errors32 X, ///
	   title("Homoskedastic and heteroskedastic errors", size(small)) ///
	   mcolor(blue%50 blue%50 red%50 red%50) ///
	   lcolor(blue%50 blue%50 red%50 red%50) ///
	   msize(vsmall vsmall vsmall vsmall) ///
	   ytitle("Errors", size(small)) ylabel(-10(2)10, labsize(small) grid) ///
	   xtitle("Observations", size(small)) xlabel(,labsize(small) grid) ///
	   yline(0, lcolor(black)) ///
	   legend(off)
	   
twoway scatter errors00 errors01 errors41 errors42 X, ///
	   title("Homoskedastic and heteroskedastic errors", size(small)) ///
	   mcolor(blue%50 blue%50 red%50 red%50) ///
	   lcolor(blue%50 blue%50 red%50 red%50) ///
	   msize(vsmall vsmall vsmall vsmall) ///
	   ytitle("Errors", size(small)) ylabel(-10(2)10, labsize(small) grid) ///
	   xtitle("Observations", size(small)) xlabel(,labsize(small) grid) ///
	   yline(0, lcolor(black)) ///
	   legend(off)
```

{{< figure library="true" src="econometrics/08_Heteroskedasticity/Fig_01.png" >}}

{{< figure library="true" src="econometrics/08_Heteroskedasticity/Fig_02.png" >}}

{{< figure library="true" src="econometrics/08_Heteroskedasticity/Fig_03.png" >}}

{{< figure library="true" src="econometrics/08_Heteroskedasticity/Fig_04.png" >}}

---

## Pure heteroskedasticity

**Pure heteroskedasticity** is when the variance of the errors can be described as a function of the error. In other words, the errors are "naturally" heteroskedastic given the nature of the problem.

For instance, a correctly specified model may include a regressor with a large difference between small and large observations. There can be large disparities between income per capita between developed and developing countries. You can expect prediction errors to have a larger absolute value in developed countries than in developing countries.

The heteroskedastic errors can be divided in an homoskedastic component and a scaling factor: $\sigma^2_{\varepsilon, i} = \sigma^2_{\varepsilon} Z_i$.

---

## Impure heteroskedasticity

**Impure heteroskedasticity** is then errors are heteroskedastic because of specification error. An omitted variable will fall into the error term, and the data in that omitted regressor can make the errors **of the model** be heteroskedastic.

Fixing the specification error will make the errors be homoskedastic again. Assume the model omits regressor $K$, then:

$$
\varepsilon_i = \varepsilon + \beta_K x_{K, i}
$$