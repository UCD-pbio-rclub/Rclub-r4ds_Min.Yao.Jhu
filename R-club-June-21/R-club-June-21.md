# R-club-June-21
Min-Yao  
2017年6月20日  


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
## Warning: package 'tibble' was built under R version 3.3.3
```

```
## Warning: package 'tidyr' was built under R version 3.3.3
```

```
## Warning: package 'readr' was built under R version 3.3.3
```

```
## Warning: package 'purrr' was built under R version 3.3.3
```

```
## Warning: package 'dplyr' was built under R version 3.3.3
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```


## 12.5 Missing values


```r
stocks <- tibble(
  year   = c(2015, 2015, 2015, 2015, 2016, 2016, 2016),
  qtr    = c(   1,    2,    3,    4,    2,    3,    4),
  return = c(1.88, 0.59, 0.35,   NA, 0.92, 0.17, 2.66)
)
stocks
```

```
## # A tibble: 7 x 3
##    year   qtr return
##   <dbl> <dbl>  <dbl>
## 1  2015     1   1.88
## 2  2015     2   0.59
## 3  2015     3   0.35
## 4  2015     4     NA
## 5  2016     2   0.92
## 6  2016     3   0.17
## 7  2016     4   2.66
```

```r
# make the implicit missing value explicit
stocks %>% 
  spread(year, return)
```

```
## # A tibble: 4 x 3
##     qtr `2015` `2016`
## * <dbl>  <dbl>  <dbl>
## 1     1   1.88     NA
## 2     2   0.59   0.92
## 3     3   0.35   0.17
## 4     4     NA   2.66
```

```r
# turn explicit missing values implicit
stocks %>% 
  spread(year, return) %>% 
  gather(year, return, `2015`:`2016`, na.rm = TRUE)
```

```
## # A tibble: 6 x 3
##     qtr  year return
## * <dbl> <chr>  <dbl>
## 1     1  2015   1.88
## 2     2  2015   0.59
## 3     3  2015   0.35
## 4     2  2016   0.92
## 5     3  2016   0.17
## 6     4  2016   2.66
```

```r
stocks %>% 
  complete(year, qtr)
```

```
## # A tibble: 8 x 3
##    year   qtr return
##   <dbl> <dbl>  <dbl>
## 1  2015     1   1.88
## 2  2015     2   0.59
## 3  2015     3   0.35
## 4  2015     4     NA
## 5  2016     1     NA
## 6  2016     2   0.92
## 7  2016     3   0.17
## 8  2016     4   2.66
```

```r
treatment <- tribble(
  ~ person,           ~ treatment, ~response,
  "Derrick Whitmore", 1,           7,
  NA,                 2,           10,
  NA,                 3,           9,
  "Katherine Burke",  1,           4
)
treatment
```

```
## # A tibble: 4 x 3
##             person treatment response
##              <chr>     <dbl>    <dbl>
## 1 Derrick Whitmore         1        7
## 2             <NA>         2       10
## 3             <NA>         3        9
## 4  Katherine Burke         1        4
```

```r
treatment %>% 
  fill(person)
```

```
## # A tibble: 4 x 3
##             person treatment response
##              <chr>     <dbl>    <dbl>
## 1 Derrick Whitmore         1        7
## 2 Derrick Whitmore         2       10
## 3 Derrick Whitmore         3        9
## 4  Katherine Burke         1        4
```


### 12.5.1 Exercises

1. Compare and contrast the fill arguments to spread() and complete().


```r
#?fill
#?spread
#?complete


