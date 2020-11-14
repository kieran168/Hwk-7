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

Some of the estimation procedures are not as tolerant about factors so
we need to set those as dummies. Some are also intolerant of NA values.
I’ll show the code for the basic set of explanatory variables, which you
can modify as you see fit.

    ##      NOTCOV            Age            female            AfAm       
    ##  Min.   :0.0000   Min.   :17.00   Min.   :0.0000   Min.   :0.0000  
    ##  1st Qu.:0.0000   1st Qu.:30.00   1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Median :0.0000   Median :44.00   Median :1.0000   Median :0.0000  
    ##  Mean   :0.1537   Mean   :43.94   Mean   :0.5205   Mean   :0.1415  
    ##  3rd Qu.:0.0000   3rd Qu.:57.00   3rd Qu.:1.0000   3rd Qu.:0.0000  
    ##  Max.   :1.0000   Max.   :75.00   Max.   :1.0000   Max.   :1.0000  
    ##      Asian           RaceOther          Hispanic         educ_hs      
    ##  Min.   :0.00000   Min.   :0.00000   Min.   :0.0000   Min.   :0.0000  
    ##  1st Qu.:0.00000   1st Qu.:0.00000   1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Median :0.00000   Median :0.00000   Median :0.0000   Median :0.0000  
    ##  Mean   :0.07181   Mean   :0.01866   Mean   :0.2038   Mean   :0.2623  
    ##  3rd Qu.:0.00000   3rd Qu.:0.00000   3rd Qu.:0.0000   3rd Qu.:1.0000  
    ##  Max.   :1.00000   Max.   :1.00000   Max.   :1.0000   Max.   :1.0000  
    ##   educ_smcoll        educ_as         educ_bach         educ_adv      
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :0.0000   Min.   :0.00000  
    ##  1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.00000  
    ##  Median :0.0000   Median :0.0000   Median :0.0000   Median :0.00000  
    ##  Mean   :0.1884   Mean   :0.1071   Mean   :0.1726   Mean   :0.09588  
    ##  3rd Qu.:0.0000   3rd Qu.:0.0000   3rd Qu.:0.0000   3rd Qu.:0.00000  
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :1.0000   Max.   :1.00000  
    ##     married          widowed          divorc_sep     Region.Midwest  
    ##  Min.   :0.0000   Min.   :0.00000   Min.   :0.0000   Min.   :0.0000  
    ##  1st Qu.:0.0000   1st Qu.:0.00000   1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Median :1.0000   Median :0.00000   Median :0.0000   Median :0.0000  
    ##  Mean   :0.5351   Mean   :0.02987   Mean   :0.1089   Mean   :0.1996  
    ##  3rd Qu.:1.0000   3rd Qu.:0.00000   3rd Qu.:0.0000   3rd Qu.:0.0000  
    ##  Max.   :1.0000   Max.   :1.00000   Max.   :1.0000   Max.   :1.0000  
    ##   Region.South     Region.West     born.Mex.CentAm.Carib   born.S.Am      
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :0.0000        Min.   :0.00000  
    ##  1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.0000        1st Qu.:0.00000  
    ##  Median :0.0000   Median :0.0000   Median :0.0000        Median :0.00000  
    ##  Mean   :0.3459   Mean   :0.2894   Mean   :0.1149        Mean   :0.01183  
    ##  3rd Qu.:1.0000   3rd Qu.:1.0000   3rd Qu.:0.0000        3rd Qu.:0.00000  
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :1.0000        Max.   :1.00000  
    ##     born.Eur        born.f.USSR        born.Africa         born.MidE       
    ##  Min.   :0.00000   Min.   :0.000000   Min.   :0.000000   Min.   :0.000000  
    ##  1st Qu.:0.00000   1st Qu.:0.000000   1st Qu.:0.000000   1st Qu.:0.000000  
    ##  Median :0.00000   Median :0.000000   Median :0.000000   Median :0.000000  
    ##  Mean   :0.01413   Mean   :0.002664   Mean   :0.008144   Mean   :0.004273  
    ##  3rd Qu.:0.00000   3rd Qu.:0.000000   3rd Qu.:0.000000   3rd Qu.:0.000000  
    ##  Max.   :1.00000   Max.   :1.000000   Max.   :1.000000   Max.   :1.000000  
    ##  born.India.subc     born.Asia        born.SE.Asia     born.elsewhere   
    ##  Min.   :0.00000   Min.   :0.00000   Min.   :0.00000   Min.   :0.00000  
    ##  1st Qu.:0.00000   1st Qu.:0.00000   1st Qu.:0.00000   1st Qu.:0.00000  
    ##  Median :0.00000   Median :0.00000   Median :0.00000   Median :0.00000  
    ##  Mean   :0.01328   Mean   :0.01382   Mean   :0.02384   Mean   :0.00514  
    ##  3rd Qu.:0.00000   3rd Qu.:0.00000   3rd Qu.:0.00000   3rd Qu.:0.00000  
    ##  Max.   :1.00000   Max.   :1.00000   Max.   :1.00000   Max.   :1.00000  
    ##   born.unknown     
    ##  Min.   :0.000000  
    ##  1st Qu.:0.000000  
    ##  Median :0.000000  
    ##  Mean   :0.002878  
    ##  3rd Qu.:0.000000  
    ##  Max.   :1.000000

