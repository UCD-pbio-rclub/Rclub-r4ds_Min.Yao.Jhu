# R-club-June-7
Min-Yao  
2017年6月6日  

# 11 Data import

## 11.1 Introduction

### 11.1.1 Prerequisites


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


## 11.2 Getting started


```r
read_csv("a,b,c
1,2,3
4,5,6")
```

```
## # A tibble: 2 × 3
##       a     b     c
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```

```r
#1
read_csv("The first line of metadata
  The second line of metadata
  x,y,z
  1,2,3", skip = 2)
```

```
## # A tibble: 1 × 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
```

```r
read_csv("# A comment I want to skip
  x,y,z
  1,2,3", comment = "#")
```

```
## # A tibble: 1 × 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
```

```r
#2
read_csv("1,2,3\n4,5,6", col_names = FALSE)
```

```
## # A tibble: 2 × 3
##      X1    X2    X3
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```

```r
read_csv("1,2,3\n4,5,6", col_names = c("x", "y", "z"))
```

```
## # A tibble: 2 × 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```


```r
read_csv("a,b,c\n1,2,.", na = ".")
```

```
## # A tibble: 1 × 3
##       a     b     c
##   <int> <int> <chr>
## 1     1     2  <NA>
```


### 11.2.1 Compared to base R

### 11.2.2 Exercises

1.What function would you use to read a file where fields were separated with
“|”?

```r
#?read_delim()

read_delim ("1|2|3\n4|5|6", delim = "|", col_names = c("x", "y", "z"))
```

```
## # A tibble: 2 × 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```

2.Apart from file, skip, and comment, what other arguments do read_csv() and read_tsv() have in common?


```r
?read_csv()
```

```
## starting httpd help server ...
```

```
##  done
```

```r
?read_tsv()
```

> read_csv2(file, col_names = TRUE, col_types = NULL,
  locale = default_locale(), na = c("", "NA"), quoted_na = TRUE,
  comment = "", trim_ws = TRUE, skip = 0, n_max = Inf,
  guess_max = min(1000, n_max), progress = interactive())

> read_tsv(file, col_names = TRUE, col_types = NULL,
  locale = default_locale(), na = c("", "NA"), quoted_na = TRUE,
  comment = "", trim_ws = TRUE, skip = 0, n_max = Inf,
  guess_max = min(1000, n_max), progress = interactive())

3.What are the most important arguments to read_fwf()?


```r
?read_fwf
```

> read_fwf(file, col_positions, col_types = NULL, locale = default_locale(),
  na = c("", "NA"), comment = "", skip = 0, n_max = Inf,
  guess_max = min(n_max, 1000), progress = interactive())

> fwf_empty(file, skip = 0, col_names = NULL, comment = "")

> fwf_widths(widths, col_names = NULL)

> fwf_positions(start, end, col_names = NULL)


4.Sometimes strings in a CSV file contain commas. To prevent them from causing problems they need to be surrounded by a quoting character, like " or '. By convention, read_csv() assumes that the quoting character will be ", and if you want to change it you’ll need to use read_delim() instead. What arguments do you need to specify to read the following text into a data frame?


```r
read_delim ("x,y\n1,'a,b'",quote = "'", delim = ",")
```

```
## # A tibble: 1 × 2
##       x     y
##   <int> <chr>
## 1     1   a,b
```

```r
read_delim ("1,2,3\n'4,a','5,2','6,!'", quote = "'", delim = ",", col_names = c("x", "y", "z"))
```

```
## # A tibble: 2 × 3
##       x     y     z
##   <chr> <dbl> <chr>
## 1     1     2     3
## 2   4,a    52   6,!
```


5.Identify what is wrong with each of the following inline CSV files. What happens when you run the code?


```r
read_csv("a,b\n1,2,3\n4,5,6")
```

```
## Warning: 2 parsing failures.
## row col  expected    actual
##   1  -- 2 columns 3 columns
##   2  -- 2 columns 3 columns
```