# Spread and gather are complements
df <- data.frame(x = c("a", "b"), y = c(3, 4), z = c(5, 6))
df
```

```
##   x y z
## 1 a 3 5
## 2 b 4 6
```

```r
df %>% spread(x, y)
```

```
##   z  a  b
## 1 5  3 NA
## 2 6 NA  4
```

```r
df %>% spread(x, y) %>% gather(x, y, a:b, na.rm = TRUE)
```

```
##   z x y
## 1 5 a 3
## 4 6 b 4
```

> fill {tidyr}
Fills missing values in using the previous entry. This is useful in the common output format where values are not repeated, they're recorded each time they change.

> spread {tidyr}
Spread a key-value pair across multiple columns.

> complete {tidyr}
Turns implicit missing values into explicit missing values. This is a wrapper around expand(), left_join() and replace_na that's useful for completing missing combinations of data.

2. What does the direction argument to fill() do?


```r
#?fill
df <- data.frame(Month = 1:12, Year = c(2000, rep(NA, 10), 10))
df
```

```
##    Month Year
## 1      1 2000
## 2      2   NA
## 3      3   NA
## 4      4   NA
## 5      5   NA
## 6      6   NA
## 7      7   NA
## 8      8   NA
## 9      9   NA
## 10    10   NA
## 11    11   NA
## 12    12   10
```

```r
df %>% fill(Year)
```

```
##    Month Year
## 1      1 2000
## 2      2 2000
## 3      3 2000
## 4      4 2000
## 5      5 2000
## 6      6 2000
## 7      7 2000
## 8      8 2000
## 9      9 2000
## 10    10 2000
## 11    11 2000
## 12    12   10
```

```r
df %>% fill(Year, .direction = c("up"))
```

```
##    Month Year
## 1      1 2000
## 2      2   10
## 3      3   10
## 4      4   10
## 5      5   10
## 6      6   10
## 7      7   10
## 8      8   10
## 9      9   10
## 10    10   10
## 11    11   10
## 12    12   10
```

> fill {tidyr}
.direction	
Direction in which to fill missing values. Currently either "down" (the default) or "up".

## 12.6 Case Study


```r
who
```

```
## # A tibble: 7,240 x 60
##        country  iso2  iso3  year new_sp_m014 new_sp_m1524 new_sp_m2534
##          <chr> <chr> <chr> <int>       <int>        <int>        <int>
##  1 Afghanistan    AF   AFG  1980          NA           NA           NA
##  2 Afghanistan    AF   AFG  1981          NA           NA           NA
##  3 Afghanistan    AF   AFG  1982          NA           NA           NA
##  4 Afghanistan    AF   AFG  1983          NA           NA           NA
##  5 Afghanistan    AF   AFG  1984          NA           NA           NA
##  6 Afghanistan    AF   AFG  1985          NA           NA           NA
##  7 Afghanistan    AF   AFG  1986          NA           NA           NA
##  8 Afghanistan    AF   AFG  1987          NA           NA           NA
##  9 Afghanistan    AF   AFG  1988          NA           NA           NA
## 10 Afghanistan    AF   AFG  1989          NA           NA           NA
## # ... with 7,230 more rows, and 53 more variables: new_sp_m3544 <int>,
## #   new_sp_m4554 <int>, new_sp_m5564 <int>, new_sp_m65 <int>,
## #   new_sp_f014 <int>, new_sp_f1524 <int>, new_sp_f2534 <int>,
## #   new_sp_f3544 <int>, new_sp_f4554 <int>, new_sp_f5564 <int>,
## #   new_sp_f65 <int>, new_sn_m014 <int>, new_sn_m1524 <int>,
## #   new_sn_m2534 <int>, new_sn_m3544 <int>, new_sn_m4554 <int>,
## #   new_sn_m5564 <int>, new_sn_m65 <int>, new_sn_f014 <int>,
## #   new_sn_f1524 <int>, new_sn_f2534 <int>, new_sn_f3544 <int>,
## #   new_sn_f4554 <int>, new_sn_f5564 <int>, new_sn_f65 <int>,
## #   new_ep_m014 <int>, new_ep_m1524 <int>, new_ep_m2534 <int>,
## #   new_ep_m3544 <int>, new_ep_m4554 <int>, new_ep_m5564 <int>,
## #   new_ep_m65 <int>, new_ep_f014 <int>, new_ep_f1524 <int>,
## #   new_ep_f2534 <int>, new_ep_f3544 <int>, new_ep_f4554 <int>,
## #   new_ep_f5564 <int>, new_ep_f65 <int>, newrel_m014 <int>,
## #   newrel_m1524 <int>, newrel_m2534 <int>, newrel_m3544 <int>,
## #   newrel_m4554 <int>, newrel_m5564 <int>, newrel_m65 <int>,
## #   newrel_f014 <int>, newrel_f1524 <int>, newrel_f2534 <int>,
## #   newrel_f3544 <int>, newrel_f4554 <int>, newrel_f5564 <int>,
## #   newrel_f65 <int>
```

```r
who1 <- who %>% 
  gather(new_sp_m014:newrel_f65, key = "key", value = "cases", na.rm = TRUE)
