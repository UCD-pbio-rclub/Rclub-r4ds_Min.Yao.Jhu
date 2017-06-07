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


```r
parse_double("1.23")
```

```
## [1] 1.23
```

```r
parse_double("1,23", locale = locale(decimal_mark = ","))
```

```
## [1] 1.23
```

```r
parse_number("$100")
```

```
## [1] 100
```

```r
parse_number("20%")
```

```
## [1] 20
```

```r
parse_number("It cost $123.45")
```

```
## [1] 123.45
```

```r
# Used in America
parse_number("$123,456,789")
```

```
## [1] 123456789
```

```r
# Used in many parts of Europe
parse_number("123.456.789", locale = locale(grouping_mark = "."))
```

```
## [1] 123456789
```

```r
# Used in Switzerland
parse_number("123'456'789", locale = locale(grouping_mark = "'"))
```

```
## [1] 123456789
```


### 11.3.2 Strings


```r
charToRaw("Hadley")
```

```
## [1] 48 61 64 6c 65 79
```

```r
x1 <- "El Ni\xf1o was particularly bad this year"
x2 <- "\x82\xb1\x82\xf1\x82\xc9\x82\xbf\x82\xcd"
x1
```

```
## [1] "El Ni隳 was particularly bad this year"
```

```r
x2
```

```
## [1] ""
```

```r
parse_character(x1, locale = locale(encoding = "Latin1"))
```

```
## [1] "El Nino was particularly bad this year"
```

```r
parse_character(x2, locale = locale(encoding = "Shift-JIS"))
```

```
## [1] "<U+3053><U+3093><U+306B><U+3061><U+306F>"
```

```r
guess_encoding(charToRaw(x1))
```

```
##     encoding confidence
## 1 ISO-8859-1       0.46
## 2 ISO-8859-9       0.23
```

```r
guess_encoding(charToRaw(x2))
```

```
##   encoding confidence
## 1   KOI8-R       0.42
```


### 11.3.3 Factors


```r
fruit <- c("apple", "banana")
parse_factor(c("apple", "banana", "bananana"), levels = fruit)
```

```
## Warning: 1 parsing failure.
## row col           expected   actual
##   3  -- value in level set bananana
```

```
## [1] apple  banana <NA>  
## attr(,"problems")
## # A tibble: 1 × 4
##     row   col           expected   actual
##   <int> <int>              <chr>    <chr>
## 1     3    NA value in level set bananana
## Levels: apple banana
```


### 11.3.4 Dates, date-times, and times


```r
parse_datetime("2010-10-01T2010")
```

```
## [1] "2010-10-01 20:10:00 UTC"
```

```r
parse_datetime("20101010")
```

```
## [1] "2010-10-10 UTC"
```

```r
parse_date("2010-10-01")
```

```
## [1] "2010-10-01"
```

```r
library(hms)
parse_time("01:10 am")
```

```
## 01:10:00
```

```r
parse_time("20:10:01")
```

```
## 20:10:01
```

```r
parse_date("01/02/15", "%m/%d/%y")
```

```
## [1] "2015-01-02"
```

```r
parse_date("01/02/15", "%d/%m/%y")
```

```
## [1] "2015-02-01"
```

```r
parse_date("01/02/15", "%y/%m/%d")
```

```
## [1] "2001-02-15"
```

```r
parse_date("1 janvier 2015", "%d %B %Y", locale = locale("fr"))
```

```
## [1] "2015-01-01"
```


### 11.3.5 Exercises

1. What are the most important arguments to locale()?


```r
#?locale()
```

> A locale object tries to capture all the defaults that can vary between countries. You set the locale in once, and the details are automatically passed on down to the columns parsers. The defaults have been chosen to match R (i.e. US English) as closely as possible.

> locale(date_names = "en", date_format = "%AD", time_format = "%AT",
  decimal_mark = ".", grouping_mark = ",", tz = "UTC",
  encoding = "UTF-8", asciify = FALSE)
  
> date_names	
Character representations of day and month names. Either the language code as string (passed on to date_names_lang) or an object created by date_names.


2. What happens if you try and set decimal_mark and grouping_mark to the same character? What happens to the default value of grouping_mark when you set decimal_mark to “,”? What happens to the default value of decimal_mark when you set the grouping_mark to “.”?


```r
# parse_double("1,000,001", locale = locale(decimal_mark = "," , grouping_mark = ","))
# Error: `decimal_mark` and `grouping_mark` must be different

parse_double("1000,001", locale = locale(decimal_mark = ","))
```

