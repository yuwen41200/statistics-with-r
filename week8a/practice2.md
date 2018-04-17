Week 8 Practice 2
================
Yu-Wen Pu
2018-04-17

``` r
knitr::opts_chunk$set(results = "hold", fig.retina = 2)
set.seed(1830)
```

Factor (Category, Enum) Data Type
---------------------------------

##### 輸出都一樣

``` r
gender <- c("FEMALE", "MALE", "FEMALE", "FEMALE")
gender
```

    ## [1] "FEMALE" "MALE"   "FEMALE" "FEMALE"

``` r
gender1 <- as.factor(gender)
gender1
```

    ## [1] FEMALE MALE   FEMALE FEMALE
    ## Levels: FEMALE MALE

``` r
(gender2 <- as.factor(gender))
```

    ## [1] FEMALE MALE   FEMALE FEMALE
    ## Levels: FEMALE MALE

``` r
gender3 <- factor(gender)
gender3
```

    ## [1] FEMALE MALE   FEMALE FEMALE
    ## Levels: FEMALE MALE

##### 實際用法

``` r
x <- c(3, 2, 1, 2, 3, 2, 3, 1, 1, 2, 3, 2, 3, 1)
x <- factor(x, ordered = TRUE, levels = c(1, 2, 3), labels = c("LOW", "MEDIAN", "HIGH"))
x
```

    ##  [1] HIGH   MEDIAN LOW    MEDIAN HIGH   MEDIAN HIGH   LOW    LOW    MEDIAN
    ## [11] HIGH   MEDIAN HIGH   LOW   
    ## Levels: LOW < MEDIAN < HIGH

##### 計算次數

``` r
table(x)
```

    ## x
    ##    LOW MEDIAN   HIGH 
    ##      4      5      5

List Data Type
--------------

``` r
a <- "a sample string"
b <- c(1:20)
c <- matrix(1:12, nrow = 4)
d <- c("xxx", "yyyy", "zzzzz")
x <- list(title = a, week = b, c, d)
x
```

    ## $title
    ## [1] "a sample string"
    ## 
    ## $week
    ##  [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
    ## 
    ## [[3]]
    ##      [,1] [,2] [,3]
    ## [1,]    1    5    9
    ## [2,]    2    6   10
    ## [3,]    3    7   11
    ## [4,]    4    8   12
    ## 
    ## [[4]]
    ## [1] "xxx"   "yyyy"  "zzzzz"

``` r
x[2]  # 傳回值和相關資訊
x[[2]]  # 只傳回值
x[["week"]]
x$week
```

    ## $week
    ##  [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
    ## 
    ##  [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
    ##  [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
    ##  [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

Logical Operators in R
----------------------

``` r
a <- 1
b <- "1"

a == b  # implicit type conversion
a != b
a < b
a <= b
a > b
a >= b
```

    ## [1] TRUE
    ## [1] FALSE
    ## [1] FALSE
    ## [1] TRUE
    ## [1] FALSE
    ## [1] TRUE

If-Else
-------

``` r
if (a == 1) {
    print("a == 1 is TRUE")
}

if (a) {
    print("1 is TRUE")
}

a <- -1
if (a) {
    print("-1 is TRUE")
}

a <- 0
if (a) {
    print("0 is TRUE")
} else {
    print("0 is FALSE")
}

if (FALSE) {
    print()
} else if (TRUE) {
    print("here")
} else {
    print()
}
```

    ## [1] "a == 1 is TRUE"
    ## [1] "1 is TRUE"
    ## [1] "-1 is TRUE"
    ## [1] "0 is FALSE"
    ## [1] "here"

Functions
---------

``` r
f <- function(x) {
    cat("x =", x)
}
f(82)
```

    ## x = 82

Loops
-----

##### for

``` r
for (i in 1:10) {
    if (i == 7)  # 可省略括號
        next  # 相當於 continue
    cat("i =", i, "\n")
}
```

    ## i = 1 
    ## i = 2 
    ## i = 3 
    ## i = 4 
    ## i = 5 
    ## i = 6 
    ## i = 8 
    ## i = 9 
    ## i = 10

##### while

``` r
i <- 1
while (i <= 3) {
    cat("i =", i, "\n")
    i <- i + 1
}
```

    ## i = 1 
    ## i = 2 
    ## i = 3