who1
```

```
## # A tibble: 76,046 x 6
##        country  iso2  iso3  year         key cases
##  *       <chr> <chr> <chr> <int>       <chr> <int>
##  1 Afghanistan    AF   AFG  1997 new_sp_m014     0
##  2 Afghanistan    AF   AFG  1998 new_sp_m014    30
##  3 Afghanistan    AF   AFG  1999 new_sp_m014     8
##  4 Afghanistan    AF   AFG  2000 new_sp_m014    52
##  5 Afghanistan    AF   AFG  2001 new_sp_m014   129
##  6 Afghanistan    AF   AFG  2002 new_sp_m014    90
##  7 Afghanistan    AF   AFG  2003 new_sp_m014   127
##  8 Afghanistan    AF   AFG  2004 new_sp_m014   139
##  9 Afghanistan    AF   AFG  2005 new_sp_m014   151
## 10 Afghanistan    AF   AFG  2006 new_sp_m014   193
## # ... with 76,036 more rows
```

```r
who1 %>% 
  count(key)
```

```
## # A tibble: 56 x 2
##             key     n
##           <chr> <int>
##  1  new_ep_f014  1032
##  2 new_ep_f1524  1021
##  3 new_ep_f2534  1021
##  4 new_ep_f3544  1021
##  5 new_ep_f4554  1017
##  6 new_ep_f5564  1017
##  7   new_ep_f65  1014
##  8  new_ep_m014  1038
##  9 new_ep_m1524  1026
## 10 new_ep_m2534  1020
## # ... with 46 more rows
```

```r
who2 <- who1 %>% 
  mutate(key = stringr::str_replace(key, "newrel", "new_rel"))
```

```
## Warning: package 'bindrcpp' was built under R version 3.3.3
```

```r
who2
```

```
## # A tibble: 76,046 x 6
##        country  iso2  iso3  year         key cases
##          <chr> <chr> <chr> <int>       <chr> <int>
##  1 Afghanistan    AF   AFG  1997 new_sp_m014     0
##  2 Afghanistan    AF   AFG  1998 new_sp_m014    30
##  3 Afghanistan    AF   AFG  1999 new_sp_m014     8
##  4 Afghanistan    AF   AFG  2000 new_sp_m014    52
##  5 Afghanistan    AF   AFG  2001 new_sp_m014   129
##  6 Afghanistan    AF   AFG  2002 new_sp_m014    90
##  7 Afghanistan    AF   AFG  2003 new_sp_m014   127
##  8 Afghanistan    AF   AFG  2004 new_sp_m014   139
##  9 Afghanistan    AF   AFG  2005 new_sp_m014   151
## 10 Afghanistan    AF   AFG  2006 new_sp_m014   193
## # ... with 76,036 more rows
```

```r
who3 <- who2 %>% 
  separate(key, c("new", "type", "sexage"), sep = "_")
