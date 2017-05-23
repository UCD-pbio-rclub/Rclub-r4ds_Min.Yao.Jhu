# Exploratory Data Analysis
Min-Yao  
2017年5月21日  

# 7 Exploratory Data Analysis

## 7.1 Introduction

### 7.1.1 Prerequisites


```r
library(tidyverse)
```

```
## Warning: package 'tidyverse' was built under R version 3.3.3
```

```
## Loading tidyverse: ggplot2
## Loading tidyverse: tibble
## Loading tidyverse: tidyr
## Loading tidyverse: readr
## Loading tidyverse: purrr
## Loading tidyverse: dplyr
```

```
## Warning: package 'purrr' was built under R version 3.3.3
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```

## 7.2 Questions

## 7.3 Variation

### 7.3.1 Visualising distributions


```r
ggplot(data = diamonds) +
  geom_bar(mapping = aes(x = cut))
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
diamonds %>% 
  count(cut)
```

```
## # A tibble: 5 × 2
##         cut     n
##       <ord> <int>
## 1      Fair  1610
## 2      Good  4906
## 3 Very Good 12082
## 4   Premium 13791
## 5     Ideal 21551
```

```r
ggplot(data = diamonds) +
  geom_histogram(mapping = aes(x = carat), binwidth = 0.5)
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-2-2.png)<!-- -->

```r
diamonds %>% 
  count(cut_width(carat, 0.5))
```

```
## # A tibble: 11 × 2
##    `cut_width(carat, 0.5)`     n
##                     <fctr> <int>
## 1             [-0.25,0.25]   785
## 2              (0.25,0.75] 29498
## 3              (0.75,1.25] 15977
## 4              (1.25,1.75]  5313
## 5              (1.75,2.25]  2002
## 6              (2.25,2.75]   322
## 7              (2.75,3.25]    32
## 8              (3.25,3.75]     5
## 9              (3.75,4.25]     4
## 10             (4.25,4.75]     1
## 11             (4.75,5.25]     1
```

```r
smaller <- diamonds %>% 
  filter(carat < 3)
  
ggplot(data = smaller, mapping = aes(x = carat)) +
  geom_histogram(binwidth = 0.1)
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-2-3.png)<!-- -->

```r
ggplot(data = smaller, mapping = aes(x = carat, colour = cut)) +
  geom_freqpoly(binwidth = 0.1)
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-2-4.png)<!-- -->


### 7.3.2 Typical values


```r
ggplot(data = smaller, mapping = aes(x = carat)) +
  geom_histogram(binwidth = 0.01)
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

```r
ggplot(data = faithful, mapping = aes(x = eruptions)) + 
  geom_histogram(binwidth = 0.25)
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-3-2.png)<!-- -->


### 7.3.3 Unusual values


```r
ggplot(diamonds) + 
  geom_histogram(mapping = aes(x = y), binwidth = 0.5)
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```r
ggplot(diamonds) + 
  geom_histogram(mapping = aes(x = y), binwidth = 0.5) +
  coord_cartesian(ylim = c(0, 50))
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-4-2.png)<!-- -->

```r
unusual <- diamonds %>% 
  filter(y < 3 | y > 20) %>% 
  select(price, x, y, z) %>%
  arrange(y)
unusual
```

```
## # A tibble: 9 × 4
##   price     x     y     z
##   <int> <dbl> <dbl> <dbl>
## 1  5139  0.00   0.0  0.00
## 2  6381  0.00   0.0  0.00
## 3 12800  0.00   0.0  0.00
## 4 15686  0.00   0.0  0.00
## 5 18034  0.00   0.0  0.00
## 6  2130  0.00   0.0  0.00
## 7  2130  0.00   0.0  0.00
## 8  2075  5.15  31.8  5.12
## 9 12210  8.09  58.9  8.06
```


### 7.3.4 Exercises

1.Explore the distribution of each of the x, y, and z variables in diamonds. What do you learn? Think about a diamond and how you might decide which dimension is the length, width, and depth.


```r
?diamonds
```

```
## starting httpd help server ...
```

```
##  done
```

```r
ggplot(diamonds) + 
  geom_histogram(mapping = aes(x = x), binwidth = 0.5)
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
ggplot(diamonds) + 
  geom_histogram(mapping = aes(x = y), binwidth = 0.5)
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-5-2.png)<!-- -->

