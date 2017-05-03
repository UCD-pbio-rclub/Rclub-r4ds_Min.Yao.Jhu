# May-3-ggplot
Min-Yao  
2017年5月1日  

## 3.6 Geometric objects


```r
library(ggplot2)
library(tibble)
library(maps)
```

```
## Warning: package 'maps' was built under R version 3.3.3
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

## 3.9 Coordinate systems

```r
ggplot(data = mpg, mapping = aes(x = class, y = hwy)) + 
  geom_boxplot()
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

```r
ggplot(data = mpg, mapping = aes(x = class, y = hwy)) + 
  geom_boxplot() +
  coord_flip()
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-9-2.png)<!-- -->

```r
#
nz <- map_data("nz")

ggplot(nz, aes(long, lat, group = group)) +
  geom_polygon(fill = "white", colour = "black")
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-9-3.png)<!-- -->

```r
ggplot(nz, aes(long, lat, group = group)) +
  geom_polygon(fill = "white", colour = "black") +
  coord_quickmap()
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-9-4.png)<!-- -->

```r
#
bar <- ggplot(data = diamonds) + 
  geom_bar(
    mapping = aes(x = cut, fill = cut), 
    show.legend = FALSE,
    width = 1
  ) + 
  theme(aspect.ratio = 1) +
  labs(x = NULL, y = NULL)

bar + coord_flip()
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-9-5.png)<!-- -->

```r
bar + coord_polar()
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-9-6.png)<!-- -->

### 3.9.1 Exercises


```r
#1.
bar2 <- ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = clarity))
bar2 + coord_polar()
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

```r
#2
?labs()

#3
?coord_quickmap()
?coord_map()
nz <- map_data("nz")

ggplot(nz, aes(long, lat, group = group)) +
  geom_polygon(fill = "white", colour = "black")
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-10-2.png)<!-- -->

```r
  coord_map()
```

```
## <ggproto object: Class CoordMap, Coord>
##     aspect: function
##     distance: function
##     is_linear: function
##     labels: function
##     limits: list
##     orientation: NULL
##     params: list
##     projection: mercator
##     range: function
##     render_axis_h: function
##     render_axis_v: function
##     render_bg: function
##     render_fg: function
##     train: function
##     transform: function
##     super:  <ggproto object: Class CoordMap, Coord>
```

```r
#4
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) +
  geom_point() + 
  geom_abline() +
  coord_fixed()  
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-10-3.png)<!-- -->

```r
?coord_fixed()
?geom_abline()
```

>1. Turn a stacked bar chart into a pie chart using coord_polar().

>2. `labs` Good labels are critical for making your plots accessible to a wider audience. Ensure the axis and legend labels display the full variable name. Use the plot title and subtitle to explain the main findings. It's common to use the caption to provide information about the data source. You can also set axis and legend labels in the individual scales (using the first argument, the name. I recommend doing that if you're changing other scale options.

>3. coord_map projects a portion of the earth, which is approximately spherical, onto a flat 2D plane using any projection defined by the mapproj package. Map projections do not, in general, preserve straight lines, so this requires considerable computation. coord_quickmap is a quick approximation that does preserve straight lines. It works best for smaller areas closer to the equator.

>4.`coord_fixed`A fixed scale coordinate system forces a specified ratio between the physical representation of data units on the axes. The ratio represents the number of units on the y-axis equivalent to one unit on the x-axis. The default, ratio = 1, ensures that one unit on the x-axis is the same length as one unit on the y-axis. Ratios higher than one make units on the y axis longer than units on the x-axis, and vice versa. This is similar to eqscplot, but it works for all types of graphics.
> `geom_abline()`These geoms add reference lines (sometimes called rules) to a plot, either horizontal, vertical, or diagonal (specified by slope and intercept). These are useful for annotating plots.

## 3.10 The layered grammar of graphics


```r
ggplot(data = diamonds) + 
  stat_count(mapping = aes(x = cut, y = ..count.., fill = ..count..))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

# use ggplot to make a graph using some of your own data.


```r
IVHall <- read.csv("D:/2017SQ/R club/Rclub-r4ds_Min.Yao.Jhu/R-club-May-3/IVHall-reduced.csv")
ggplot(data = IVHall) +
  geom_boxplot(mapping = aes(x = identity, y = total.number))
```

![](May-3-ggplot_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