who3
```

```
## # A tibble: 76,046 x 8
##        country  iso2  iso3  year   new  type sexage cases
##  *       <chr> <chr> <chr> <int> <chr> <chr>  <chr> <int>
##  1 Afghanistan    AF   AFG  1997   new    sp   m014     0
##  2 Afghanistan    AF   AFG  1998   new    sp   m014    30
##  3 Afghanistan    AF   AFG  1999   new    sp   m014     8
##  4 Afghanistan    AF   AFG  2000   new    sp   m014    52
##  5 Afghanistan    AF   AFG  2001   new    sp   m014   129
##  6 Afghanistan    AF   AFG  2002   new    sp   m014    90
##  7 Afghanistan    AF   AFG  2003   new    sp   m014   127
##  8 Afghanistan    AF   AFG  2004   new    sp   m014   139
##  9 Afghanistan    AF   AFG  2005   new    sp   m014   151
## 10 Afghanistan    AF   AFG  2006   new    sp   m014   193
## # ... with 76,036 more rows
```

```r
who3 %>% 
  count(new)
```

```
## # A tibble: 1 x 2
##     new     n
##   <chr> <int>
## 1   new 76046
```

```r
who4 <- who3 %>% 
  select(-new, -iso2, -iso3)

who5 <- who4 %>% 
  separate(sexage, c("sex", "age"), sep = 1)
who5
```

```
## # A tibble: 76,046 x 6
##        country  year  type   sex   age cases
##  *       <chr> <int> <chr> <chr> <chr> <int>
##  1 Afghanistan  1997    sp     m   014     0
##  2 Afghanistan  1998    sp     m   014    30
##  3 Afghanistan  1999    sp     m   014     8
##  4 Afghanistan  2000    sp     m   014    52
##  5 Afghanistan  2001    sp     m   014   129
##  6 Afghanistan  2002    sp     m   014    90
##  7 Afghanistan  2003    sp     m   014   127
##  8 Afghanistan  2004    sp     m   014   139
##  9 Afghanistan  2005    sp     m   014   151
## 10 Afghanistan  2006    sp     m   014   193
## # ... with 76,036 more rows
```

```r
who.final <- who %>%
  gather(code, value, new_sp_m014:newrel_f65, na.rm = TRUE) %>% 
  mutate(code = stringr::str_replace(code, "newrel", "new_rel")) %>%
  separate(code, c("new", "var", "sexage")) %>% 
  select(-new, -iso2, -iso3) %>% 
  separate(sexage, c("sex", "age"), sep = 1)
who.final
```

```
## # A tibble: 76,046 x 6
##        country  year   var   sex   age value
##  *       <chr> <int> <chr> <chr> <chr> <int>
##  1 Afghanistan  1997    sp     m   014     0
##  2 Afghanistan  1998    sp     m   014    30
##  3 Afghanistan  1999    sp     m   014     8
##  4 Afghanistan  2000    sp     m   014    52
##  5 Afghanistan  2001    sp     m   014   129
##  6 Afghanistan  2002    sp     m   014    90
##  7 Afghanistan  2003    sp     m   014   127
##  8 Afghanistan  2004    sp     m   014   139
##  9 Afghanistan  2005    sp     m   014   151
## 10 Afghanistan  2006    sp     m   014   193
## # ... with 76,036 more rows
```


### 12.6.1 Exercises

1. In this case study I set na.rm = TRUE just to make it easier to check that we had the correct values. Is this reasonable? Think about how missing values are represented in this dataset. Are there implicit missing values? What’s the difference between an NA and zero?


```r
who.na <- who %>%
  gather(code, value, new_sp_m014:newrel_f65) %>% 
  mutate(code = stringr::str_replace(code, "newrel", "new_rel")) %>%
  separate(code, c("new", "var", "sexage")) %>% 
  select(-new, -iso2, -iso3) %>% 
  separate(sexage, c("sex", "age"), sep = 1)
