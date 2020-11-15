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
training set is comprised of 20% of the observations.

#### OLS

    ## 
    ## Call:
    ## lm(formula = sobj$formula, data = sobj$data)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -0.63871 -0.17152 -0.08945 -0.00404  1.03573 
    ## 
    ## Coefficients:
    ##                          Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)             0.3943589  0.0619257   6.368 1.96e-10 ***
    ## Age                    -0.0401233  0.0031881 -12.585  < 2e-16 ***
    ## female1                -0.0122144  0.0026681  -4.578 4.73e-06 ***
    ## AfAm1                  -0.0164170  0.0040827  -4.021 5.82e-05 ***
    ## Asian1                 -0.0143641  0.0083606  -1.718 0.085802 .  
    ## RaceOther1              0.0373773  0.0097603   3.830 0.000129 ***
    ## Hispanic1               0.0193867  0.0047109   4.115 3.89e-05 ***
    ## educ_hs1               -0.0005653  0.0043125  -0.131 0.895717    
    ## educ_smcoll1           -0.0310521  0.0046546  -6.671 2.62e-11 ***
    ## educ_as1               -0.0274274  0.0053142  -5.161 2.48e-07 ***
    ## educ_bach1             -0.0533572  0.0048056 -11.103  < 2e-16 ***
    ## educ_adv1              -0.0671569  0.0056160 -11.958  < 2e-16 ***
    ## married1               -0.0265638  0.0034426  -7.716 1.27e-14 ***
    ## widowed1               -0.0215873  0.0088095  -2.450 0.014278 *  
    ## divorc_sep1             0.0016613  0.0050733   0.327 0.743326    
    ## Region.Midwest1         0.0168660  0.0044298   3.807 0.000141 ***
    ## Region.South1           0.0380560  0.0039923   9.532  < 2e-16 ***
    ## Region.West1            0.0126649  0.0041635   3.042 0.002355 ** 
    ## born.Mex.CentAm.Carib1  0.1206322  0.0057188  21.094  < 2e-16 ***
    ## born.S.Am1              0.0724097  0.0133533   5.423 5.96e-08 ***
    ## born.Eur1               0.0075462  0.0114026   0.662 0.508110    
    ## born.f.USSR1            0.0028652  0.0256390   0.112 0.911021    
    ## born.Africa1            0.0686910  0.0143355   4.792 1.67e-06 ***
    ## born.MidE1             -0.0072496  0.0207780  -0.349 0.727165    
    ## born.India.subc1        0.0417634  0.0144345   2.893 0.003817 ** 
    ## born.Asia1              0.0514502  0.0135720   3.791 0.000151 ***
    ## born.SE.Asia1           0.0278490  0.0118692   2.346 0.018972 *  
    ## born.elsewhere1         0.0179289  0.0165713   1.082 0.279303    
    ## born.unknown1          -0.0286173  0.0251313  -1.139 0.254841    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.331 on 15748 degrees of freedom
    ## Multiple R-squared:  0.1371, Adjusted R-squared:  0.1356 
    ## F-statistic: 89.35 on 28 and 15748 DF,  p-value: < 2.2e-16

    ##        true
    ## pred        0     1
    ##   FALSE 52942  8355
    ##   TRUE    974  1524

