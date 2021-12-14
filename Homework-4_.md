Homework 4\_
================
Theresa Jones
9/10/2021

``` r
library("tidyverse")
a <- 3
b <- 2
sum(a,b)
```

    ## [1] 5

``` r
library("nycflights13")
```

now we’re going to make the AA data frame

``` r
data("flights")
AA_flights <- filter(flights, carrier == "AA")

ggplot(data = AA_flights) + 
  geom_point(mapping = aes(x = dep_delay, y = arr_delay))
```

    ## Warning: Removed 782 rows containing missing values (geom_point).

![](Homework-4__files/figure-gfm/homework%20parte%20tres-1.png)<!-- -->
