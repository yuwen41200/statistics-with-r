Week 5 Practice 1
================
Yu-Wen Pu
2018/3/27

Normal Distribution
-------------------

``` r
dnorm(x = 1, mean = 0, sd = 1)  # density
```

    ## [1] 0.2419707

``` r
rnorm(n = 10, mean = 0, sd = 1)  # random generation
```

    ##  [1] -0.3100351  1.5190127  0.2891615  0.9616945 -0.5621757  0.5560993
    ##  [7]  1.1373688  2.0761147 -0.4159112  0.7598759

``` r
pnorm(2, mean = 0, sd = 1)  # distribution function
```

    ## [1] 0.9772499

``` r
pnorm(-1, mean = 0, sd = 1)
```

    ## [1] 0.1586553

``` r
test <- pnorm(-1, mean = 0, sd = 1)
qnorm(test, mean = 0, sd = 1)  # quantile function
```

    ## [1] -1
