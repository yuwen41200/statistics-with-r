Week 13 Practice 1
================
Yu-Wen Pu
2018-05-22

regression
----------

``` r
knitr::opts_chunk$set(results = "hold", fig.retina = 2)
set.seed(1830)
```

### residual

``` r
d <- read.table("../week12a/Tab10-1.dat", header = TRUE, sep = "")
```

``` r
sym_avg <- mean(d$Symptoms)
d$sym_dev <- d$Symptoms - sym_avg
sum(d$sym_dev)  # almost 0
```

    ## [1] 3.836931e-13

``` r
str_avg <- mean(d$Stress)
d$str_dev <- d$Stress - str_avg
sum(d$str_dev)  # almost 0
```

    ## [1] -1.172396e-13

``` r
d$sym_hat <- predict(lm(d$Symptoms ~ d$Stress))
d$residual <- d$Symptoms - d$sym_hat
sum(d$residual)  # almost 0
```

    ## [1] -9.663381e-13

``` r
d <- d[order(d$Stress, decreasing = TRUE), ]
head(d, 4)
tail(d, 4)
```

    ##    id Stress Symptoms  sym_dev  str_dev  sym_hat   residual
    ## 55 55     74      117 26.29907 52.53271 131.8401 -14.840062
    ## 72 72     58      102 11.29907 36.53271 119.3102 -17.310230
    ## 28 28     45      131 40.29907 23.53271 109.1297  21.870259
    ## 30 30     45      107 16.29907 23.53271 109.1297  -2.129741
    ##    id Stress Symptoms    sym_dev   str_dev  sym_hat   residual
    ## 85 85      3      100   9.299065 -18.46729 76.23893  23.761068
    ## 58 58      2       61 -29.700935 -19.46729 75.45582 -14.455817
    ## 51 51      1       68 -22.700935 -20.46729 74.67270  -6.672703
    ## 84 84      1       65 -25.700935 -20.46729 74.67270  -9.672703

### standardized regression coefficient (beta)

``` r
library(boot)
library(QuantPsyc)
```

    ## Loading required package: MASS

    ## 
    ## Attaching package: 'QuantPsyc'

    ## The following object is masked from 'package:base':
    ## 
    ##     norm

``` r
lm.beta(lm(d$Symptoms ~ d$Stress))
```

    ##  d$Stress 
    ## 0.5060454
