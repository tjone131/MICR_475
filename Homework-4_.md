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
![flightsplot](https://user-images.githubusercontent.com/89625876/145930978-ff83f1e4-2692-4f28-85eb-ed3279c08ca4.png)

   


