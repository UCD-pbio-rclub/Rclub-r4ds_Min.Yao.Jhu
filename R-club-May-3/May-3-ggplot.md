# May-3-ggplot
Min-Yao  
2017年5月1日  

## 3.6 Geometric objects


```r
library(ggplot2)
library(tibble)
```



```r
# left
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
# right
ggplot(data = mpg) + 
  geom_smooth(mapping = aes(x = displ, y = hwy))
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-2-2.png)<!-- -->

```r
ggplot(data = mpg) + 
  geom_smooth(mapping = aes(x = displ, y = hwy, linetype = drv))
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-2-3.png)<!-- -->

```r
ggplot(data = mpg) + 
  geom_smooth(mapping = aes(x = displ, y = hwy, linetype = drv, color = drv)) +
  geom_point(mapping = aes(x = displ, y = hwy, color = drv))
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-2-4.png)<!-- -->


```r
ggplot(data = mpg) +
  geom_smooth(mapping = aes(x = displ, y = hwy))
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

```r
ggplot(data = mpg) +
  geom_smooth(mapping = aes(x = displ, y = hwy, group = drv))
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-3-2.png)<!-- -->

```r
ggplot(data = mpg) +
  geom_smooth(
    mapping = aes(x = displ, y = hwy, group = drv)
  )
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-3-3.png)<!-- -->

```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  geom_smooth(mapping = aes(x = displ, y = hwy))
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-3-4.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point() + 
  geom_smooth()
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-3-5.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point(mapping = aes(color = class)) + 
  geom_smooth()
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-3-6.png)<!-- -->

```r
#ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
#  geom_point(mapping = aes(color = class)) + 
#  geom_smooth(data = filter (mpg, class == "subcompact"), se = FALSE)
```

### 3.6.1 Exercises


```r
#2
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point() + 
  geom_smooth(se = FALSE)
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```r
#5
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point() + 
  geom_smooth()
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-4-2.png)<!-- -->

```r
ggplot() + 
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy))
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-4-3.png)<!-- -->

```r
#6
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  geom_smooth(mapping = aes(x = displ, y = hwy), se = FALSE)
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-4-4.png)<!-- -->

```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  geom_smooth(mapping = aes(x = displ, y = hwy, group = drv), se = FALSE)
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-4-5.png)<!-- -->

```r
ggplot(data = mpg) + 
  geom_smooth(mapping = aes(x = displ, y = hwy, color = drv), se = FALSE) +
  geom_point(mapping = aes(x = displ, y = hwy, color = drv))
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-4-6.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_smooth(se = FALSE) +
  geom_point(mapping = aes(color = drv))
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-4-7.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_smooth(mapping = aes(group = drv, linetype = drv), se = FALSE) +
  geom_point(mapping = aes(color = drv))
```

```
## `geom_smooth()` using method = 'loess'
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-4-8.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point(mapping = aes(color = drv, stroke = 2))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-4-9.png)<!-- -->

>1. a line chart:  `geom_curve()`. A boxplot: `geom_boxplot()`. A histogram: `geom_histogram()`. An area chart: `geom_area(stat = "bin")`.

>3. show.legend: logical. Should this layer be included in the legends? NA, the default, includes if any aesthetics are mapped. FALSE never includes, and TRUE always includes.`show.legend = FALSE` will not show the legend labels. If you remove it, it will show the legend labels. You used it earlier in the chapter because you don't need the legend labels.

>4. se: display confidence interval around smooth (TRUE by default, see level to control.

>5. No, these two graphs look the same. By passing a set of mappings to ggplot(), ggplot2 will treat these mappings as global mappings that apply to each geom in the graph. In other words, this code will produce the same plot as the previous code.

## 3.7 Statistical transformations


```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
?geom_bar
```

```
## starting httpd help server ...
```

```
##  done
```

```r
ggplot(data = diamonds) + 
  stat_count(mapping = aes(x = cut))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-5-2.png)<!-- -->

