homework 5\_plots for flights
================
Theresa Jones
9/17/2021

``` r
library(tidyverse)
library(dplyr)
glimpse(diamonds)
```

    ## Rows: 53,940
    ## Columns: 10
    ## $ carat   <dbl> 0.23, 0.21, 0.23, 0.29, 0.31, 0.24, 0.24, 0.26, 0.22, 0.23, 0.…
    ## $ cut     <ord> Ideal, Premium, Good, Premium, Good, Very Good, Very Good, Ver…
    ## $ color   <ord> E, E, E, I, J, J, I, H, E, H, J, J, F, J, E, E, I, J, J, J, I,…
    ## $ clarity <ord> SI2, SI1, VS1, VS2, SI2, VVS2, VVS1, SI1, VS2, VS1, SI1, VS1, …
    ## $ depth   <dbl> 61.5, 59.8, 56.9, 62.4, 63.3, 62.8, 62.3, 61.9, 65.1, 59.4, 64…
    ## $ table   <dbl> 55, 61, 65, 58, 58, 57, 57, 55, 61, 61, 55, 56, 61, 54, 62, 58…
    ## $ price   <int> 326, 326, 327, 334, 335, 336, 336, 337, 337, 338, 339, 340, 34…
    ## $ x       <dbl> 3.95, 3.89, 4.05, 4.20, 4.34, 3.94, 3.95, 4.07, 3.87, 4.00, 4.…
    ## $ y       <dbl> 3.98, 3.84, 4.07, 4.23, 4.35, 3.96, 3.98, 4.11, 3.78, 4.05, 4.…
    ## $ z       <dbl> 2.43, 2.31, 2.31, 2.63, 2.75, 2.48, 2.47, 2.53, 2.49, 2.39, 2.…

``` r
diamonds %>% count(cut)
```

    ## # A tibble: 5 × 2
    ##   cut           n
    ##   <ord>     <int>
    ## 1 Fair       1610
    ## 2 Good       4906
    ## 3 Very Good 12082
    ## 4 Premium   13791
    ## 5 Ideal     21551

``` r
cuts.of.diamonds <- diamonds %>% count(cut)
```

``` r
sample_frac(diamonds,.01,replace=TRUE)
```

    ## # A tibble: 539 × 10
    ##    carat cut       color clarity depth table price     x     y     z
    ##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ##  1  1.2  Premium   G     SI2      59.2    60  5278  6.92  6.9   4.09
    ##  2  0.31 Ideal     G     VS2      62.3    56   544  4.29  4.34  2.69
    ##  3  1.51 Premium   E     SI2      63      55  9302  7.34  7.3   4.61
    ##  4  1    Premium   G     VS2      61.6    58  5940  6.39  6.43  3.95
    ##  5  1.59 Ideal     I     SI2      61.6    57  7978  7.56  7.51  4.64
    ##  6  0.32 Ideal     E     VS1      61.4    55   713  4.42  4.44  2.72
    ##  7  1.76 Very Good H     SI1      63.1    59 12288  7.69  7.59  4.82
    ##  8  1.01 Very Good J     SI2      63.3    53  3088  6.35  6.31  4.01
    ##  9  0.55 Ideal     H     VVS2     61.7    57  1806  5.28  5.26  3.25
    ## 10  0.32 Ideal     G     VS2      62.1    56   524  4.36  4.4   2.72
    ## # … with 529 more rows

`{r question #3, message=FALSE, warning=FALSE, eval=TRUE   group_by(clarity) %>%   slice_max(carat, n=100) %>%   summarize(large.size.average = mean(carat, na.rm = TRUE))`

``` r
ggplot(data = diamonds) +
   geom_point(mapping = aes(x = x, y = y, color = clarity))
```

![](homework_5--working-with-diamonds-and-dplyr_files/figure-gfm/question%20#4-1.png)<!-- -->

``` r
ggplot(data = diamonds) +
   geom_point(mapping = aes(x = x, y = z, color = clarity))
```

![](homework_5--working-with-diamonds-and-dplyr_files/figure-gfm/question%20#4-2.png)<!-- -->

``` r
diamonds2 <- filter(diamonds, x > 3 & z < 10 & y < 20 & z > 2)
ggplot(data = diamonds2) +
   geom_point(mapping = aes(x = x, y = y, color = clarity))
```

![](homework_5--working-with-diamonds-and-dplyr_files/figure-gfm/question%20#5-1.png)<!-- -->

``` r
ggplot(data = diamonds2) +
   geom_point(mapping = aes(x = x, y = z, color = clarity))
```

![](homework_5--working-with-diamonds-and-dplyr_files/figure-gfm/question%20#5-2.png)<!-- -->