who.na
```

```
## # A tibble: 405,440 x 6
##        country  year   var   sex   age value
##  *       <chr> <int> <chr> <chr> <chr> <int>
##  1 Afghanistan  1980    sp     m   014    NA
##  2 Afghanistan  1981    sp     m   014    NA
##  3 Afghanistan  1982    sp     m   014    NA
##  4 Afghanistan  1983    sp     m   014    NA
##  5 Afghanistan  1984    sp     m   014    NA
##  6 Afghanistan  1985    sp     m   014    NA
##  7 Afghanistan  1986    sp     m   014    NA
##  8 Afghanistan  1987    sp     m   014    NA
##  9 Afghanistan  1988    sp     m   014    NA
## 10 Afghanistan  1989    sp     m   014    NA
## # ... with 405,430 more rows
```

```r
summary(who.final)
```

```
##    country               year          var                sex           
##  Length:76046       Min.   :1980   Length:76046       Length:76046      
##  Class :character   1st Qu.:2003   Class :character   Class :character  
##  Mode  :character   Median :2007   Mode  :character   Mode  :character  
##                     Mean   :2006                                        
##                     3rd Qu.:2010                                        
##                     Max.   :2013                                        
##      age                value         
##  Length:76046       Min.   :     0.0  
##  Class :character   1st Qu.:     3.0  
##  Mode  :character   Median :    26.0  
##                     Mean   :   570.7  
##                     3rd Qu.:   184.0  
##                     Max.   :250051.0
```

```r
summary(who.na)
```

```
##    country               year          var                sex           
##  Length:405440      Min.   :1980   Length:405440      Length:405440     
##  Class :character   1st Qu.:1988   Class :character   Class :character  
##  Mode  :character   Median :1997   Mode  :character   Mode  :character  
##                     Mean   :1997                                        
##                     3rd Qu.:2005                                        
##                     Max.   :2013                                        
##                                                                         
##      age                value         
##  Length:405440      Min.   :     0.0  
##  Class :character   1st Qu.:     3.0  
##  Mode  :character   Median :    26.0  
##                     Mean   :   570.7  
##                     3rd Qu.:   184.0  
##                     Max.   :250051.0  
##                     NA's   :329394
```

```r
who.complete.na <- who.na %>% complete(country,year,var,sex,age)
summary(who.complete.na)
```

```
##    country               year          var                sex           
##  Length:416976      Min.   :1980   Length:416976      Length:416976     
##  Class :character   1st Qu.:1988   Class :character   Class :character  
##  Mode  :character   Median :1996   Mode  :character   Mode  :character  
##                     Mean   :1996                                        
##                     3rd Qu.:2005                                        
##                     Max.   :2013                                        
##                                                                         
##      age                value         
##  Length:416976      Min.   :     0.0  
##  Class :character   1st Qu.:     3.0  
##  Mode  :character   Median :    26.0  
##                     Mean   :   570.7  
##                     3rd Qu.:   184.0  
##                     Max.   :250051.0  
##                     NA's   :340930
```


2. What happens if you neglect the mutate() step? (mutate(key = stringr::str_replace(key, "newrel", "new_rel")))


```r
who.nomutate <- who %>%
  gather(code, value, new_sp_m014:newrel_f65, na.rm = TRUE) %>% 
  separate(code, c("new", "var", "sexage")) %>% 
  select(-new, -iso2, -iso3) %>% 
  separate(sexage, c("sex", "age"), sep = 1)