#### Logit

    ## 
    ## Call:
    ## glm(formula = sobj$formula, family = binomial, data = sobj$data)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.8296  -0.5692  -0.3931  -0.2330   3.0235  
    ## 
    ## Coefficients:
    ##                        Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)            -0.35139    0.63245  -0.556 0.578479    
    ## Age                    -0.38256    0.03095 -12.360  < 2e-16 ***
    ## female1                -0.10541    0.02452  -4.299 1.72e-05 ***
    ## AfAm1                  -0.10481    0.03778  -2.774 0.005536 ** 
    ## Asian1                 -0.11644    0.08281  -1.406 0.159670    
    ## RaceOther1              0.24634    0.07390   3.333 0.000858 ***
    ## Hispanic1               0.13799    0.03873   3.563 0.000367 ***
    ## educ_hs1                0.02991    0.03302   0.906 0.364970    
    ## educ_smcoll1           -0.21925    0.03847  -5.699 1.20e-08 ***
    ## educ_as1               -0.18446    0.04666  -3.953 7.70e-05 ***
    ## educ_bach1             -0.53480    0.04838 -11.054  < 2e-16 ***
    ## educ_adv1              -1.02187    0.08923 -11.452  < 2e-16 ***
    ## married1               -0.21826    0.03112  -7.014 2.31e-12 ***
    ## widowed1               -0.21749    0.09959  -2.184 0.028979 *  
    ## divorc_sep1             0.05821    0.04455   1.307 0.191343    
    ## Region.Midwest1         0.18493    0.04625   3.998 6.39e-05 ***
    ## Region.South1           0.37907    0.04027   9.412  < 2e-16 ***
    ## Region.West1            0.16201    0.04238   3.823 0.000132 ***
    ## born.Mex.CentAm.Carib1  0.71326    0.04275  16.683  < 2e-16 ***
    ## born.S.Am1              0.60564    0.09786   6.189 6.06e-10 ***
    ## born.Eur1               0.06948    0.12620   0.551 0.581951    
    ## born.f.USSR1           -0.01891    0.27934  -0.068 0.946037    
    ## born.Africa1            0.59365    0.11398   5.208 1.91e-07 ***
    ## born.MidE1             -0.11569    0.26435  -0.438 0.661657    
    ## born.India.subc1        0.52396    0.14141   3.705 0.000211 ***
    ## born.Asia1              0.54277    0.12586   4.313 1.61e-05 ***
    ## born.SE.Asia1           0.26818    0.11818   2.269 0.023258 *  
    ## born.elsewhere1         0.21471    0.15749   1.363 0.172779    
    ## born.unknown1          -0.24651    0.27101  -0.910 0.363033    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 13281  on 15776  degrees of freedom
    ## Residual deviance: 11193  on 15748  degrees of freedom
    ## AIC: 11251
    ## 
    ## Number of Fisher Scoring iterations: 6

    ##        true
    ## pred        0     1
    ##   FALSE 53024  8454
    ##   TRUE    892  1425

Given the standardized variables, we can compare the OLS and Logit
regressions. While the values of each coefficient vary, the sign for
each coefficient is the same across both regressions. The OLS regression
is demonstrating the correlation of each variable with the condition of
not having health insurance. The logit regression is giving us the
probability of the condition of not having health insurance, given each
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
rate of the OLS and Logit models are 85.38% and 85.35% respectively.

### Random Forest Model

    ## Loading required package: randomForest

    ## randomForest 4.6-14

    ## Type rfNews() to see new features/changes/bug fixes.

    ## 
    ## Call:
    ##  randomForest(formula = as.factor(NOTCOV) ~ ., data = sobj$data,      importance = TRUE, proximity = TRUE) 
    ##                Type of random forest: classification
    ##                      Number of trees: 500
    ## No. of variables tried at each split: 5
    ## 
    ##         OOB estimate of  error rate: 13.77%
    ## Confusion matrix:
    ##       0   1 class.error
    ## 0 13207 220   0.0163849
    ## 1  1952 398   0.8306383

    ##                           0      1 MeanDecreaseAccuracy MeanDecreaseGini
    ## Age                   37.76  41.85                52.82           335.30
    ## female                 5.57   7.51                 8.85            36.76
    ## AfAm                   0.47  21.61                16.04            26.19
    ## Asian                  9.58   1.69                11.19            14.46
    ## RaceOther              5.90   8.32                 9.75            19.79
    ## Hispanic              -9.81  31.35                36.33           123.57
    ## educ_hs               17.99  -9.37                14.97            33.46
    ## educ_smcoll           13.63  14.93                22.66            29.61
    ## educ_as               14.35  11.69                19.96            21.13
    ## educ_bach             20.35  26.99                33.81            43.40
    ## educ_adv              25.42  27.85                36.67            40.04
    ## married               28.37 -16.28                27.19            52.56
    ## widowed                5.99   0.61                 6.61             9.90
    ## divorc_sep             8.74  -2.07                 7.25            20.14
    ## Region.Midwest         0.73   7.99                 7.03            18.81
    ## Region.South           4.47  17.84                19.03            37.55
    ## Region.West           -2.24  10.65                 8.65            24.74
    ## born.Mex.CentAm.Carib -1.70  61.87                48.10           201.37
    ## born.S.Am              6.60  12.33                13.10            13.77
    ## born.Eur               2.27  -2.56                 1.05             7.80
    ## born.f.USSR           -5.49  -4.43                -6.35             2.56
    ## born.Africa           -1.78   5.20                -0.03            10.47
    ## born.MidE             -4.93  -1.39                -5.12             2.69
    ## born.India.subc       13.10   1.79                14.34             8.60
    ## born.Asia              2.24   1.32                 2.77             9.81
    ## born.SE.Asia           9.40  -2.38                 9.19             8.69
    ## born.elsewhere         2.25   1.81                 2.76             7.43
    ## born.unknown          -1.84  -0.89                -2.17             2.78

