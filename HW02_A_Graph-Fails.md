Corrected graphs, answers, and comments
================
Bei Wang

``` r
knitr::opts_chunk$set(echo = TRUE, error = TRUE)
```

HW02 Part A
-----------

In this document, I will add some examples of some coding mistakes, it is up to you to figure out why the graphs are messing up.

### First load packages

It is always best to load the packages you need at the top of a script. It's another common coding formatting standard (like using the assignment operator instead of the equals sign). In this case, it helps people realize what they need to install for the script and gives an idea of what functions will be called.

It is also best coding practice to only call the packages you use, so if you use a package but end up tossing the code you use for it, then make sure to remove loading it in the first place. For example, I could use `library("tidyverse")` but since this script will only be using ggplot2, I only load ggplot2.

``` r
library("ggplot2")
library("magrittr") #so I can do some piping
```

### Graph Fail 1

What error is being thrown? How do you correct it? (hint, the error message tells you)

**My answer/comment:**

*the following 2 errors have been corrected.*

*1.error 1: use "+"" instead of "%&gt;%"*

*2.error 2: "city" was misspelled; there is a variable called "cty" that means city miles per gallow.*

``` r
data(mpg) #this is a dataset from the ggplot2 package

mpg %>% 
  ggplot(mapping = aes(x = cty, y = hwy, color = "blue")) +
  geom_point()
```

![](HW02_A_Graph-Fails_files/figure-markdown_github/unnamed-chunk-1-1.png)

### Graph Fail 2

Why aren't the points blue? It is making me blue that the points in the graph aren't blue :\`(

**My answer/comment:**

*It seems the color command should be wrapped in geom\_point(), and my guess is this is because color belongs to this layer instead of ggplot(). I'm not so sure about this.*

``` r
ggplot(mpg, aes(x = displ, y = hwy)) + 
  geom_point(color = "blue")
```

![](HW02_A_Graph-Fails_files/figure-markdown_github/unnamed-chunk-2-1.png)

### Graph Fail 3

Two mistakes in this graph. First, I wanted to make the the points slightly bolder, but changing the alpha to 2 does nothing. What does alpha do and what does setting it to 2 do? What could be done instead if I want the points slightly bigger?

**My answer/comment:**

*alpha is for degree of transparency of the points, which ranges from 0(transparent) to 1(opaque). Using "size=2" can make the points bolder.*

Second, I wanted to move the legend on top of the graph since there aren't any points there, putting it at approximately the point/ordered pair (5, 40). How do you actually do this? Also, how do you remove the legend title ("class")? Finally, how would you remove the plot legend completely?

**My answer/comment**

*The position of the legend can be changed by using theme(legend.position = c()), and I found (0.7.0.9) is a good position for this graph. *

*The legend title can be removed by using theme(legend.title = element\_blank())*

*Using them(legend.position= "none") could remove the legend*

``` r
mpg %>% 
ggplot() + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class), size = 2) + 
  theme(legend.direction = "horizontal") + 
  theme(legend.position = c(0.7, 0.9))+
  theme(legend.title = element_blank())
```

![](HW02_A_Graph-Fails_files/figure-markdown_github/unnamed-chunk-3-1.png)

### Graph Fail 4

I wanted just one smoothing line. Just one line, to show the general relationship here. But that's not happening. Instead I'm getting 3 lines, why and fix it please?

**My answer/comment**

*Wrapping color=drv in ggplot() will apply the color to every layerl, which is why there were three seperate lines. To have one line, I moved the color=drv to the geom\_point. This way it's only applied to the points.*

*I also noticed an interesting fact that the block of codes below would fail with an error message saying "%&gt;% cannot be found" and wont if I didnt run the library("magrittr") in the very first r code block in this file.*

``` r
mpg %>%  
ggplot(mapping = aes(x = displ, y=hwy)) + 
  geom_point(mapping = aes(color = drv)) + 
  geom_smooth(se = F) 
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](HW02_A_Graph-Fails_files/figure-markdown_github/unnamed-chunk-4-1.png)

### Graph Fail 5

I got tired of the points, so I went to boxplots instead. However, I wanted the boxes to be all one color, but setting the color aesthetic just changed the outline? How can I make the box one color, not just the outline?

Also, the x-axis labels were overlaping, so I rotated them. But now they overlap the bottom of the graph. How can I fix this so axis labels aren't on the graph?

**My answer/comment**

*Using fill instead of color will change the box colors.*

*Using hjust = 1 will adjust the x-axis labels to a proper position without overlapping with the graph.*

``` r
ggplot(data = mpg, mapping = aes(x = manufacturer, y = cty, fill = manufacturer)) + 
  geom_boxplot() + 
  theme(axis.text.x = element_text(angle = 45, hjust=1))
```

![](HW02_A_Graph-Fails_files/figure-markdown_github/unnamed-chunk-5-1.png)