```r
demo <- tribble(
  ~a,      ~b,
  "bar_1", 20,
  "bar_2", 30,
  "bar_3", 40
)

ggplot(data = demo) +
  geom_bar(mapping = aes(x = a, y = b), stat = "identity")
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-5-3.png)<!-- -->

```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, y = ..prop.., group = 1))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-5-4.png)<!-- -->

```r
ggplot(data = diamonds) + 
  stat_summary(
    mapping = aes(x = cut, y = depth),
    fun.ymin = min,
    fun.ymax = max,
    fun.y = median
  )
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-5-5.png)<!-- -->

```r
?stat_bin
```

### 3.7.1 Exercises


```r
#1
?geom_pointrange

#ggplot(data = diamonds, aes(x = cut, y = depth)) + 
#  geom_pointrange(mapping = aes(ymin = min, ymax = max))

#2
?geom_col()
?geom_bar()

#3
?stat_count
?stat_summary
?geoms_point
```

```
## No documentation for 'geoms_point' in specified packages and libraries:
## you could try '??geoms_point'
```

```r
?geom_smooth
?geom_bar
?
#4
?stat_smooth()

#5
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, y = ..prop..))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = color, y = ..prop..))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-6-2.png)<!-- -->

```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, y = ..prop.., group = 1))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-6-3.png)<!-- -->

```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = color, y = ..prop.., group = 1))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-6-4.png)<!-- -->

>1. the default geom associated with stat_summary() summarises the y values for each unique x value.

>2. There are two types of bar charts: geom_bar makes the height of the bar proportional to the number of cases in each group (or if the weight aethetic is supplied, the sum of the weights). If you want the heights of the bars to represent values in the data, use geom_col instead. 

>3.  in common: ggplot2 will treat these mappings as global mappings that apply to each geom in the graph.

>4. `stat_smooth()` Calculation is performed by the (currently undocumented) predictdf generic and its methods. For most methods the standard error bounds are computed using the predict method - the exceptions are loess which uses a t-based approximation, and glm where the normal confidence interval is constructed on the link scale, and then back-transformed to the response scale.

>5.

## 3.8 Position adjustments


```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, colour = cut))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = cut))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-7-2.png)<!-- -->

```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = clarity))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-7-3.png)<!-- -->

```r
ggplot(data = diamonds, mapping = aes(x = cut, fill = clarity)) + 
  geom_bar(alpha = 1/5, position = "identity")
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-7-4.png)<!-- -->

```r
ggplot(data = diamonds, mapping = aes(x = cut, colour = clarity)) + 
  geom_bar(fill = NA, position = "identity")
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-7-5.png)<!-- -->

```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = clarity), position = "fill")
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-7-6.png)<!-- -->

```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = clarity), position = "dodge")
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-7-7.png)<!-- -->

```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy), position = "jitter")
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-7-8.png)<!-- -->





```r
#1
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_point()
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_point(position = "jitter")
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-8-2.png)<!-- -->

```r
#2
?geom_jitter()

#3
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + geom_jitter()
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-8-3.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + geom_count()
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-8-4.png)<!-- -->

```r
?geom_count

#4
?geom_boxplot
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + geom_boxplot(mapping = aes(group = 1, position = "jitter"))
```

```
## Warning: Ignoring unknown aesthetics: position
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-8-5.png)<!-- -->

>1. This problem is known as overplotting. This arrangement makes it hard to see where the mass of the data is. We can improve it by adding `position = "jitter"`.

>2. position: Position adjustment, either as a string, or the result of a call to a position adjustment function.
width: Amount of vertical and horizontal jitter. The jitter is added in both positive and negative directions, so the total spread is twice the value specified here.
height: Amount of vertical and horizontal jitter. The jitter is added in both positive and negative directions, so the total spread is twice the value specified here.

>3. `geom_count` This is a variant geom_point that counts the number of observations at each location, then maps the count to point area. It useful when you have discrete data and overplotting.

>4. 
