---
# Title, summary, and page position.
linktitle: "Running your first regression"
weight: 4

# Page metadata.
title: Running your first regression
type: book  # Do not modify.
---

---

This section walks you through running your first regression. There are two issues to pay attention in this exercise. One is the *technical* discussion of how to run a regression and how to read the results. The other one is to pay attention to the *subjective* interpretations of the econometrician. For instance, how a model should be built and what are the results saying to us? A discussion and interpretation of a regression results is part of the econometric exercise as well.

The exercise follows the following steps:

1. Organize and clean your data
2. Familiarize yourself with your data
3. Define your models
4. Run your regressions
5. Evaluate the quality of the models

---

## Organize and clean your data

Consider first **how** is your data is stored. If you are working with `STATA`, or any other statistical package, you may be lucky and have access to the data already in your software format. In that case, all you need to do is load the file to your software. STATA data files have the `.dta` extension.

However, it is possible that data is stored in a more general format, just as `.csv` or Excel file, so that it can be used in different platforms. Unless the data you need is already in a dataset, you will have to create your own dataset. If that is the case, you may want to consider *how* you organize your data.

Let us use an hypothetical example. Assume you are looking at data for the 50 U.S. states.

Data is usually organized the following way. Regressors are columns and rows are observations. In addition, you know you have three types of variables: (1) the **dependent** variable $(y)$, (2) your regressors **of interest** $(x_i)$, (3) and your **control** variables $(z_j)$. When building your dataset, you may want to start with some metadata such as the observation number and the U.S. state. This metadata helps to navigate the information. Then you can identify (with borders or different colors) your dependent variable. To the right your dependent variable you can have your variable(s) of interest. Finally, the last set of columns can be your control variables. You may also want to consider other *format* edits that will facilitate your reading of the data such as number of decimals, or horizontal lines every a few observations, and so on).

The figure below is an example of how a user-friendly dataset in Excel may look like. You can also download a copy of the Excel file.

{{< figure library="true" src="econometrics/03_OLS/Fig_09.png" >}}

{{<icon name="file-excel" pack="fas" >}} {{% staticref "media/econometrics/03_OLS/Dataset format example.xlsx" %}}Download Excel sample file.{{% /staticref %}}

A user-friendly format of your dataset is important because you may need to do some data exploration at some point in your regression exercise. Maybe you need to clean up some typos, or identify outliers and missing values, and so on. If you need to go back to the original file, then you want the information in that file to be as easy to read and navigate as possible. It is also a good gesture towards third-parties using your dataset as well.

Besides thinking of a format that would facilitate the visual navigation of the file, you also want to think what number formats can produce errors when importing an `Excel` or `.csv` file into your statistical software. You will learn what to be careful about with experience and use of your statistical software of choice. Just to give a couple of examples. If the first column has the regressor's names, then you may need to avoid `spaces` and resort to `underscores` (for instance, `Variable_1` instead of `Variable 1`). Another potential issue may the use of thousand delimiter (use `10000` instead of `10,000`). Different statistical software may read data differently. Finding out about these errors would probably be a process o trial and error.

The following `STATA` code produces all the output shared below.

