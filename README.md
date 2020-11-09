
<!-- README.md is generated from README.Rmd. Please edit that file -->

# MovieShots

<!-- badges: start -->

<!-- badges: end -->

The goal of MovieShots is to provide information on shot duration in
movies. The data spans 192 movies across the century from 1915 to 2015.

## Installation

You can install MovieShots from [GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("jmelican21/MovieShots")
```

## Example

This is a basic example which shows you how to solve a common problem:

``` r
library(MovieShots)
library(tidyverse)

meandur <- MovieShots %>% group_by(year) %>% summarize(mean = mean(duration))


runtime <- MovieShots %>% group_by(year,title) %>% summarize(runtime = sum(duration)/60) #divide by 60 for minutes
```

Please analyze the data on Golf discs to answer the following questions.

### a. How has average shot duration changed over time?

SOLUTION:

``` r
ggplot(meandur,
  aes(x = year, y = mean)) +
 geom_col() + geom_smooth(se= FALSE, color = "red")+
labs(x = "Release Year", y = "Average shot duration (seconds)")
```

<img src="man/figures/README-unnamed-chunk-2-1.png" width="100%" />

As shown above, the average shot duration of movies in this dataset
peaks in 1945 at over 12 seconds before declining fairly steadily since
the 1960’s to around 3 seconds in 2015.

### b) Has total runtime changed over the past century?

SOLUTION:

``` r
ggplot(runtime,
  aes(x = year, y = runtime)) +
  geom_point() + 
  geom_smooth(se = FALSE) + 
  labs(x = "Release Year", y = "Runtime (minutes)")
```

<img src="man/figures/README-unnamed-chunk-3-1.png" width="100%" />

After increasing throughout the first half of the 20th century, average
runtime has remained fairly constant at about 120 minutes since the
1960’s.
