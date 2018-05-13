Week 9 Practice 1
================
Yu-Wen Pu
2018-04-24

``` r
knitr::opts_chunk$set(results = "hold", fig.retina = 2)
set.seed(1830)
```

語法說明
--------

``` r
# both are the same
dataset <- edit(dataset)
fix(dataset)
```

``` r
apply(x, margin, fun)
# x: data object
# margin: 1 for rows, 2 for columns
# fun: apply this function to data object
```

模擬樣本分佈
------------

``` r
survey <- read.table("../week7/2018class.csv", header = TRUE, sep = ",")
x <- survey$height
length(x)
mean(x)
sd(x)
head(x)
```

    ## [1] 34
    ## [1] 165.3529
    ## [1] 8.373415
    ## [1] 153 162 158 176 181 181

``` r
y <- data.frame(p1 = numeric(0), p2 = numeric(0), p3 = numeric(0),
                p4 = numeric(0), p5 = numeric(0), mean = numeric(0),
                sd = numeric(0), low_critical_val = numeric(0),
                high_critical_val = numeric(0), p_val = numeric(0))
y <- edit(y)
y
```

    ##    p1  p2  p3  p4  p5 mean sd low_critical_val high_critical_val p_val
    ## 1 176 163 168 181 174   NA NA               NA                NA    NA
    ## 2 163 151 157 175 176   NA NA               NA                NA    NA
    ## 3 175 163 176 176 175   NA NA               NA                NA    NA
    ## 4 176 157 176 176 165   NA NA               NA                NA    NA
    ## 5 165 162 165 163 176   NA NA               NA                NA    NA

``` r
n_samples <- nrow(y)  # number of rows
for (i in 1:n_samples) {
    print(i)
    y$mean[i] <- apply(y[i, c(1:5)], 1, mean)
    y$sd[i] <- apply(y[i, c(1:5)], 1, sd)
    y$low_critical_val[i] <- y$mean[i] - 1.96 * y$sd[i]
    y$high_critical_val[i] <- y$mean[i] + 1.96 * y$sd[i]
    if (y$mean[i] > mean(x)) {
        y$p_val[i] <- format(round(pnorm(y$mean[i], mean = mean(x),
                                         sd = sd(x), lower.tail = FALSE),
                                   digits = 3),
                             nsmall = 3)  # minimum number of digits
    } else {
        y$p_val[i] <- format(round(pnorm(y$mean[i], mean = mean(x),
                                         sd = sd(x), lower.tail = TRUE),
                                   digits = 3),
                             nsmall = 3)
    }
}
```

    ## [1] 1
    ## [1] 2
    ## [1] 3
    ## [1] 4
    ## [1] 5

``` r
y
write.csv(y, file = "height.csv", row.names = FALSE)  # output to csv
```

    ##    p1  p2  p3  p4  p5  mean        sd low_critical_val high_critical_val
    ## 1 176 163 168 181 174 172.4  7.021396         158.6381          186.1619
    ## 2 163 151 157 175 176 164.4 10.990905         142.8578          185.9422
    ## 3 175 163 176 176 175 173.0  5.612486         161.9995          184.0005
    ## 4 176 157 176 176 165 170.0  8.689074         152.9694          187.0306
    ## 5 165 162 165 163 176 166.2  5.630275         155.1647          177.2353
    ##   p_val
    ## 1 0.200
    ## 2 0.455
    ## 3 0.181
    ## 4 0.289
    ## 5 0.460