Next create a common data object that is standardized (check what it
does\! run summary(sobj$data) ) and split into training and test sets. I
have to use a very small training set to prevent my little laptop from
running out of memory. You can try a bigger value like max=0.75 or
similar. Summary(restrict\_1) will tell you how many are in the training
set vs test.

    ## Loading required package: standardize

    ## Warning: package 'standardize' was built under R version 4.0.3

    ## [1] 79572

    ##    Mode   FALSE    TRUE 
    ## logical   66393   13179

    ##      NOTCOV              Age.V1        female   AfAm      Asian     RaceOther
    ##  Min.   :0.0000   Min.   :-1.6923561   1:6914   1: 1884   1:  924   1:  244  
    ##  1st Qu.:0.0000   1st Qu.:-0.8766675   0:6265   0:11295   0:12255   0:12935  
    ##  Median :0.0000   Median : 0.0017663                                         
    ##  Mean   :0.1487   Mean   : 0.0000000                                         
    ##  3rd Qu.:0.0000   3rd Qu.: 0.8174549                                         
    ##  Max.   :1.0000   Max.   : 1.9468699                                         
    ##  Hispanic  educ_hs  educ_smcoll educ_as   educ_bach educ_adv  married 
    ##  1: 2672   1:3358   1: 2457     1: 1516   1: 2305   1: 1308   1:7143  
    ##  0:10507   0:9821   0:10722     0:11663   0:10874   0:11871   0:6036  
    ##                                                                       
    ##                                                                       
    ##                                                                       
    ##                                                                       
    ##  widowed   divorc_sep Region.Midwest Region.South Region.West
    ##  1:  373   1: 1419    1: 2576        1:4539       1:3863     
    ##  0:12806   0:11760    0:10603        0:8640       0:9316     
    ##                                                              
    ##                                                              
    ##                                                              
    ##                                                              
    ##  born.Mex.CentAm.Carib born.S.Am born.Eur  born.f.USSR born.Africa born.MidE
    ##  1: 1523               1:  136   1:  182   1:   35     1:  118     1:   52  
    ##  0:11656               0:13043   0:12997   0:13144     0:13061     0:13127  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##  born.India.subc born.Asia born.SE.Asia born.elsewhere born.unknown
    ##  1:  159         1:  183   1:  289      1:   89        1:   35     
    ##  0:13020         0:12996   0:12890      0:13090        0:13144     
    ##                                                                    
    ##                                                                    
    ##                                                                    
    ## 

Then start with some models. I’ll give code for the Linear Probability
Model (ie good ol’ OLS) and logit, to show how to call those with the
standarized object. \#\#\# LPM and OLS

You can play around to see if the “predvals \> 0.5” cutoff is best.
These give a table about how the models predict.

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

\#\#\#Bibliography
<ftp://ftp.cdc.gov/pub/Health_Statistics/NCHS/Dataset_Documentation/NHIS/2014/personsx_layout.pdf>

<https://www.healthcare.gov/young-adults/children-under-26/>

James, Gareth, Daniela Witten, Trevor Hastie, and Robert Tibshirani,
(2017). Introduction to Statistical Learning. New York: Springer
Science+Business Media,
<https://trevorhastie.github.io/ISLR/ISLR%20Seventh%20Printing.pdf>