```r
ggplot(diamonds) + 
  geom_histogram(mapping = aes(x = z), binwidth = 0.5)
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-5-3.png)<!-- -->

> x=length in mm (0–10.74), y= width in mm (0–58.9), z= depth in mm (0–31.8)

2.Explore the distribution of price. Do you discover anything unusual or surprising? (Hint: Carefully think about the binwidth and make sure you try a wide range of values.)


```r
ggplot(diamonds) + 
  geom_histogram(mapping = aes(x = price), binwidth = 100)
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

```r
ggplot(diamonds) + 
  geom_histogram(mapping = aes(x = price), binwidth = 100) +
  coord_cartesian(ylim = c(0, 500))
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-6-2.png)<!-- -->

> There is a sharply dropping at around $1300 

3.How many diamonds are 0.99 carat? How many are 1 carat? What do you think is the cause of the difference?


```r
ggplot(data = diamonds) +
  geom_histogram(mapping = aes(x = carat), binwidth = 0.01)
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

```r
diamonds %>% 
  count(carat)
```

```
## # A tibble: 273 × 2
##    carat     n
##    <dbl> <int>
## 1   0.20    12
## 2   0.21     9
## 3   0.22     5
## 4   0.23   293
## 5   0.24   254
## 6   0.25   212
## 7   0.26   253
## 8   0.27   233
## 9   0.28   198
## 10  0.29   130
## # ... with 263 more rows
```

> 23 diamonds are 0.99 carat. 1558 diamonds are 1 carat. I think the cause of the difference is price because 1 carat diamonds are much more expensive than 0.99 carat.

4.Compare and contrast coord_cartesian() vs xlim() or ylim() when zooming in on a histogram. What happens if you leave binwidth unset? What happens if you try and zoom so only half a bar shows?


```r
ggplot(diamonds) + 
  geom_histogram(mapping = aes(x = y), binwidth = 0.5) +
  coord_cartesian(ylim = c(0, 50))
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

```r
ggplot(diamonds) + 
  geom_histogram(mapping = aes(x = y), binwidth = 0.5) +
  ylim(0, 50)
```

```
## Warning: Removed 11 rows containing missing values (geom_bar).
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-8-2.png)<!-- -->

```r
ggplot(diamonds) + 
  geom_histogram(mapping = aes(x = y), binwidth = 0.5) +
  xlim(0, 50)
```

```
## Warning: Removed 1 rows containing non-finite values (stat_bin).
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-8-3.png)<!-- -->

> xlim() or ylim() removes data points outside of the given range

## 7.4 Missing values


```r
diamonds2 <- diamonds %>% 
  filter(between(y, 3, 20))

ggplot(data = diamonds2, mapping = aes(x = x, y = y)) + 
  geom_point()
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

```r
diamonds2 <- diamonds %>% 
  mutate(y = ifelse(y < 3 | y > 20, NA, y))

ggplot(data = diamonds2, mapping = aes(x = x, y = y)) + 
  geom_point()
```

```
## Warning: Removed 9 rows containing missing values (geom_point).
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-9-2.png)<!-- -->

```r
ggplot(data = diamonds2, mapping = aes(x = x, y = y)) + 
  geom_point(na.rm = TRUE)
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-9-3.png)<!-- -->


