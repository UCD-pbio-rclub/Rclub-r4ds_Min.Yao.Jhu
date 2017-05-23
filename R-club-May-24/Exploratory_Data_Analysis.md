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

## 7.4 Missing values

### 7.4.1 Exercises

## 7.5 Covariation

### 7.5.1 A categorical and continuous variable

#### 7.5.1.1 Exercises

### 7.5.2 Two categorical variables

#### 7.5.2.1 Exercises

### 7.5.3 Two continuous variables

#### 7.5.3.1 Exercises