```
*==============================================================================*
* ORDINARLY LEAST SQUARES
* Running your first regression
* Code sample: 2.5
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and required data
ssc install estout, replace
set scheme s1color  // Set plot scheme
sysuse auto, clear  // Load 1978 Automobile Data from STATA


*|CELL 2|----------------------------------------------------------------------*
*|Produce statistical summary

global    regressors mpg weight length rep78 headroom trunk
summarize price $regressors


*|CELL 3|----------------------------------------------------------------------*
*|Produce correlation matrix
correl price $regressors


*|CELL 4|----------------------------------------------------------------------*
*|Produce scatter plots

twoway scatter price mpg, ///
        mcolor(blue%50) ///
        xlabel(10(5)45) ///
        ylabel(2000(4000)16000) ytitle("Price") ///
        xlabel(, grid labsize(small)) xtitle(, size(small)) ///
        ylabel(, grid labsize(small)) ytitle(, size(small)) ///
               text(15400 22.5 "Outlier?", color(blue%75) justification(left)) ///
     ||lfit price mpg, ///
        lcolor(blue%75) ///
        legend(off)


twoway scatter price weight, ///
        mcolor(red%50) ///
        xlabel(1500(500)5000) ///
        ylabel(2000(4000)16000) ytitle("Price") ///
        xlabel(, grid labsize(small)) xtitle(, size(small)) ///
        ylabel(, grid labsize(small)) ytitle(, size(small)) ///
     ||lfit price weight, ///
        lcolor(red%50) ///
        legend(off)


twoway scatter price length, ///
        mcolor(green%50) ///
        xlabel(125(25)250) ///
        ylabel(2000(4000)16000) ytitle("Price") ///
        xlabel(, grid labsize(small)) xtitle(, size(small)) ///
        ylabel(, grid labsize(small)) ytitle(, size(small)) ///
     ||lfit price length, ///
        lcolor(green%50) ///
        legend(off)


*|CELL 5|----------------------------------------------------------------------*
*|Run base model

regress price $regressors, ///
		cformat(%9.2f) ///
		pformat(%9.4f)


*|CELL 6|----------------------------------------------------------------------*
*|Run all models

quietly regress price $regressors
        estimates store M1, title (Model 1)
        predict resid1, residuals
        predict y_hat1, xb

quietly regress price mpg weight rep78 headroom trunk
        estimates store M2, title (Model 2)
        predict resid2, residuals
        predict y_hat2, xb

quietly regress price mpg weight headroom trunk
        estimates store M3, title (Model 3)
        predict resid3, residuals
        predict y_hat3, xb

quietly regress price mpg length rep78 headroom trunk
        estimates store M4, title (Model 4)
        predict resid4, residuals
        predict y_hat4, xb

quietly regress price mpg length headroom trunk
        estimates store M5, title (Model 5)
        predict resid5, residuals
        predict y_hat5, xb


estout M1 M2 M3 M4 M5, title(Robustness check) ///
       collabels(none) ///
       mlabels(, titles) ///
       cells(b(star fmt(3)) se(par fmt(2))) legend ///
       label varlabels(_cons Constant) ///
       stats(df_r r2 r2_a rmse aic bic, fmt(0 3 3 0 0 0) ///
             label(DF R2 adj-R2 RMSE AIC BIC))


*|CELL 7|----------------------------------------------------------------------*
*|Build the residuals' plots

quietly{
* Residuals model 1
twoway scatter price mpg, nodraw saving(model1_resid1, replace) ///
          msize(small) mcolor(blue%50) ///
          xlabel(10(5)45) ///
          ylabel(2000(4000)16000) ytitle("Price") ///
          xlabel(, grid labsize(small)) xtitle(, size(small)) ///
          ylabel(, grid labsize(small)) ytitle(, size(small)) ///
     ||scatter y_hat1 mpg, ///
          msize(small) mcolor(red%50) ///
          legend(label(1 "Observation") label(2 "Estimation") ///
                 size(small) region(lstyle(none))) 

twoway scatter resid1 mpg, nodraw saving(model1_resid2, replace) ///
          msize(small) mcolor(red%50) ///
          xlabel(10(5)45) ///
          ylabel(-6000(2000)6000) ///
          ytitle("Residuals, model 1") ///
          yline(0, lstyle(foreground)) ///
          xlabel(, grid labsize(small)) xtitle(, size(small)) ///
          ylabel(, grid labsize(small)) ytitle(, size(small))

histogram resid1, nodraw saving(model1_resid3, replace) ///
          start(-8000) color(red%50) normal normopts(lcolor(black%75)) ///
          xtitle(, size(small)) ytitle(, size(small)) ///
          ylabel(, grid labsize(small) angle(0)) ///
          xlabel(, grid labsize(small))

graph combine model1_resid1.gph model1_resid2.gph model1_resid3.gph, ///
              cols(1) ysize(10) title("Model 1: Residuals", size(small))
}

* Residuals model 2
quietly{
twoway scatter price mpg, nodraw saving(model2_resid1, replace) ///
          msize(small) mcolor(blue%50) ///
          xlabel(10(5)45) ///
          ylabel(2000(4000)16000) ytitle("Price") ///
          xlabel(, grid labsize(small)) xtitle(, size(small)) ///
          ylabel(, grid labsize(small)) ytitle(, size(small)) ///
     ||scatter y_hat2 mpg, ///
          msize(small) mcolor(red%50) ///
          legend(label(1 "Observation") label(2 "Estimation") ///
                 size(small) region(lstyle(none)))

twoway scatter resid2 mpg, nodraw saving(model2_resid2, replace) ///
          msize(small) mcolor(red%50) ///
          xlabel(10(5)45) ///
          ylabel(-6000(2000)6000) ///
          ytitle("Residuals, model 1") ///
          yline(0, lstyle(foreground)) ///
          xlabel(, grid labsize(small)) xtitle(, size(small)) ///
          ylabel(, grid labsize(small)) ytitle(, size(small))

histogram resid2, nodraw saving(model2_resid3, replace) ///
          start(-8000) color(red%50) normal normopts(lcolor(black%75)) ///
          xtitle(, size(small)) ytitle(, size(small)) ///
          ylabel(, grid labsize(small) angle(0)) ///
          xlabel(, grid labsize(small))

graph combine model2_resid1.gph model2_resid2.gph model2_resid3.gph, ///
              cols(1) ysize(10) title("Model 2: Residuals", size(small))
}

* Residuals model 3
quietly{
twoway scatter price mpg, nodraw saving(model3_resid1, replace) ///
          msize(small) mcolor(blue%50) ///
          xlabel(10(5)45) ///
          ylabel(2000(4000)16000) ytitle("Price") ///
          xlabel(, grid labsize(small)) xtitle(, size(small)) ///
          ylabel(, grid labsize(small)) ytitle(, size(small)) ///
     ||scatter y_hat3 mpg, ///
          msize(small) mcolor(red%50) ///
          legend(label(1 "Observation") label(2 "Estimation") ///
                 size(small) region(lstyle(none)))

twoway scatter resid3 mpg, nodraw saving(model3_resid2, replace) ///
          msize(small) mcolor(red%50) ///
          xlabel(10(5)45) ///
          ylabel(-6000(2000)6000) ///
          ytitle("Residuals, model 1") ///
          yline(0, lstyle(foreground)) ///
          xlabel(, grid labsize(small)) xtitle(, size(small)) ///
          ylabel(, grid labsize(small)) ytitle(, size(small))

histogram resid3, nodraw saving(model3_resid3, replace) ///
          start(-8000) color(red%50) normal normopts(lcolor(black%75)) ///
          xtitle(, size(small)) ytitle(, size(small)) ///
          ylabel(, grid labsize(small) angle(0)) ///
          xlabel(, grid labsize(small))

graph combine model3_resid1.gph model3_resid2.gph model3_resid3.gph, ///
              cols(1) ysize(10) title("Model 3: Residuals", size(small))
}

* Residuals model 4
quietly{
twoway scatter price mpg, nodraw saving(model4_resid1, replace) ///
          msize(small) mcolor(blue%50) ///
          xlabel(10(5)45) ///
          ylabel(2000(4000)16000) ytitle("Price") ///
          xlabel(, grid labsize(small)) xtitle(, size(small)) ///
          ylabel(, grid labsize(small)) ytitle(, size(small)) ///
     ||scatter y_hat4 mpg, ///
          msize(small) mcolor(red%50) ///
          legend(label(1 "Observation") label(2 "Estimation") ///
                 size(small) region(lstyle(none)))

twoway scatter resid4 mpg, nodraw saving(model4_resid2, replace) ///
          msize(small) mcolor(red%50) ///
          xlabel(10(5)45) ///
          ylabel(-6000(2000)6000) ///
          ytitle("Residuals, model 1") ///
          yline(0, lstyle(foreground)) ///
          xlabel(, grid labsize(small)) xtitle(, size(small)) ///
          ylabel(, grid labsize(small)) ytitle(, size(small))

histogram resid4, nodraw saving(model4_resid3, replace) ///
          start(-8000) color(red%50) normal normopts(lcolor(black%75)) ///
          xtitle(, size(small)) ytitle(, size(small)) ///
          ylabel(, grid labsize(small) angle(0)) ///
          xlabel(, grid labsize(small))

graph combine model4_resid1.gph model4_resid2.gph model4_resid3.gph, ///
              cols(1) ysize(10) title("Model 4: Residuals", size(small))
}

* Residuals model 5
quietly{
twoway scatter price mpg, nodraw saving(model5_resid1, replace) ///
          msize(small) mcolor(blue%50) ///
          xlabel(10(5)45) ///
          ylabel(2000(4000)16000) ytitle("Price") ///
          xlabel(, grid labsize(small)) xtitle(, size(small)) ///
          ylabel(, grid labsize(small)) ytitle(, size(small)) ///
     ||scatter y_hat5 mpg, ///
          msize(small) mcolor(red%50) ///
          legend(label(1 "Observation") label(2 "Estimation") ///
                 size(small) region(lstyle(none)))

twoway scatter resid5 mpg, nodraw saving(model5_resid2, replace) ///
          msize(small) mcolor(red%50) ///
          xlabel(10(5)45) ///
          ylabel(-6000(2000)6000) ///
          ytitle("Residuals, model 1") ///
          yline(0, lstyle(foreground)) ///
          xlabel(, grid labsize(small)) xtitle(, size(small)) ///
          ylabel(, grid labsize(small)) ytitle(, size(small))

histogram resid5, nodraw saving(model5_resid3, replace) ///
          start(-8000) color(red%50) normal normopts(lcolor(black%75)) ///
          xtitle(, size(small)) ytitle(, size(small)) ///
          ylabel(, grid labsize(small) angle(0)) ///
          xlabel(, grid labsize(small))

graph combine model5_resid1.gph model5_resid2.gph model5_resid3.gph, ///
              cols(1) ysize(10) title("Model 5: Residuals", size(small))
}

* Compare scatter of residuals
twoway scatter resid1 mpg, msize(vsmall) mcolor(blue%50) ///
          yline(0, lstyle(foreground)) ///
          xlabel(10(5)45,         grid labsize(small)) ///
          ylabel(-8000(2000)8000, grid labsize(small) angle(0)) ///
          xtitle(, size(small)) ytitle(, size(small)) ///
     ||scatter resid2 mpg, msize(vsmall) mcolor(green%50) ///
     ||scatter resid3 mpg, msize(vsmall) mcolor(yellow%50) ///
     ||scatter resid4 mpg, msize(vsmall) mcolor(teal%50) ///
     ||scatter resid5 mpg, msize(vsmall) mcolor(gray%50) ///
           legend(rows(2) size(small) region(lstyle(none)) ///
                  label(1 "Residuals (model 1)") ///
                  label(2 "Residuals (model 2)") ///
                  label(3 "Residuals (model 3)") ///
                  label(4 "Residuals (model 4)") ///
                  label(5 "Residuals (model 5)"))

graph combine model1_resid3.gph model2_resid3.gph model3_resid3.gph ///
              model4_resid3.gph model5_resid3.gph, ///
              cols(1) ysize(20) xsize(10) ///
              title("Residual histogram: All models", size(small))


*==============================================================================*
*|THE END|=====================================================================*
*==============================================================================*
```

