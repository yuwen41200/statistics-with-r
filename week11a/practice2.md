Week 11 Practice 2
================
Yu-Wen Pu
2018-05-08

Correlation
-----------

``` r
knitr::opts_chunk$set(results = "hold", fig.retina = 2)
set.seed(1830)
```

### part 1

``` r
x <- read.table("Fig9-1.dat", header = TRUE, sep = "")
dim(x)
str(x)
head(x)
```

    ## [1] 18  3
    ## 'data.frame':    18 obs. of  3 variables:
    ##  $ Doctors: num  11.5 13.4 19.8 12.5 16.8 19.5 11.4 15.4 18.3 13.7 ...
    ##  $ Infmort: num  -2.5 -2 6.6 -2.2 3 8.5 -5.8 1.5 7.5 -5 ...
    ##  $ Country: Factor w/ 18 levels "Australi","Austria",..: 10 6 2 13 3 11 7 17 9 12 ...
    ##   Doctors Infmort  Country
    ## 1    11.5    -2.5  Ireland
    ## 2    13.4    -2.0 Eng-Wale
    ## 3    19.8     6.6  Austria
    ## 4    12.5    -2.2 New_Zeal
    ## 5    16.8     3.0  Belgium
    ## 6    19.5     8.5    Italy

``` r
plot(x$Doctors, x$Infmort, xlab = "physicians per 10000 population",
     ylab = "infant mortality", pch = 19)
abline(lm(x$Infmort ~ x$Doctors), col = "red")
```

<img src="practice2_files/figure-markdown_github/a-1.png" width="672" />