```r
nycflights13::flights %>% 
  mutate(
    cancelled = is.na(dep_time),
    sched_hour = sched_dep_time %/% 100,
    sched_min = sched_dep_time %% 100,
    sched_dep_time = sched_hour + sched_min / 60
  ) %>% 
  ggplot(mapping = aes(sched_dep_time)) + 
    geom_freqpoly(mapping = aes(colour = cancelled), binwidth = 1/4)
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-10-1.png)<!-- -->


### 7.4.1 Exercises

1.What happens to missing values in a histogram? What happens to missing values in a bar chart? Why is there a difference?


```r
diamonds2 <- diamonds %>% 
  mutate(y = ifelse(y < 3 | y > 20, NA, y))

ggplot(diamonds2) + 
  geom_histogram(mapping = aes(x = y), binwidth = 0.5)
```

```
## Warning: Removed 9 rows containing non-finite values (stat_bin).
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

```r
ggplot(diamonds2) +
  geom_bar(mapping = aes(x = y))
```

```
## Warning: Removed 9 rows containing non-finite values (stat_count).
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-11-2.png)<!-- -->

> ggplot2 doesn’t include them in the plot, but it does warn that they’ve been removed.

2.What does na.rm = TRUE do in mean() and sum()?


```r
?mean
?sum()
```

> `na.rm` a logical value indicating whether NA values should be stripped before the computation proceeds.
> If na.rm is FALSE an NA or NaN value in any of the arguments will cause a value of NA or NaN to be returned, otherwise NA and NaN values are ignored.


## 7.5 Covariation

### 7.5.1 A categorical and continuous variable


#### 7.5.1.1 Exercises

1.Use what you’ve learned to improve the visualisation of the departure times of cancelled vs. non-cancelled flights.

2.What variable in the diamonds dataset is most important for predicting the price of a diamond? How is that variable correlated with cut? Why does the combination of those two relationships lead to lower quality diamonds being more expensive?

3.Install the ggstance package, and create a horizontal boxplot. How does this compare to using coord_flip()?

4.One problem with boxplots is that they were developed in an era of much smaller datasets and tend to display a prohibitively large number of “outlying values”. One approach to remedy this problem is the letter value plot. Install the lvplot package, and try using geom_lv() to display the distribution of price vs cut. What do you learn? How do you interpret the plots?

5.Compare and contrast geom_violin() with a facetted geom_histogram(), or a coloured geom_freqpoly(). What are the pros and cons of each method?

6.If you have a small dataset, it’s sometimes useful to use geom_jitter() to see the relationship between a continuous and categorical variable. The ggbeeswarm package provides a number of methods similar to geom_jitter(). List them and briefly describe what each one does.

### 7.5.2 Two categorical variables

#### 7.5.2.1 Exercises

1.How could you rescale the count dataset above to more clearly show the distribution of cut within colour, or colour within cut?

2.Use geom_tile() together with dplyr to explore how average flight delays vary by destination and month of year. What makes the plot difficult to read? How could you improve it?

3.Why is it slightly better to use aes(x = color, y = cut) rather than aes(x = cut, y = color) in the example above?

### 7.5.3 Two continuous variables

#### 7.5.3.1 Exercises

1.Instead of summarising the conditional distribution with a boxplot, you could use a frequency polygon. What do you need to consider when using cut_width() vs cut_number()? How does that impact a visualisation of the 2d distribution of carat and price?

2.Visualise the distribution of carat, partitioned by price.

3.How does the price distribution of very large diamonds compare to small diamonds. Is it as you expect, or does it surprise you?

4.Combine two of the techniques you’ve learned to visualise the combined distribution of cut, carat, and price.

5.Two dimensional plots reveal outliers that are not visible in one dimensional plots. For example, some points in the plot below have an unusual combination of x and y values, which makes the points outliers even though their x and y values appear normal when examined separately.


```r
ggplot(data = diamonds) +
  geom_point(mapping = aes(x = x, y = y)) +
  coord_cartesian(xlim = c(4, 11), ylim = c(4, 11))
```

![](Exploratory_Data_Analysis_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

Why is a scatterplot a better display than a binned plot for this case?
