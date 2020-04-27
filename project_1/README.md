# Project 1: SAT & ACT Analysis


## Problem Statement

How can the College Board increase the SAT participation rate in Wisconsin?

## Contents

1) Data Import & Cleaning
2) Key trends observed in 2017 and 2018
3) Description of statistics
4) Interesting trends
5) Conclusions
6) Recommendations

### Data Import & Cleaning

Import data in csv format.

Screen data for errors using .describe() function: 
    Correct error in ACT 2017 Science score for Maryland.
    Correct error in SAT 2017 Math score for Maryland.

Fix incorrect data type:
    Convert 'Participation' column from string to integer (float) in SAT and ACT in 2017 and 2018.
    Remove 'x' from ACT 2017 'Composite'. 
    Convert 2017 and 2018 ACT 'Composite' from string to integer.
    
Rename columns in SAT and ACT in both 2017 and 2018 data.

Combine SAT and ACT test scores in 2017 and 2018.


### Description of statistics
There are limited meaning conclusions to draw from statistical inference as the data is not normal distribution. There are several ways to check for the normality of the data distribution:

1) The skewness and kurtosis of all categories are NOT zero.

2) Using Sharpiro-Wilk method, P-values of all categories are smaller than 0.05. Therefore, the null hypotheses of normality are rejected and we can assume that the data are NOT normal distribution.

3) Boxplots show that all median values are NOT equal to means.


### Key trends observed in 2017 and 2018

#### General observations
1) ACT seemed to have higher participation rates than SAT in the US.
2) SAT had lower minimum participation rate than ACT.
3) ACT had more states with 100% participation rate than SAT.

#### Common trends for both ACT and SAT
1) Total/Composite scores were negatively correlated with participation rates.
2) Total/Composite scores were highly positively correlated with sub-category scores.
3) Total/Composite scores in 2017 and 2018 were highly positively correlated. 

#### Correlations between ACT and SAT
1) Participation rates for SAT and ACT were negatively correlated.
2) Scores for SAT and ACT were negatively correlated.


### Interesting Trends

Three states (1. Illinois, 2. Colorado and 3. Rhode Island) have demonstrated significant increase in their SAT participation rates from 2017 to 2018. See following for possible reasons:

1) Illinois State Board of Education has ended its contract with ACT as the College Board earlier won a three-year, $14.3 million bid to give its exam to all public high school juniors in Illinois in 2016.(source: https://www.chicagotribune.com/news/ct-illinois-chooses-sat-met-20160211-story.html)

2) In Colorado, the state Department of Education announced in 2015 that a selection committee chose The College Board, makers of the SAT, over the ACT testing company, through a competitive bidding process.(source:https://chalkbeat.org/posts/co/2015/12/23/goodbye-act-hello-sat-a-significant-change-for-colorado-high-schoolers/)

3) In 2018, the SATs and PSATs became a graduation requirement, part of the Rhode Island’s college admission test.(source:https://www.providencejournal.com/news/20181025/with-sat-required-ri-sees-jump-in-participation-decline-in-scores)


### Conclusions 

1) ACT is a competitor of SAT.
2) 100% participation rates are observed in states that mandate either SAT or ACT.
3) The participation rates for ACT and SAT are highly dependent on the States that usually engage SAT and ACT through the government bidding process.
4) States without mandatory SAT or ACT requirements are likely to have participation rates higher than 50%.


### Recommendations

The College Board could target Wisconsin, given the following reasons:
    1) Wisconsin mandates student from public schools to take ACT - potential to achieve 100%
    2) Wisconsin had the third lowest participation rate (0.03) in 2018
    3) Wisconsin's public high school student population was larger than Iowa, North Dakota and Wyoming (source: https://educationdata.org/number-of-public-schools/)
    
Win contracts with the Wisconsin Department of Education to make SAT mandatory, the College Board can aim undercut ACT when Wisconsin’s contract with ACT ends.  
    1) Wisconsin state is likely to prioritise cost reduction over the next few years as the US government has only approved a state budget which was half the amount of what was requested by Wisconsin in 2019 (source: https://www.wuwm.com/post/budget-compromise-gives-wisconsin-schools-half-funding-boost-evers-wanted#stream/0)
    2) Assumptions: Wisconsin’s contract duration with ACT will end in 2020 and Wisconsin will continue to mandate SAT/ACT
    Other considerations include offering free SAT to students 


