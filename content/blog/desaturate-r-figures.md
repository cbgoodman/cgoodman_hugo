---
title: "How to Desaturate Figures for Publication using R"
date: 2020-02-25T10:26:25-06:00
categories: [dataviz, R]
footnotes: false
htmlwidgets: false
mathjax: false
draft: true
---

Many academic journals require figures in greyscale. This can be done relatively simply by printing to PDF as greyscale; however, this doesn't give you a) a way to preview what the resulting figure will look like and b) much control over the process of desaturation. If you're making figures in ```R```, this process is almost as easy as the more simplistic print to PDF method.

<!--more-->
We'll need a few extra libraries before we can get started. The primary means we'll use to examine the desaturated figures (and look for issues with colorblindness) is ```colorblindr```. This depends on the development versions of ```cowplot``` and ```colorspace``` (the latter we'll use to desaturate) so we need to make sure those two are install before we install ```colorblindr```.

``` R
devtools::install_github("wilkelab/cowplot")
install.packages("colorspace")
devtools::install_github("clauswilke/colorblindr")
```

Once that's all done, we can load up ```tidyverse``` and our newly installed libraries and get to making a figure. This part is totally up to you, but I've created a very common plot using the included **mtcars** data in ```R```.

```R
library(tidyverse)
library(cowplot)
library(colorspace)
library(colorblindr)

plot.data <- mtcars

p <- ggplot(plot.data, aes(x = wt, y = mpg, color = factor(cyl))) +
  geom_point(size = 3) +
  theme_minimal()
```

This uses the built in color scheme.

{{% figure src="files/misc/desaturate-ex1.png" alt="" caption="" %}}

If we wanted to desaturate this figure, what would it look like? How would we know if there is appropriate color separation so the reader could determine the various *cyl* levels? ```colorblindr``` gives us two ways to preview this; one static and one interactive.

```R
cvd_grid(p) # prints grid of colorblind types
view_cvd(p) # starts an interactive app
```

As can be seen below, the standard color palette in ```ggplot``` is ok (but not great) on three of the colorblindness scales, but completely falls flat on desaturation. There's no separation between the number of engine cylinders.

{{% figure src="files/misc/desaturate-ex2.png" alt="" caption="" %}}

How can we fix this? First, we need a new color scale. I am partial to *[viridis](https://cran.r-project.org/web/packages/viridis/vignettes/intro-to-viridis.html)* as it is designed to solve many of the problems outlined above (and built into ```R```).

```R
p.viridis <- p +
  scale_colour_viridis_d()
```

{{% figure src="files/misc/desaturate-ex3.png" alt="" caption="" %}}

When we subject this new figure to our colorblindness test, it performs much better. Important for our purposes, there is ample separation for desaturation.
```R
cvd_grid(p.viridis)
```

{{% figure src="files/misc/desaturate-ex4.png" alt="" caption="" %}}

### How to desaturate
Once we have a figure that is amenable to desaturation, how do we do it? That's where ```colorspace``` comes in. It can do far more than we are going to use it for (see the [CRAN vignette for more info](https://cran.r-project.org/web/packages/colorspace/vignettes/colorspace.html)), but it makes desaturating a breeze.

```R
p.des.viridis <- edit_colors(p.viridis, desaturate)
ggdraw(p.des.viridis)
```

Using ```edit_colors(foo, desaturate)```, we can completely desaturate our figure. And ```ggdraw``` plots the figure for easy viewing. As can be seen below, our mission is accomplished.

{{% figure src="files/misc/desaturate-ex5.png" alt="" caption="" %}}

The last step is to save the figure for upload. I tend to save these files as PDFs; however, the journal likely has its own preferred file format (TIFF being really common).

```R
ggsave(plot=p.des.viridis, "p_des_viridis.pdf", dpi=300, device = cairo_pdf)
```

And that's it! Easy, reproducible desaturation (with a brief sidebar into colorblind friendly color palettes).