---

## Familiarize yourself with the data

Let us use the *auto* dataset in `STATA` and assume we want to study the price of cars $(y)$ as a function of mileage (mpg) $(x)$. For this, we have a dataset with a number of variables. Our first step, once we have data ready to use, it so get as familiar as possible how the data looks like. This familiarity is usually a prerequisite of a good econometric analysis.

### Statistical summary

Statistical summaries are a first approach to see know your data. This is particularly useful in very large datasets where a detailed view of the whole information may not be feasible or practical.

The following table provides the number of available observations for each regressor (each column), the mean, standard deviation, and minimum and maximum values.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 01.png" >}}

Recall that an econometric regression *explains* variations. That is, how much of the variations of $y$ around its mean can be explained by variations of the regressors around their means. A **regressor** with low standard deviation (in relation to the mean) suggests that such variable may not have much explanatory power (its behavior is similar to that of the constant). On the other hand, a **dependent** variable with a low standard deviation (in relation to its mean) suggests that there is not much to *explain* in that variable.

### Correlation matrix

A summary statistics table provides some information about each variable, but does not provide information of how are they related. Our next step is to look at the correlation matrix of all the variables.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 02.png" >}}

Looking at the table, we see that `weight` and `length` are the two variables more positively correlated with your dependent variable, `price`. For some reason, seems that the higher `mileage` (mpg) the lower the price, when in principle we would expect the opposite (can you think of a reason?) But, we should not jump to conclusions because it is also the case that `mileage` is highly negatively correlated with `weight` and `length`. We need a full regression to estimate the marginal and controlled effect of `mileage` on the `price` of the cars.