```
## [1] 1000.001
```

```r
parse_number("1.000.001", locale = locale(grouping_mark = "."))
```

```
## [1] 1000001
```

```r
parse_number("1.000,001", locale = locale(grouping_mark = "."))
```

```
## [1] 1000.001
```
> 1. Error: `decimal_mark` and `grouping_mark` must be different

> 3. when I set the grouping_mark to `.`, the default value of decimal_mark become `,`

3. I didn’t discuss the date_format and time_format options to locale(). What do they do? Construct an example that shows when they might be useful.


```r
#?locale()

parse_date("2015-01-02")
```

```
## [1] "2015-01-02"
```

```r
parse_date("01-02-15", locale=locale(date_format = "%m-%d-%y"))
```

```
## [1] "2015-01-02"
```

```r
parse_date("01-02-15", locale=locale(date_format = "%y-%m-%d"))
```

```
## [1] "2001-02-15"
```

```r
library(hms)
parse_time("20:10:01")
```

```
## 20:10:01
```

```r
parse_time("20:10:01", locale=locale(time_format = "%S:%M:%H"))
```

```
## 01:10:20
```

> Usage
locale(date_names = "en", date_format = "%AD", time_format = "%AT",
  decimal_mark = ".", grouping_mark = ",", tz = "UTC",
  encoding = "UTF-8", asciify = FALSE)

4. If you live outside the US, create a new locale object that encapsulates the settings for the types of file you read most commonly.

> If I lived in Taiwan, 
locale = locale(date_names = "zh", date_format = "%y-%m-%d", tz = "Asia/Taipei", encoding = "zh_TW.UTF-8")


```r
date_names_lang("zh")
```

```
## <date_names>
## Days:   星期日 (周日), 星期一 (周一), 星期二 (周二), 星期三 (周三), 星期四
##         (周四), 星期五 (周五), 星期六 (周六)
## Months: 一月 (1月), 二月 (2月), 三月 (3月), 四月 (4月), 五月 (5月), 六月
##         (6月), 七月 (7月), 八月 (8月), 九月 (9月), 十月 (10月),
##         十一月 (11月), 十二月 (12月)
## AM/PM:  上午/下午
```


5. What’s the difference between read_csv() and read_csv2()?

> read_csv() reads comma delimited files, read_csv2() reads semicolon separated files (common in countries where `,` is used as the decimal place)

6. What are the most common encodings used in Europe? What are the most common encodings used in Asia? Do some googling to find out.

> ISO 8859:
ISO 8859-1 Western Europe
ISO 8859-2 Western and Central Europe
ISO 8859-3 Western Europe and South European (Turkish, Maltese plus Esperanto)
ISO 8859-4 Western Europe and Baltic countries (Lithuania, Estonia, Latvia and Lapp)

> Taiwan Big5 (a more famous variant is Microsoft Code page 950)
> Chinese Guobiao
GB 2312
GBK (Microsoft Code page 936)
GB 18030
> JIS X 0208 is a widely deployed standard for Japanese character encoding that has several encoding forms.
> Korean
KS X 1001 is a Korean double-byte character encoding standard

7. Generate the correct format string to parse each of the following dates and times:


```r
d1 <- "January 1, 2010"
parse_date(d1, "%B %d, %Y", locale = locale("en"))
```

```
## [1] "2010-01-01"
```

```r
d2 <- "2015-Mar-07"
parse_date(d2, "%Y-%b-%d", locale = locale("en"))
```

```
## [1] "2015-03-07"
```

```r
d3 <- "06-Jun-2017"
parse_date(d3, "%d-%b-%Y", locale = locale("en"))
```

```
## [1] "2017-06-06"
```

```r
d4 <- c("August 19 (2015)", "July 1 (2015)")
parse_date(d4, "%B %d (%Y)", locale = locale("en"))
```

```
## [1] "2015-08-19" "2015-07-01"
```

```r
d5 <- "12/30/14" # Dec 30, 2014
parse_date(d5, "%m/%d/%y", locale = locale("en"))
```

```
## [1] "2014-12-30"
```

```r
t1 <- "1705"
parse_time(t1, "%H%M")
```

```
## 17:05:00
```

```r
t2 <- "11:15:10.12 PM"
parse_time(t2, "%I:%M:%OS %p")
```

```
## 23:15:10.12
```


## 11.4 Parsing a file

### 11.4.1 Strategy

### 11.4.2 Problems

### 11.4.3 Other strategies

## 11.5 Writing to a file

## 11.6 Other types of data




