---
title: "Figure Desaturation in R"
date: 2020-01-22T16:56:02-06:00
categories: [x,y]
footnotes: false
htmlwidgets: false
mathjax: false
draft: true
---


<!--more-->
```R```
required: [colorblindr](https://github.com/clauswilke/colorblindr), cowplot, ggplot2

```r
p_des <- edit_colors(p, desaturate)
ggdraw(p_des)
ggsave(plot=p_des, filename = "pcpigrow-coeff-region-des.pdf", units="in", device = cairo_pdf)
```

{{% figure src="" alt="" caption="" %}}


{{< highlight r >}}


{{< /highlight >}}
