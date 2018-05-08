Week 11 Practice 1
================
Yu-Wen Pu
2018-05-08

卡方分佈的修正
--------------

``` r
knitr::opts_chunk$set(results = "hold", fig.retina = 2)
set.seed(1830)
```

### part 1

``` r
x <- matrix(c(13, 36, 14, 30), byrow = TRUE, ncol = 2)
chisq.test(x, correct = FALSE)
```

    ## 
    ##  Pearson's Chi-squared test
    ## 
    ## data:  x
    ## X-squared = 0.31458, df = 1, p-value = 0.5749

``` r
chisq.test(x, correct = TRUE)
```

    ## 
    ##  Pearson's Chi-squared test with Yates' continuity correction
    ## 
    ## data:  x
    ## X-squared = 0.11029, df = 1, p-value = 0.7398

### part 2

``` r
fisher.test(x, alternative = "two.sided")
```

    ## 
    ##  Fisher's Exact Test for Count Data
    ## 
    ## data:  x
    ## p-value = 0.6501
    ## alternative hypothesis: true odds ratio is not equal to 1
    ## 95 percent confidence interval:
    ##  0.2859687 2.0897821
    ## sample estimates:
    ## odds ratio 
    ##  0.7759623

``` r
fisher.test(x, alternative = "greater")
```

    ## 
    ##  Fisher's Exact Test for Count Data
    ## 
    ## data:  x
    ## p-value = 0.7852
    ## alternative hypothesis: true odds ratio is greater than 1
    ## 95 percent confidence interval:
    ##  0.3309917       Inf
    ## sample estimates:
    ## odds ratio 
    ##  0.7759623

``` r
fisher.test(x, alternative = "less")
```

    ## 
    ##  Fisher's Exact Test for Count Data
    ## 
    ## data:  x
    ## p-value = 0.3695
    ## alternative hypothesis: true odds ratio is less than 1
    ## 95 percent confidence interval:
    ##  0.000000 1.809645
    ## sample estimates:
    ## odds ratio 
    ##  0.7759623

### part 3

``` r
x <- matrix(c(370, 352, 198, 187, 359, 290, 110, 160), byrow = TRUE, nrow = 2,
            dimnames = list(c("female", "male"), c("blue", "brown", "green", "hazel")))
x
```

    ##        blue brown green hazel
    ## female  370   352   198   187
    ## male    359   290   110   160

``` r
chisq.test(x, correct = FALSE)
```

    ## 
    ##  Pearson's Chi-squared test
    ## 
    ## data:  x
    ## X-squared = 16.091, df = 3, p-value = 0.001087

``` r
fisher.test(x, alternative = "two.sided")
```

    ## 
    ##  Fisher's Exact Test for Count Data
    ## 
    ## data:  x
    ## p-value = 0.00101
    ## alternative hypothesis: two.sided

### part 4

``` r
x <- matrix(c(41, 80, 385, 290, 477, 499), nrow = 2)
result <- chisq.test(x, correct = FALSE)
str(result)
```

    ## List of 9
    ##  $ statistic: Named num 25.8
    ##   ..- attr(*, "names")= chr "X-squared"
    ##  $ parameter: Named int 2
    ##   ..- attr(*, "names")= chr "df"
    ##  $ p.value  : num 2.51e-06
    ##  $ method   : chr "Pearson's Chi-squared test"
    ##  $ data.name: chr "x"
    ##  $ observed : num [1:2, 1:3] 41 80 385 290 477 499
    ##  $ expected : num [1:2, 1:3] 61.7 59.3 344 331 497.4 ...
    ##  $ residuals: num [1:2, 1:3] -2.631 2.682 2.212 -2.255 -0.913 ...
    ##  $ stdres   : num [1:2, 1:3] -3.89 3.89 4.01 -4.01 -1.95 ...
    ##  - attr(*, "class")= chr "htest"

``` r
result$statistic
```

    ## X-squared 
    ##  25.79365

``` r
result$expected
```

    ##          [,1]     [,2]     [,3]
    ## [1,] 61.66084 343.9757 497.3634
    ## [2,] 59.33916 331.0243 478.6366