A correlation matrix is a first look at which variables have a positive or negative relationship and how strong is that relationship. It can provide the first clues on how regressors are related to each other and the dependent variable.

### Scatter plots

After looking at the correlation matrix, you suspect that `weight` and `legnth` may be good candidates for your regression. These are likely to be good control variables because the `mileage` of a car is not independent of its `weight` or `length`. Let's look, then, at three scatter plots, one for each regressor with respect to the dependent variable.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 03.png" >}}

{{< figure library="true" src="econometrics/03_OLS/OLS Example 04.png" >}}

{{< figure library="true" src="econometrics/03_OLS/OLS Example 05.png" >}}

The scatter plots reflect the negative and positive slopes you saw in the correlation matrix. Look at the first plot, where there seems to be an [outlier](https://en.wikipedia.org/wiki/Outlier). Is that point accurate or is there a typo in your source? If the data is correct, then you need to decide if you want to keep this observation in your regression or not. The answer to that questions depends on what information you want to extract from your regression. You want to capture the relatonship of the whole sample or you want an estimation of the relationship of *normal* (average) cars?

Look now at the second and third scatter plots. You can see that to the left side of the graph, dots are closer to the fitted line than dots to the right side of the graph. We will get back to this issue in a later chapter. However, the looks of these scatter plots suggest that, for `weight` and `length`, the accuracy of the model prediction is not even. A univariate model would be more accurate for lighter and shorter cars than would be for heavier and longer cars.  

---

## Define and run your models

Having now an impression of how the data looks like, we can develop our regression models. Remember our objective, to find the relationship between `price` and `mileage`. We know, however, that we also need control variables if we want to obtain an unbiased estimation.

There are different models, using different combinations of regressors, we can think of. To navigate through them we are going to build a base model and then run different specifications for **robustness checking**. Remember that every regressor we add to the model contributes with new information but also consumes a degree of freedom. It is important to see of all models provide, more or less, similar results. If this is not the case, you may have to explore potential problems with your model (next chapters).

The relevant question is what other variables have an effect on the `price` of cars besides its `mileage`. These are the variables we cannot forget in our model. `Mileage` is clearly important, but so is the car' (1) weight, (2) length, (3) how many repairs it had since 1978, (4) its headroom, and (5) the trunk size. Our base model, then, has a total of one variable of interest $(x)$ and 5 control variables ($z_1, ..., z_5)$:

$$
y_i = \beta_0 + \beta_1 x_i + \gamma_1 z_{1,i} + \gamma_2 z_{2,i} + \gamma_3 z_{3,i} + \gamma_4 z_{4,1} + \gamma_5 z_{5,1} + \varepsilon_i
$$

Before discussing different versions of the base model, let us run this regression in `STATA` and see what output we get. There is plenty of information to see, and we are still able to read all the calculations. Nonetheless, we can start by learning how to read what we have seen so far. Below is a typical regression output.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 06.png" >}}

The estimation of the model is in the second table. The header's row shows `price` as the dependent variable. The regressors are located below (in the same order used in the code) with the constant (`_const`) at the end. The second row shows the $betas$. In this model, for instance, a change of one unit in the `mileage` (mpg) explains, **in average**, a fall of 101.4388 units in the `price` variable. We will discuss how to read the other columns to the right as we move through the next chapters. But you are already familiar with the last two columns, which are the limits of a 95% confidence interval for each coefficient. The coefficients of the output say our base model looks the following way (allowing for rounding):

$$
\hat{y_i} = 12,266 - 101.44 x_i + 4.95 z_{1,i} - 112.41 z_{2,i} + 889.67 z_{3,1} - 652.13 z_{4,i} + 80.29 z_{5,i}
$$

We can now look at the data above the coefficient's table. The first information that appears to the left is the [partition of sum of squares](https://econ-lecture-notes.netlify.app/econometrics/03_ols/section-3/#partition-of-sum-of-squares). We have $ESS$ (model), $RSS$ (residual), and $TSS$ (total) respectively. You can see that $model + residual = total$. 

On the right side you can find some regression evaluations. You have the total number of observations $(N=69$), the $R^2$, the $\bar{R}^2$, and the $RMSE$. You can see that $R^2 = \frac{model}{total}$. Finally, note that $\bar{R}^2 < R^2$.

We do not know, yet, if our base model is the best one. This model is just our first guess. We need to look at the output, data information, and think if a different model specification may produce a better outcome.

Have a look at the correlation matrix. We see that both `weight` and `length` are correlated with `price`, and therefore we probably want them in our model as controls. However, `weight` and `length` have a high positive correlation of 0.9478. These two variables have a very similar behavior. Maybe we do not need both in the model since we may be duplicating the information (a problem will discuss later as *multicollinearity*). We can run two more regressions, one with `weight` and the other one with `length`. Since both variables move so similarly, maybe we can save a degree of freedom by having only one of those two variables. It is possible that the $\bar{R}$ will increase. We have now **three** models in total.

Looking at the summary statistics and correlation matrix you also wonder about whether reparations since 1978 (`rep78`) should be included in the model. This variable has a very low correlation with `price` and what seems to be a low standard deviation. You can't be sure what the impact of this regressor is in the model until you try. Therefore, to complete the robustness check, we will run other two models, with and without `rep78` for each one of the two above specifications.

To make it easier to compare all these models, it is customary to put all of them in one table next to each other. This is what we have in the output below.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 07.png" >}}

---

## Evaluate the quality of your models

There are a number of issues to pay attention to. Look **first** at how some coefficients significantly change in value, such as `mileage`, `length`, `trunk`, and even the `constant`. Some of them even change their sign. This illustrates the importance of evaluating a regression and thinking about which one makes economic sense in order to get the more accurate coefficient estimation. This variance in the estimated coefficients is also a typical indicator of *multicollinearity* in the regressors, which we do not know yet how to assess and deal with.

**Second**, look at the bottom part of the table. You can see the degrees of freedom for each model as well as information about the quality of the model. Consider the $R^2$ information. As expected, the model with more regressors has the higher $R^2$. It also happens to have the higher $\bar{R}^2$. Compare, however, the $\bar{R}^2$ of models 3 and 4. Model 3 has less regressors than model 4, and yet has a higher $\bar{R}^2$.

**Third**, look at $RMSE$. According to this measure, model 1 is also the best choice.

**Fourth**, there is the information criteria measures of $AIC$ and $BIC$. According to these measures, Model 1 is also the best model. But, not by much with respect to Model 2.

**Fifth**, we should also look how the residuals of the model look like. A good looking normal distribution of the residuals is also a good sign.

### Looking at the residuals

We can look at the residuals of each of the five models in three different ways:

1. Compare the observable $y_i$ with the predicted $\hat{y_i}$.
2. Look how the residuals are distributed around our variable of interest, `mileage` (mpg).
3. Compare the residual's distribution with a normal distribution.

Below are the five sets of plots with the residuals for each one of the five models. The **first** plot shows in the observed $y_i$ in <span style="color:blue">**blue**</span> and the predicted values $\hat{y_i}$ in <span style="color:red">**red**</span>. The **second** plot shows the location of the residuals around `mileage`. The vertical axis shows a *zero* because we are looking at estimation errors (that cancel out). The **third** plot shows the histogram of the residuals along a normal distribution. You need to spend some time looking and comparing these plots.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 08.png" >}}


{{< figure library="true" src="econometrics/03_OLS/OLS Example 09.png" >}}

{{< figure library="true" src="econometrics/03_OLS/OLS Example 10.png" >}}

{{< figure library="true" src="econometrics/03_OLS/OLS Example 11.png" >}}

{{< figure library="true" src="econometrics/03_OLS/OLS Example 12.png" >}}

The first two plots for each model can help identify a number of issues, such as an omitted relevant regressors. Once you can identify in your friendly-looking dataset which observations have the larger residuals, you may be able to recognize a pattern. Such pattern can reflect a missing variable. For instance, the `mileage` of sport sedans is different than non-sport sedans. Therefore, adding a regressor that takes into account the type of car can improve the overall fitting of the model and minimize biases in the coefficient of other regressors. Residual evaluation is an exploratory exercise, and how you read the data in front of you depends on your knowledge of the subject as well as on your subjective intuition.

The third plot for each model compares the distribution of the residuals with a normal distribution. We have not seen yet how to run a formal test of normality. However, visual inspection seems to confirm that Model 1 is offers the best from all of your five specifications.

Before some final thoughts, let us put all the residuals together. The first graph below shows the residuals of all five models in the same scatter plot. Can you see how the <span style="color:blue">****blue****</span> dots (Model 1) seem to be closer to the zero (vertical axis) than the dots from the other models? The second plot shows all histograms next to each other to facilitate the visual comparison.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 13.png" >}}

{{< figure library="true" src="econometrics/03_OLS/OLS Example 14.png" >}}

---

## Some final thoughts

This is a _running-your-first-regression_ exercise. We can summarize our steps in the following list:

1. Get or build your data and, if needed, give it a user-friendly format.
2. Familiarize yourself with the data
   * Statistical summary
   * Correlation matrix
   * Scatter plots
3. Define your base model and alternative versions
4. Evaluate the quality of each model
   * Coefficient of determination $(R^2, \bar{R}^2$)
   * Root Mean Squared Error $(RMSE)$
   * Information Criteria $(AIC, BIC)$
   * Distribution of the residuals

You can probably see that running this regression involves a combination of technical steps (such as how to estimate the coefficient or read the output) as well as subjective inputs in terms of what control variables to include or which model makes more economic sense (for instance, to avoid over-fitting).

However, there is plenty more than must be taken into consideration when evaluating a model, for instance:

1. What hypotheses tests can we perform?
2. Is the model correctly specified?
3. Is there heteroskedasticity?
4. Is there serial correlation?
5. Is there multicollinearity?
6. Is there endogeneity?

Before discussing these topics, we must study the classical assumptions used in a regression analysis. These assumptions will provide a more precise foundation of econometric techniques, precision needed before moving to the next topics.