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
training set is comprised of 20% of the observations. We noticed that
creating factors of REGION and region\_born excluded Northeast and [Born
in the US](https://www.youtube.com/watch?v=EPhWR4d3FJQ), which will
influence the results the models produce. This may be an important
factor for the researcher querying the dataset to consider.

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

    ## Warning: package 'randomForest' was built under R version 4.0.3

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

    ## Loading required package: e1071

    ## Warning: package 'e1071' was built under R version 4.0.3

    ##     true
    ## pred     0     1
    ##    0 52412  7986
    ##    1  1504  1893

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

Changing the gamma value in the model adjusts the flexibility of the
separating plane. We removed the gamma value from the model and saw that
while our False Positive prediction rate decreased by 7.25%, our False
Negative rate increased by 0.09%. The trade off of these change in
predictions depends on the context of the person asking the questions of
the model. For a policy maker, correctly identifying those who lack
healthcare coverage is important. Misallocating resources to provide
health services to demographics that already have good access to those
service is a waste of critical government infrastructure and revenues.
For a health insurance company, the tolerance of misclassification may
be higher. A person who was predicted to not have coverage can still be
pitched with other health insurance products if they already have some
sort of coverage.

### Regularized Regression Models (Elastic Net, Ridge, Lasso)

We have run one model for each of the regularized regression models:
Elastic Net, Ridge, and Lasso. We ran one for each to be able to see and
understand the difference between the three. Lastly, after going through
the three models individually, we will compare the prediction results at
the end.

As we have made sure to standardize our explanatory variables, the
coefficients are all on a common scale and that means the penalty terms
we will be applying in these models will equally penalize all predictors
(e.g. Age will not be penalized more than female = “1”).

Being able to remove explanatory variables from our models that have
been overloaded with explanatory variables helps make our models more
interpretable. We want to remove explanatory variables that are not
contributing to our model because as the number of explanatory variables
increase, the more likely we will tend to overfit our training data and
underfit our testing data.

#### Elastic Net

Looking at the plot of our cross-validation ridge regression across all
the lambda values (*plot(cvmodel1\_elasticnet)*), we see a slight
improvement in the MSE as our penalty log(lambda) gets larger, which
suggests that a regular OLS model likely overfits the training data. But
if we continue to constrain the MSE further (i.e increase the penalty),
our MSE starts to increase. In this plot we can also see the optimal
lambda (the log value of the lambda which best minimizes the error in
cross-validation) is -7.772985, as calculated from the function
*log(cvmodel1\_elasticnet$lambda.min)*.

We chose to set alpha = 0.5 so that there will be an equal combination
of the Lasso penalty and the Ridge penalty.

Next, we want to identify which variables are most important to our
model which the elastic net regression can help us with. We run a
Variable Important Plot (*vip(cvmodel1\_elasticnet, num\_features = 50,
geom = “col”)*) on the cross-validation model of our elastic net
regression and see that the advanced degree, bachelor’s degree and being
married increases our likelihood of having health insurance. Whereas
variables such as a high school education being born in the South, your
age, being Hispanic or being born in Mexico/Central America/Carribean
decrease your likelihood of having health insurance. It is important to
note that the variables Hispanic and being born in Mexico/Central
American/Caribbean are probably related and have multicollinearity. For
this Elastic Net model has some of the ridge penatly incorporated in it
since the alpha is set to 0.5 so it can be better fit to handle
multicollinearity if we set the alpha closer to 0.

As elastic net performs feature selection (since it includes the Lasso
penalty), the next step we would take is to remove the variables who
have their coefficients pushed to zero from the model including all the
other “born-from,” region-based and other variables that show as zero in
the Variable Importance Plot below and re-run the elastic net to see how
the prediction results improve aka our model becomes more accurate and
also easier to interpret.

#### Ridge Regression

Looking at the plot of our cross-validation ridge regression across all
the lambda values (*plot(cvmodel1\_ridge)*), we see a slight improvement
in the MSE as our penalty log(lambda) gets larger, which suggests that a
regular OLS model likely overfits the training data. But if we continue
to constrain the MSE further (i.e increase the penalty), our MSE starts
to increase. In this plot we can also see the optimal lambda (the log
value of the lambda which best minimizes the error in cross-validation)
is -4.62849, as calculated from the function
*log(cvmodel1\_ridge$lambda.min)*.

As ridge regression does not perform feature selection, that is why you
see in the Variable Importance Plot below that all variables show some
degree of shading of importance. Whereas the Lasso and Elastic Net
regressions will zero out/push to zero the variables that are
unimportant. As ridge regression performs better when it only has
variables that are important, we will re-run a Ridge Regression after
removing some of the variables we have identified as less important
based on the Lasso and/or Elastic Net Regressions. However, this also
means that if we DO have a model where we do not want to drop any of our
variables for whatever reason, we can do a ridge regression as it will
keep all available features in the final model.

#### Lasso Regression

Looking at the plot of our cross-validation lasso regression across all
the lambda values (*plot(cvmodel1\_lasso)*), we see a slight improvement
in the MSE as our penalty log(lambda) gets larger, which suggests that a
regular OLS model likely overfits the training data. But if we continue
to constrain the MSE further (i.e increase the penalty), our MSE starts
to increase. In this plot we can also see the optimal lambda (the log
value of the lambda which best minimizes the error in cross-validation)
is -8.187031, as calculated from the function
*log(cvmodel1\_lasso$lambda.min)*.

And as the lasso regression also performs a automated explanatory
variable importance selection by using it’s ridge penalty to push
variables not just approximately to zero, but all the way to zero, we
can look at the Variable Important Plot to identify which variables are
less important. The Variable Important Plot function is informing us
that the “born-in” variables along with the “Region.” variables and some
other various variables are not important as they have no shading as the
coefficients of these variables have been pushed to zero by the lasso
regression. Compared to the elastic net regression we ran above, this
lasso regression marks the same variables as important as the elastic
net, but this lasso regression includes a few more: some college
education and female are (both more likely for health insurance) &
Race\_Other, born Africa, born South America (all three less likely for
having health insurance). This makes senses as the Elastic Net includes
both the ridge penalty and the lasso penalty: getting effective
regularization from the ridge penalty and also the explanatory variable
importance selection of the lasso penalty.

#### Results Comparison: Regularization Regression

Overall, the correct prediction percentage between the three models are
very close, even between the ridge and lasso regressions as that is
where you expect to see the largest differences which differ by less
than 0.0003%. The elastic net’s prediction results are right in between
that of the ridge and lasso. Even tweaking the elastic net alpha from
0.5 to 0.7 we only see a slight change that brings the correct
prediction percentage closer to the lasso’s percentage, which makes
sense since the alpha is getting closer to 1 (a lasso regression).

But all three of these results are significantly less than the \~80%+ we
are seeing from Random Forest and Support Vector Machines.

### Other Explanatory Variables

Based on the results from the previous Random Forest, SVM and Lasso
models, we noticed that REGION and region\_born were consistently
unimportant to the models. Age, education, gender and marriage variables
were all important, across all models. To test how these models would
handle other variables, we removed REGION, region\_born and the marriage
variables. We created a factor from the person\_healthstatus
observations and included them in a new subset to test. We noticed that
the factor excluded observations that had been coded “Excellent”, which
will influence how the models make the comparisons between the
observations.

    ## [1] 79572

#### OLS 2

    ## 
    ## Call:
    ## lm(formula = sobj2$formula, data = sobj2$data)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -0.52383 -0.17547 -0.09373 -0.01417  1.04528 
    ## 
    ## Coefficients:
    ##               Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)   0.057517   0.022554   2.550   0.0108 *  
    ## Age          -0.045734   0.002857 -16.008  < 2e-16 ***
    ## female1      -0.012388   0.002692  -4.602 4.22e-06 ***
    ## AfAm1         0.001419   0.003971   0.357   0.7209    
    ## Asian1        0.003446   0.005337   0.646   0.5184    
    ## RaceOther1    0.039184   0.009846   3.980 6.94e-05 ***
    ## Hispanic1     0.079525   0.003620  21.970  < 2e-16 ***
    ## educ_hs1     -0.018230   0.004310  -4.230 2.35e-05 ***
    ## educ_smcoll1 -0.050649   0.004641 -10.914  < 2e-16 ***
    ## educ_as1     -0.048079   0.005324  -9.031  < 2e-16 ***
    ## educ_bach1   -0.071002   0.004857 -14.619  < 2e-16 ***
    ## educ_adv1    -0.083047   0.005681 -14.619  < 2e-16 ***
    ## Very_Good1    0.007574   0.003462   2.187   0.0287 *  
    ## Good1         0.023991   0.003690   6.502 8.16e-11 ***
    ## Fair1         0.011995   0.005238   2.290   0.0220 *  
    ## Poor1        -0.015004   0.008644  -1.736   0.0826 .  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.3368 on 15761 degrees of freedom
    ## Multiple R-squared:  0.1058, Adjusted R-squared:  0.105 
    ## F-statistic: 124.3 on 15 and 15761 DF,  p-value: < 2.2e-16

    ##        true
    ## pred        0     1
    ##   FALSE 53802  9760
    ##   TRUE    114   119

The estimates for Age, gender and education all have the same signs as
they did in the initial OLS model. The health status coefficient
estimates suggest that the variables of very good health and poor health
correlate towards NOTCOV being zero. Intuition would suggest this is on
the right track - those in very good health would have cheaper insurance
premiums; those in poor health likely require health insurance to make
sure all medical expenses can be covered.

#### Logit 2

    ## 
    ## Call:
    ## glm(formula = sobj2$formula, family = binomial, data = sobj2$data)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.4886  -0.5810  -0.4161  -0.2528   2.9855  
    ## 
    ## Coefficients:
    ##              Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)  -3.05239    0.20039 -15.232  < 2e-16 ***
    ## Age          -0.40968    0.02611 -15.691  < 2e-16 ***
    ## female1      -0.10229    0.02384  -4.290 1.79e-05 ***
    ## AfAm1         0.02965    0.03538   0.838 0.402016    
    ## Asian1        0.06948    0.05137   1.353 0.176187    
    ## RaceOther1    0.25207    0.07071   3.565 0.000364 ***
    ## Hispanic1     0.51277    0.02671  19.195  < 2e-16 ***
    ## educ_hs1     -0.08193    0.03133  -2.615 0.008926 ** 
    ## educ_smcoll1 -0.33609    0.03674  -9.147  < 2e-16 ***
    ## educ_as1     -0.31491    0.04501  -6.997 2.62e-12 ***
    ## educ_bach1   -0.62559    0.04728 -13.230  < 2e-16 ***
    ## educ_adv1    -1.07014    0.08776 -12.195  < 2e-16 ***
    ## Very_Good1    0.07681    0.03210   2.393 0.016723 *  
    ## Good1         0.21421    0.03195   6.705 2.01e-11 ***
    ## Fair1         0.14093    0.04522   3.117 0.001829 ** 
    ## Poor1        -0.10433    0.08779  -1.188 0.234647    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 13281  on 15776  degrees of freedom
    ## Residual deviance: 11617  on 15761  degrees of freedom
    ## AIC: 11649
    ## 
    ## Number of Fisher Scoring iterations: 6

    ##        true
    ## pred        0     1
    ##   FALSE 53376  9478
    ##   TRUE    540   401

The results of the Logit model align with those from the OLS model. We
see a similar pattern of probability of not having health coverage.
Those with more education have a lower probability of not having health
insurance coverage. Those with very good health and those in poor health
also have a lower probability of not having health insurance. The health
status variables in the middle, Good and Fair health, while still low
probabilities, tend towards not having health insurance.

#### Random Forest Model 2

    ## 
    ## Call:
    ##  randomForest(formula = as.factor(NOTCOV) ~ ., data = sobj2$data,      importance = TRUE, proximity = TRUE) 
    ##                Type of random forest: classification
    ##                      Number of trees: 500
    ## No. of variables tried at each split: 3
    ## 
    ##         OOB estimate of  error rate: 14.55%
    ## Confusion matrix:
    ##       0   1 class.error
    ## 0 13356  71 0.005287853
    ## 1  2225 125 0.946808511

    ##                  0      1 MeanDecreaseAccuracy MeanDecreaseGini
    ## Age          19.16  27.75                29.90           216.40
    ## female        6.84  10.60                11.82            18.57
    ## AfAm         -6.89  13.46                 5.78            13.46
    ## Asian        -1.69   3.86                 1.20             8.43
    ## RaceOther     0.95   8.46                 5.78            13.51
    ## Hispanic    -15.94  32.34                32.80           185.94
    ## educ_hs      20.80 -17.11                18.17            24.58
    ## educ_smcoll  21.48   7.23                23.41            27.32
    ## educ_as      16.71   1.64                16.99            16.56
    ## educ_bach    16.14  22.43                22.76            46.30
    ## educ_adv     11.32  22.87                18.74            44.92
    ## Very_Good    -1.04   2.57                 1.16            10.51
    ## Good          0.50   2.57                 3.12            18.42
    ## Fair          4.51   1.58                 5.23            11.47
    ## Poor          1.61   4.54                 3.94             6.00

![](Lab7_files/figure-gfm/Random%20Forest%202-1.png)<!-- --> Our second
random forest model has a large increase in the false positive rate. It
jumps from 83.06% to 94.68%. Again, the relevance of this increase
depends on the context of the researcher. Pharmaceutical sales companies
developing new drugs would be concerned with such an increase in false
positives. Their sales and marketing teams would miss product placement
opportunities amongst demographics that were falsely predicted to have
low rates of health coverage.

#### SVM 2

    ##     true
    ## pred     0     1
    ##    0 52881  8620
    ##    1  1035  1259

    ##     true
    ## pred          0          1
    ##    0 0.82892076 0.13512031
    ##    1 0.01622384 0.01973509

    ## [1] 0.8486559

The second SVM model has a decrease in correct prediction rate of 0.26%.
This is a smaller change than the difference in correct prediction rates
of the Random Forest models (0.71%)

#### Elastic Net 2

#### Ridge Regression 2

#### Lasso Regression 2

#### Results Comparison 2: Regularization Regression

So after dropping some of the explanatory variables that were deemed to
be less important to the model by the Variable Important Plots and
re-running the three regularization regression models, we see that the
correct prediction rates actually went down\! This is very surprising as
we thought that dropping variables marked as not important would improve
our model and therefore improve the prediction accuracy.

It appears that the majority of the shift was from the True Falses,
which were at \~53% but are now at \~49%, to the False Positives, which
were at \~30% and are now at \~35%.

### Summary

When you summarize, you should be able to explain which models predict
best (noting if there is a tradeoff of false positive vs false negative)
and if there are certain explanatory variables that are consistently
more or less useful. Also try other lists of explanatory variables.

### Bibliography

<ftp://ftp.cdc.gov/pub/Health_Statistics/NCHS/Dataset_Documentation/NHIS/2014/personsx_layout.pdf>

<https://www.healthcare.gov/young-adults/children-under-26/>

<https://bradleyboehmke.github.io/HOML/regularized-regression.html>

Brownlee, Jason, (2016). “Support Vector Machines for Machine Learning”,
<https://machinelearningmastery.com/support-vector-machines-for-machine-learning/>

James, Gareth, Daniela Witten, Trevor Hastie, and Robert Tibshirani,
(2017). “Introduction to Statistical Learning”, New York: Springer
Science+Business Media,
<https://trevorhastie.github.io/ISLR/ISLR%20Seventh%20Printing.pdf>

Springsteen, Bruce, (1984) “Born In The USA”, *Born In The USA*,
Columbia, <https://www.youtube.com/watch?v=EPhWR4d3FJQ>
