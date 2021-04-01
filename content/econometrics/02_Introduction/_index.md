---
# Title, summary, and page position.
linktitle: "Introduction to Econometrics"
weight: 2

# Page metadata.
title: Introduction to Econometrics
date: "2018-09-09T00:00:00Z"
type: book  # Do not modify.
---



---

## What is econometrics

It is easy to infer a definition of [**econometrics**](https://en.wikipedia.org/wiki/Econometrics) from its etymology. The literal interpretation of the word *econometrics* is *economic measurement*. More precisely, econometrics is the application of statistical techniques to economics.

Econometrics is not in itself economic theory. It is, however, a very important complement. Economic theory estipulates *qualitative* relationships. For instance, a demand function can be represented as $q^D = a - bp$; where $q^D$ is the quantity demanded, $p$ is the price of the good in question, and $a$ and $b$ are two parameters. From economic **theory** we know that $a$ and $b$ are positive $(a, b, >0)$. However, economic theory **does not** give values to either $a$ or $b$. We do not know, just from theory, how steep the demand line is. Econometrics is a statistical method through which the values of $a$ and $b$ are estimated. Put it differently, if economic theory is **qualitative**, then econometrics is **quantitative**.

Note that econometrics uses the values of **observable** economic **variables** (such as quantities and prices) to estimate what would be the **parameters** in an economic model (such as $a$ and $b$ in the demand function). This is a different excercise from finding, say, an $x^*$ that optimizes the value of $y = f(x)$ with **given** parameter values.

---

## Uses of econometrics

Econometrics is a technique that can be used in different ways such as:

* To test a hypothesis
* To make an economic description
* To forecast or predict the unobserved value of economic variables

For instance, you may want to test the hunch or intuition (the hypothesis) that the [elasticity](https://en.wikipedia.org/wiki/Elasticity_(economics)) of the demand function equals 1 at a given price.[^1] Alternatively, you may just be interested in what the slope of the demand is at a given price point, so that you can plan your business strategy accordingly. Finally, you may want to estimate what the quantity demanded of a gadget you produce would be in a country where you do not operate by looking at data from countries where you do have business operations.

These are three very distinctive uses of econometrics. These different uses also shows that econometrics, and doing empirical work, is not just about testing hypothesis. It can also be descriptive or predictive. Furthermore, this also means that, epistemologically speaking, doing econometrics and empirical work does not mean one is necessarily being a logical positivist (later known as [logical empiricism](https://plato.stanford.edu/entries/logical-empiricism/)).

---

## The econometric technique

### Regression analysis and the estimation rule

There are different ways to estimate the value of a parameter, such as the slope of a demand function. One alternative is to ask your mother what she thinks the slope is. Asking yout mother is an easy method, but also is a method very likely to be very innacurate. Econometrics applies regression analysis to infer a more accurate estimation of these parameters.

The estimation of the slope of a demand function makes use (ideally) of a large set of prices and quantities. All these prices and quantities do not offer a perfect match to one and unique slope of the demand function. Therefore, we need a *rule* to decide how the slope must be estimated. Econometrics is a technique  built to minimize mistakes between what the econometric model estimates and the observed data.

### An example

Let the quantity demanded of a good $(q^D)$ depend on its price $p$, the price of a substitute good $p_S$, and the level of disposable income of potential customers $Y_D$. Then, we can represent this relationship in the following way

$$ q^D = \beta_0 + \beta_1 P + \beta_2 P_S + \beta_3 Y_D + \varepsilon $$

Through data collection (observation) we know values of $q^D$, $p$, $p_S$, and $Y_D$. After applying a regression analysis we get an estimation of the parameters, that is, the $betas$. Our estimated model may look the following way (where the *hats* denote estimated values):

$$ \hat{q^D} = \hat{\beta_0} + \hat{\beta_1} p + \hat{\beta_2} p_S + \hat{\beta_3} Y_D $$

$$ \hat{q^D} = 25 - 0.25 p + 0.15 p_S + 0.10 Y_D $$

At this point is enough to point to two issues. The first one is that there is *hat* on top of $q^D$. This hat means that once you have your $beta$ estimations, you can use the prices and disposable income information to *predict* or *estimate* values of $q^D$. The second one is that there is no error term in the estimated equation because now we have specific estimations of $q^D$ rather than randmo variables.

Now, some terminology. The left-hand variable $(q^D)$ is called the dependent variable. The right-hand variables are called the **regressors** (the *independent* variables).

{{% callout warning %}}
In econometrics, the word **explanation** means that **changes in a regressor** are correlated with **changes** in the dependent variable.

The **change** in one regressor *explains* **part** of the **change** of the dependent variable.

In econometrics, the word **explanation** does not have a *cause-effect* meaning. An econometric model is silent about whether the **change** in one regressor is the **cause** of changes in the dependent variable.
{{% /callout %}}

### Regression and causality

**Cause and effect** relationships belong to the realm of economic **theory**. Econometrics is about **measurement**. A regression captures correlations between variables, that is, co-movements. Regardless of how strong a correlation is, the fact that two variables are somehow correlated does not mean in itself there is a cause-effect relationship between them.

The fact that an econometrics model is built over an economic theory, or over some cause-effect theory, does not mean a regression is showing causality. For instance, variables $x$ and $y$ may have no causality relationship and still be correlated if both of them are independently related to the same variable $z$. The overlap of a regression over a theory should not led us to confussion about what a regression can and cannot show.

{{% callout note %}}
A regression shows **correlations**, it does not show or prove **causality**.
{{% /callout %}}

---

## Types of data

What type of econometric techniques can be used depends on the type of data you have at your disposal. There are three types of datasets:

1. Cross-sectional
2. Time-series
3. Panel data (also known as longitudinal data)

**Cross-sectional** data includes number of *sections* and one time-period only. For instance, income and unemployment information for the 50 U.S. states in the year 1930.

**Time-series** data is the inverse situation. The dataset has information of one section for a number of years. For instance, the unemployment rate of the state of Colorado between 1920 and 1950.

**Panel data** is the combination of the other two. Now the dataset includes information for more than one section and more than one time period. For instance, income for the 50 U.S. states between 1920 and 1950.

---

## A recommendation and a word of advice

Before moving into the next chapter and delving into the details of econometric analysis, a recommendation and a word of advice

### A recommendation: Think of econometrics more as an art than as hard-science

Econometrics can be highly technical and theoretical. There is a reason why econometrics has the fame of being a difficulty subject. However, you should remember that econometrics is the applciation of **statistical** methods. This has two important implications.

First, there is no unique answer to the question of what value is the right estimation of your unknown parameters. This means that different people will disagree on what the right approach should be in different cases. And in many times there is no definite way to sort out those disagreements. 

Second, there is no unique method or *model specification* that can be used to make an estimation. Several regression analyses may be possible. Again, different people can disagree on what the best application is, without a definite way to sort out the difference of opinion. Your focus should be on what are the *reasonable* ways to answer your questions, not in finding the unique proper solution to an econometric problem.

These implications mean that, even if an estimation is obtained following strict and precise theoretical methods, the estimation output is open to interpretation. While regression analysis can be objective, in the sense of following a specific methods and theories, model application and interpretation is subjective. How to apply and read a model requires the economist intuition of what is happening behind the scenes (unobservable) and what the proper reading of the output should be.

Therefore, econometrics is not only a scientific application, it also an **art**, in the sense that each econometric application is driven by a subjective point of view that can vary from person to person. Forgetting the subjective component of applied econometrics can make this subject harder than it has to be.

### A word of advice: Econometrics is not economics (and the other way around)

Even thouth econometrics is an important field in economics, neither econometrics is economics nor economics is econometrics.

Anyone can be an excellent economist and at the same time have a very limited knowledge of econometrics. In fact, some of the most influential economics, such as [James M. Buchanan](https://en.wikipedia.org/wiki/James_M._Buchanan[), [Ronald H. Coase](https://en.wikipedia.org/wiki/Ronald_Coase), or [Friedrich A. von Hayek](https://en.wikipedia.org/wiki/Friedrich_Hayek), made little use of intense mathematics or econometric applications.

Inversely, someone can be an outstanding econometrician while being clueless about economics. Economics is a way of thinking (theory) about how the world works. Economics itself is not a way of testing an hypothesis. Statistics without a theory is not economics, it is just statistics. To wit, [economics is not statistics (and vice versa)](https://www.peterleeson.com/Economics_is_Not_Statistics.pdf).

To sum, you can be a good economists with little knowledge of econometrics, such as you can become a great econometrician but not become a good economist.

<!-- FOOTNOTES -->
[^1]: Recall that the point price-elasticity of demand is: $|\epsilon| = \frac{\partial Q^D}{\partial p} \cdot \frac{p}{Q^D}.$