```

```
## Warning: Too few values at 2580 locations: 73467, 73468, 73469, 73470,
## 73471, 73472, 73473, 73474, 73475, 73476, 73477, 73478, 73479, 73480,
## 73481, 73482, 73483, 73484, 73485, 73486, ...
```

```r
summary(who.nomutate)
```

```
##    country               year          var                sex           
##  Length:76046       Min.   :1980   Length:76046       Length:76046      
##  Class :character   1st Qu.:2003   Class :character   Class :character  
##  Mode  :character   Median :2007   Mode  :character   Mode  :character  
##                     Mean   :2006                                        
##                     3rd Qu.:2010                                        
##                     Max.   :2013                                        
##      age                value         
##  Length:76046       Min.   :     0.0  
##  Class :character   1st Qu.:     3.0  
##  Mode  :character   Median :    26.0  
##                     Mean   :   570.7  
##                     3rd Qu.:   184.0  
##                     Max.   :250051.0
```

```r
who.nomutate[73460:73470,]
```

```
## # A tibble: 11 x 6
##        country  year   var   sex   age value
##          <chr> <int> <chr> <chr> <chr> <int>
##  1    Zimbabwe  2006    ep     f    65    92
##  2    Zimbabwe  2007    ep     f    65     9
##  3    Zimbabwe  2008    ep     f    65   104
##  4    Zimbabwe  2009    ep     f    65   138
##  5    Zimbabwe  2010    ep     f    65   146
##  6    Zimbabwe  2011    ep     f    65   129
##  7    Zimbabwe  2012    ep     f    65   143
##  8 Afghanistan  2013  m014  <NA>  <NA>  1705
##  9     Albania  2013  m014  <NA>  <NA>    14
## 10     Algeria  2013  m014  <NA>  <NA>    25
## 11     Andorra  2013  m014  <NA>  <NA>     0
```


3. I claimed that iso2 and iso3 were redundant with country. Confirm this claim.


```r
who %>% count(country)
```

```
## # A tibble: 219 x 2
##                country     n
##                  <chr> <int>
##  1         Afghanistan    34
##  2             Albania    34
##  3             Algeria    34
##  4      American Samoa    34
##  5             Andorra    34
##  6              Angola    34
##  7            Anguilla    34
##  8 Antigua and Barbuda    34
##  9           Argentina    34
## 10             Armenia    34
## # ... with 209 more rows
```

```r
who %>% count(iso2)
```

```
## # A tibble: 219 x 2
##     iso2     n
##    <chr> <int>
##  1    AD    34
##  2    AE    34
##  3    AF    34
##  4    AG    34
##  5    AI    34
##  6    AL    34
##  7    AM    34
##  8    AN    30
##  9    AO    34
## 10    AR    34
## # ... with 209 more rows
```

```r
who %>% count(iso3)
```

```
## # A tibble: 219 x 2
##     iso3     n
##    <chr> <int>
##  1   ABW    34
##  2   AFG    34
##  3   AGO    34
##  4   AIA    34
##  5   ALB    34
##  6   AND    34
##  7   ANT    30
##  8   ARE    34
##  9   ARG    34
## 10   ARM    34
## # ... with 209 more rows
```

```r
who %>% count(country,iso2,iso3)
```

```
## # A tibble: 219 x 4
##                country  iso2  iso3     n
##                  <chr> <chr> <chr> <int>
##  1         Afghanistan    AF   AFG    34
##  2             Albania    AL   ALB    34
##  3             Algeria    DZ   DZA    34
##  4      American Samoa    AS   ASM    34
##  5             Andorra    AD   AND    34
##  6              Angola    AO   AGO    34
##  7            Anguilla    AI   AIA    34
##  8 Antigua and Barbuda    AG   ATG    34
##  9           Argentina    AR   ARG    34
## 10             Armenia    AM   ARM    34
## # ... with 209 more rows
```


4. For each country, year, and sex compute the total number of cases of TB. Make an informative visualisation of the data.


```r
who.final <- who %>%
  gather(code, value, new_sp_m014:newrel_f65, na.rm = TRUE) %>% 
  mutate(code = stringr::str_replace(code, "newrel", "new_rel")) %>%
  separate(code, c("new", "var", "sexage")) %>% 
  select(-new, -iso2, -iso3) %>% 
  separate(sexage, c("sex", "age"), sep = 1)
who.final
```

```
## # A tibble: 76,046 x 6
##        country  year   var   sex   age value
##  *       <chr> <int> <chr> <chr> <chr> <int>
##  1 Afghanistan  1997    sp     m   014     0
##  2 Afghanistan  1998    sp     m   014    30
##  3 Afghanistan  1999    sp     m   014     8
##  4 Afghanistan  2000    sp     m   014    52
##  5 Afghanistan  2001    sp     m   014   129
##  6 Afghanistan  2002    sp     m   014    90
##  7 Afghanistan  2003    sp     m   014   127
##  8 Afghanistan  2004    sp     m   014   139
##  9 Afghanistan  2005    sp     m   014   151
## 10 Afghanistan  2006    sp     m   014   193
## # ... with 76,036 more rows
```


## 12.7 Non-tidy data

