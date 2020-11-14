Lab 7
================
Marjan Rezvani, Patrick Sinclair, Kieran Yuen

### Predicting Health Insurance Coverage

Using the provided data from the National Health Interview Survey 2014,
we took a subset of respondents between the ages of 17 and 75. We chose
this particular range with a view to further possible subgroups, such as
examining the changes in insurance coverage from those of college age up
to 26 and those in their late 20s and early 30s, who are [no longer
eligible](https://www.healthcare.gov/young-adults/children-under-26/) to
be claimed on their parents’ plans.

Below we have subtotals and proportions for the respondents in the data
set between the ages of 17 and 75 who have and do not have health
insurance coverage.

<table class="kable_wrapper">

<tbody>

<tr>

<td>

| Coverage    | Total |
| :---------- | :---- |
| Covered     | 67343 |
| Not Covered | 12229 |
| Sum         | 79572 |

</td>

<td>

| Coverage    | Proportion |
| :---------- | ---------: |
| Covered     |  0.8463153 |
| Not Covered |  0.1536847 |

</td>

</tr>

</tbody>

</table>

Approximately 85% of respondents have health insurance coverage.

Here are the logit regression results from the amended subset - Age
\(\ge 17\), \(\le 75\).

    ## 
    ## Call:
    ## glm(formula = NOTCOV ~ AGE_P + I(AGE_P^2) + female + AfAm + Asian + 
    ##     RaceOther + Hispanic + educ_hs + educ_smcoll + educ_as + 
    ##     educ_bach + educ_adv + married + widowed + divorc_sep + veteran_stat + 
    ##     REGION + region_born, family = binomial, data = dat2)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.9027  -0.5923  -0.3807  -0.1889   3.3181  
    ## 
    ## Coefficients:
    ##                                 Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)                   -3.475e+00  1.056e-01 -32.897  < 2e-16 ***
    ## AGE_P                          1.455e-01  5.235e-03  27.791  < 2e-16 ***
    ## I(AGE_P^2)                    -2.031e-03  6.192e-05 -32.808  < 2e-16 ***
    ## female                        -2.804e-01  2.216e-02 -12.653  < 2e-16 ***
    ## AfAm                          -1.443e-01  3.299e-02  -4.375 1.21e-05 ***
    ## Asian                         -2.245e-01  7.539e-02  -2.977 0.002907 ** 
    ## RaceOther                      5.108e-01  6.640e-02   7.694 1.43e-14 ***
    ## Hispanic                       3.185e-01  3.456e-02   9.216  < 2e-16 ***
    ## educ_hs                       -2.222e-01  2.988e-02  -7.438 1.02e-13 ***
    ## educ_smcoll                   -6.288e-01  3.465e-02 -18.148  < 2e-16 ***
    ## educ_as                       -7.498e-01  4.271e-02 -17.556  < 2e-16 ***
    ## educ_bach                     -1.442e+00  4.378e-02 -32.944  < 2e-16 ***
    ## educ_adv                      -2.087e+00  7.160e-02 -29.152  < 2e-16 ***
    ## married                       -6.677e-01  2.751e-02 -24.271  < 2e-16 ***
    ## widowed                       -3.463e-02  8.582e-02  -0.404 0.686554    
    ## divorc_sep                    -4.753e-02  3.892e-02  -1.221 0.222005    
    ## veteran_stat                  -5.787e-01  5.962e-02  -9.707  < 2e-16 ***
    ## REGIONMidwest                  2.882e-01  4.068e-02   7.084 1.40e-12 ***
    ## REGIONSouth                    6.940e-01  3.522e-02  19.704  < 2e-16 ***
    ## REGIONWest                     2.874e-01  3.721e-02   7.724 1.13e-14 ***
    ## region_bornMex Cent Am Caribb  1.072e+00  3.851e-02  27.843  < 2e-16 ***
    ## region_bornS Am                9.464e-01  8.515e-02  11.115  < 2e-16 ***
    ## region_bornEur                 3.699e-01  1.024e-01   3.613 0.000303 ***
    ## region_bornformer USSR         9.618e-01  2.057e-01   4.675 2.94e-06 ***
    ## region_bornAfrica              8.155e-01  1.092e-01   7.469 8.05e-14 ***
    ## region_bornMidE                4.319e-01  1.753e-01   2.464 0.013741 *  
    ## region_bornIndia subc          9.019e-01  1.209e-01   7.458 8.80e-14 ***
    ## region_bornAsia                9.204e-01  1.136e-01   8.104 5.32e-16 ***
    ## region_bornSE Asia             4.811e-01  1.041e-01   4.623 3.79e-06 ***
    ## region_bornElsewhere           2.878e-01  1.626e-01   1.770 0.076771 .  
    ## region_bornunknown            -9.682e-02  1.912e-01  -0.506 0.612529    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 67348  on 78049  degrees of freedom
    ## Residual deviance: 55501  on 78019  degrees of freedom
    ##   (1522 observations deleted due to missingness)
    ## AIC: 55563
    ## 
    ## Number of Fisher Scoring iterations: 6

Given that the dependent variable NOTCOV is coded 0 and 1. [(p. 202,
Person Variable Layout Document) N.B. This link immediately initiates a
PDF
download](ftp://ftp.cdc.gov/pub/Health_Statistics/NCHS/Dataset_Documentation/NHIS/2014/personsx_layout.pdf).
The value 1 meaning that the condition of no coverage *is* present, we
can interpret from the logit regression that coefficients with a
positive value are predictors of **NOT** having health insurance.

As we implement the other machine learning prediction models and
interpret their results, we can keep the results of this logit
regression in mind, as a guide for what the models are putting emphasis
on and how they are treating the variables differently from model to
model. For example, when we look at the results from the Support vector
Machine, we know that in an SVM, the loss function for observations that
fall on the correct side of the margins of the separating plane have no
bearing on the position or slope of the separating plane. In a logit
regression, the loss function is never exactly equal to zero, so
observations that fall well within in each classification zone will
still impact the position and slope of the separating plane as those
observations change, even if the impact is very small. If the dependent
classes are well separated, the logit regression is more susceptible to
the impact of outlying determining variables than Support Vector
Machines [(James, Witten, Hastie and Tibshirani,
p. 357)](https://trevorhastie.github.io/ISLR/ISLR%20Seventh%20Printing.pdf).

We’ve utilized the provided data.frame and standarizing code to
standardize the variables and create our training and test sets. The
training set is comprised of 75% of the observations.

#### OLS

    ## 
    ## Call:
    ## lm(formula = sobj$formula, data = sobj$data)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -0.64347 -0.17562 -0.09177 -0.00847  1.06728 
    ## 
    ## Coefficients:
    ##                         Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)             0.457555   0.032292  14.169  < 2e-16 ***
    ## Age                    -0.040676   0.001660 -24.496  < 2e-16 ***
    ## female1                -0.014050   0.001391 -10.100  < 2e-16 ***
    ## AfAm1                  -0.012040   0.002124  -5.668 1.45e-08 ***
    ## Asian1                 -0.017047   0.004504  -3.785 0.000154 ***
    ## RaceOther1              0.036836   0.005204   7.079 1.47e-12 ***
    ## Hispanic1               0.021955   0.002451   8.958  < 2e-16 ***
    ## educ_hs1               -0.006280   0.002218  -2.832 0.004632 ** 
    ## educ_smcoll1           -0.032028   0.002401 -13.339  < 2e-16 ***
    ## educ_as1               -0.031766   0.002796 -11.362  < 2e-16 ***
    ## educ_bach1             -0.058236   0.002496 -23.329  < 2e-16 ***
    ## educ_adv1              -0.066090   0.002936 -22.510  < 2e-16 ***
    ## married1               -0.026369   0.001787 -14.754  < 2e-16 ***
    ## widowed1               -0.019298   0.004518  -4.271 1.95e-05 ***
    ## divorc_sep1             0.003838   0.002621   1.464 0.143073    
    ## Region.Midwest1         0.013818   0.002308   5.987 2.15e-09 ***
    ## Region.South1           0.035328   0.002081  16.975  < 2e-16 ***
    ## Region.West1            0.012189   0.002176   5.602 2.13e-08 ***
    ## born.Mex.CentAm.Carib1  0.114031   0.002972  38.369  < 2e-16 ***
    ## born.S.Am1              0.064050   0.006712   9.542  < 2e-16 ***
    ## born.Eur1               0.015393   0.005745   2.679 0.007376 ** 
    ## born.f.USSR1            0.046016   0.013322   3.454 0.000552 ***
    ## born.Africa1            0.053062   0.007755   6.843 7.85e-12 ***
    ## born.MidE1              0.014229   0.010581   1.345 0.178682    
    ## born.India.subc1        0.041993   0.007429   5.653 1.59e-08 ***
    ## born.Asia1              0.047528   0.007167   6.631 3.35e-11 ***
    ## born.SE.Asia1           0.028574   0.006203   4.606 4.10e-06 ***
    ## born.elsewhere1         0.013040   0.009681   1.347 0.178008    
    ## born.unknown1           0.002700   0.012735   0.212 0.832101    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.3357 on 59598 degrees of freedom
    ## Multiple R-squared:  0.1297, Adjusted R-squared:  0.1293 
    ## F-statistic: 317.3 on 28 and 59598 DF,  p-value: < 2.2e-16

    ##        true
    ## pred        0     1
    ##   FALSE 16542  2660
    ##   TRUE    285   458

#### Logit

    ## 
    ## Call:
    ## glm(formula = sobj$formula, family = binomial, data = sobj$data)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.8479  -0.5807  -0.4028  -0.2500   2.9873  
    ## 
    ## Coefficients:
    ##                        Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)             0.52586    0.28955   1.816 0.069347 .  
    ## Age                    -0.37604    0.01562 -24.069  < 2e-16 ***
    ## female1                -0.11855    0.01241  -9.554  < 2e-16 ***
    ## AfAm1                  -0.06342    0.01877  -3.379 0.000728 ***
    ## Asian1                 -0.12145    0.04241  -2.864 0.004186 ** 
    ## RaceOther1              0.24811    0.03831   6.476 9.41e-11 ***
    ## Hispanic1               0.15787    0.01950   8.097 5.65e-16 ***
    ## educ_hs1               -0.01242    0.01656  -0.750 0.453237    
    ## educ_smcoll1           -0.21762    0.01918 -11.345  < 2e-16 ***
    ## educ_as1               -0.21793    0.02399  -9.086  < 2e-16 ***
    ## educ_bach1             -0.57293    0.02476 -23.139  < 2e-16 ***
    ## educ_adv1              -0.87361    0.04078 -21.421  < 2e-16 ***
    ## married1               -0.21032    0.01567 -13.418  < 2e-16 ***
    ## widowed1               -0.17073    0.04856  -3.516 0.000438 ***
    ## divorc_sep1             0.07916    0.02227   3.554 0.000379 ***
    ## Region.Midwest1         0.14460    0.02309   6.264 3.76e-10 ***
    ## Region.South1           0.33499    0.01998  16.769  < 2e-16 ***
    ## Region.West1            0.14045    0.02110   6.657 2.80e-11 ***
    ## born.Mex.CentAm.Carib1  0.65762    0.02152  30.562  < 2e-16 ***
    ## born.S.Am1              0.52652    0.04881  10.787  < 2e-16 ***
    ## born.Eur1               0.16952    0.05743   2.952 0.003158 ** 
    ## born.f.USSR1            0.44475    0.11830   3.759 0.000170 ***
    ## born.Africa1            0.46611    0.06236   7.474 7.76e-14 ***
    ## born.MidE1              0.17140    0.10424   1.644 0.100121    
    ## born.India.subc1        0.46334    0.07035   6.587 4.50e-11 ***
    ## born.Asia1              0.47606    0.06476   7.351 1.97e-13 ***
    ## born.SE.Asia1           0.25315    0.05979   4.234 2.30e-05 ***
    ## born.elsewhere1         0.14647    0.09361   1.565 0.117686    
    ## born.unknown1           0.07727    0.10869   0.711 0.477121    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 50985  on 59626  degrees of freedom
    ## Residual deviance: 43533  on 59598  degrees of freedom
    ## AIC: 43591
    ## 
    ## Number of Fisher Scoring iterations: 6

    ##        true
    ## pred        0     1
    ##   FALSE 16571  2700
    ##   TRUE    256   418

Given the standardized variables, we can compare the OLS and Logit
regressions. While the values of each coefficient vary, the sign for
each coefficient is the same across both regressions. The OLS regression
is demonstrating the correlation of each variable with the condition of
not having health insurance. The logit regression is giving us the
probability of the condition of not having health insurance given each
variable.

Due to the standardization of the variables, the coefficients estimated
by the OLS regression are all small - considering them as raw values
gives us a skewed interpretation of the result; we need to consider
where these the absolute values of the coefficients sit on the interval
\[0,1\].

The logit regression is more straightforward, as we would expect the
probabilities to be given on a \[0,1\] interval.

Changing the predvals parameter to \> 0.45 increases the accuracy of
both models, by 0.3% and 0.11% for the OLS and Logit models
respectively. The increases are negligible. Leaving the Logit predvals
value at \> 0.5 makes more sense as 0.5 is a probability value in this
model. Setting it to a value below 0.5 would skew the correct prediction
rate of whether the dependent variable is equal to 1. The prediction
rate of the OLS and Logit models are 85.23% and 85.18% respectively.

### Random Forest

Here is code for a Random Forest, which takes a bit of computing,

Note that the estimation prints out a Confusion Matrix first but that’s
within the training data; the later one calculates how well it does on
the test data.

### Support Vector Machines

Next is Support Vector Machines. First it tries to find optimal tuning
parameter, next uses those optimal values to train. (Tuning takes a long
time so skip for now\!)

### Elastic Net

Here is Elastic Net. It combines LASSO with Ridge and the alpha
parameter (from 0 to 1) determines the relative weight. Begin with alpha
= 1 so just LASSO.

When you summarize, you should be able to explain which models predict
best (noting if there is a tradeoff of false positive vs false negative)
and if there are certain explanatory variables that are consistently
more or less useful. Also try other lists of explanatory variables.

### Bibliography

<ftp://ftp.cdc.gov/pub/Health_Statistics/NCHS/Dataset_Documentation/NHIS/2014/personsx_layout.pdf>

<https://www.healthcare.gov/young-adults/children-under-26/>

James, Gareth, Daniela Witten, Trevor Hastie, and Robert Tibshirani,
(2017). Introduction to Statistical Learning. New York: Springer
Science+Business Media,
<https://trevorhastie.github.io/ISLR/ISLR%20Seventh%20Printing.pdf>