```
## # A tibble: 2 × 2
##       a     b
##   <int> <int>
## 1     1     2
## 2     4     5
```

> There are 2 columns in the first row, but 3 columns in the second and third rows.


```r
read_csv("a,b,c\n1,2\n1,2,3,4")
```

```
## Warning: 2 parsing failures.
## row col  expected    actual
##   1  -- 3 columns 2 columns
##   2  -- 3 columns 4 columns
```

```
## # A tibble: 2 × 3
##       a     b     c
##   <int> <int> <int>
## 1     1     2    NA
## 2     1     2     3
```

> There are 2 columns in the second row, but 3 columns in the first and 4 columns in the third rows.


```r
read_csv("a,b\n\"1")
```

```
## Warning: 2 parsing failures.
## row col                     expected    actual
##   1  a  closing quote at end of file          
##   1  -- 2 columns                    1 columns
```

```
## # A tibble: 1 × 2
##       a     b
##   <int> <chr>
## 1     1  <NA>
```

> `\` need to be quoted


```r
read_csv("a,b\n1,2\na,b")
```

```
## # A tibble: 2 × 2
##       a     b
##   <chr> <chr>
## 1     1     2
## 2     a     b
```

> `1` and `2` are characters.


```r
read_csv("a;b\n1;3")
```

```
## # A tibble: 1 × 1
##   `a;b`
##   <chr>
## 1   1;3
```

```r
read_csv2("a;b\n1;3")
```

```
## # A tibble: 1 × 2
##       a     b
##   <int> <int>
## 1     1     3
```



## 11.3 Parsing a vector

```r
str(parse_logical(c("TRUE", "FALSE", "NA")))
```

```
##  logi [1:3] TRUE FALSE NA
```

```r
str(parse_integer(c("1", "2", "3")))
```

```
##  int [1:3] 1 2 3
```

```r
str(parse_date(c("2010-01-01", "1979-10-14")))
```

```
##  Date[1:2], format: "2010-01-01" "1979-10-14"
```

```r
parse_integer(c("1", "231", ".", "456"), na = ".")
```

```
## [1]   1 231  NA 456
```

```r
x <- parse_integer(c("123", "345", "abc", "123.45"))
```

```
## Warning: 2 parsing failures.
## row col               expected actual
##   3  -- an integer                abc
##   4  -- no trailing characters    .45
```

```r
x
```

```
## [1] 123 345  NA  NA
## attr(,"problems")
## # A tibble: 2 × 4
##     row   col               expected actual
##   <int> <int>                  <chr>  <chr>
## 1     3    NA             an integer    abc
## 2     4    NA no trailing characters    .45
```

```r
problems(x)
```

```
## # A tibble: 2 × 4
##     row   col               expected actual
##   <int> <int>                  <chr>  <chr>
## 1     3    NA             an integer    abc
## 2     4    NA no trailing characters    .45
```

parse_logical() and parse_integer() parse logicals and integers respectively. There’s basically nothing that can go wrong with these parsers so I won’t describe them here further.

parse_double() is a strict numeric parser, and parse_number() is a flexible numeric parser. These are more complicated than you might expect because different parts of the world write numbers in different ways.

parse_character() seems so simple that it shouldn’t be necessary. But one complication makes it quite important: character encodings.

parse_factor() create factors, the data structure that R uses to represent categorical variables with fixed and known values.

parse_datetime(), parse_date(), and parse_time() allow you to parse various date & time specifications. These are the most complicated because there are so many different ways of writing dates.

### 11.3.1 Numbers

### 11.3.2 Strings

### 11.3.3 Factors

### 11.3.4 Dates, date-times, and times

### 11.3.5 Exercises

## 11.4 Parsing a file

### 11.4.1 Strategy

### 11.4.2 Problems

### 11.4.3 Other strategies

## 11.5 Writing to a file

## 11.6 Other types of data