![](Lab7_files/figure-gfm/Random%20Forest-1.png)<!-- --> ![RF
Plot](./RFPlot.png)

    ##     true
    ## pred     0     1
    ##    0 52996  8269
    ##    1   920  1610

Our Random Forest model gives us a correct prediction rate within the
test data of 85.6% and it provides us some clearer insight into the
variables that are important to the accuracy of the model. We can see
from both the Mean Accuracy Decrease and the Mean Gini Decrease that
age, the education variables and the race variables are important to the
accuracy of the model. Interestingly enough, region of birth is
unimportant to the accuracy of this model - the two birth regions, Sth
America and Mexico, Central America and the Caribbean with the highest
importance link to the race variable with the highest importance,
i.e. Hispanic. The Hispanic variable has a large impact on predicting
that an observation *does not* have health coverage.

We can use the variable importance generated from the Random Forest to
redesign our earlier OLS and Logit models and remove the less important
variables.

Prior to that, we should tune our Random Forest model to determine the
optimal number of variables used at each split of the data. We can also
change the number of trees to make the model easier to compute.

Here is some code to tune the Random Forest for mtry (the number of
variables used at each split). The number of trees in the forest has
also been reduced to 100.

``` r
mtry <- tuneRF(sobj$data[-1], as.factor(sobj$data$NOTCOV), ntreeTry = 100, stepFactor = 1.5, improve = 0.05, trace = TRUE, plot = TRUE)
```

    ## mtry = 5  OOB error = 13.67% 
    ## Searching left ...
    ## mtry = 4     OOB error = 13.83% 
    ## -0.01205937 0.05 
    ## Searching right ...
    ## mtry = 7     OOB error = 13.74% 
    ## -0.005565863 0.05

![](Lab7_files/figure-gfm/Optimal%20Variable%20Code%20for%20Random%20Forest-1.png)<!-- -->

    ##       mtry  OOBError
    ## 4.OOB    4 0.1383026
    ## 5.OOB    5 0.1366546
    ## 7.OOB    7 0.1374152

    ##      mtry  OOBError 
    ## 5.0000000 0.1366546

The optimal mtry number is 5, which in concert with a smaller number of
trees reduced the Out of Box error rate from 13.77% to 13.67%. This rate
tells us that as the model makes the splits and performs prediction
tests on internally designated training and test data, it makes errors
at a rate of 13.67%, performing slightly better than when the model is
applied to the overall test data.

### Support Vector Machines

Next is Support Vector Machines. First it tries to find optimal tuning
parameter, next uses those optimal values to train. (Tuning takes a long
time so skip for now\!)

    ## Loading required package: e1071

    ##     true
    ## pred          0          1
    ##    0 0.82156909 0.12518222
    ##    1 0.02357552 0.02967317

    ## [1] 0.8512423

Running the SVM as given produces a correct prediction rate of 85.12%.
We can change the SVM model by adjusted the cost and gamma parameters.
The cost parameter determines the tolerance the model has to violations
of the margins of the separating plane; the higher the cost, the
narrower the margin, which produces results with high variance but a
lower bias. With higher variance, the model may give [different
estimates](https://machinelearningmastery.com/support-vector-machines-for-machine-learning/)
for the function of the separating plane when applied to different data
sets. If we want to lower the variance to keep estimates produced by the
model similar as we change data sets, we need to increase the bias - we
have to accept that the model makes more assumptions about the form of
the separating function. To keep estimates more consistent across
different data sets, we have to accept that the model will lose
predictive power.

If we are comfortable with the data set at hand and seek strong
predictive power, we can set our cost high, increasing the variance and
lowering the bias of the model - similar to a logistic model. If we wish
to look at multiple data-sets, to assess correlation and causality, the
SVM model has to be adjusted with lower cost, reducing the variance and
increasing the bias - similar to an OLS model.

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

Brownlee, Jason, (2016). “Support Vector Machines for Machine Learning”,
<https://machinelearningmastery.com/support-vector-machines-for-machine-learning/>

James, Gareth, Daniela Witten, Trevor Hastie, and Robert Tibshirani,
(2017). “Introduction to Statistical Learning”, New York: Springer
Science+Business Media,
<https://trevorhastie.github.io/ISLR/ISLR%20Seventh%20Printing.pdf>
