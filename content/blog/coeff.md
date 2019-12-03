---
title: "Custom Coefficient Graphs"
date: 2019-12-03T11:33:45-06:00
categories: [Dataviz,R]
footnotes: false
htmlwidgets: false
mathjax: false
---

Recently, I was asked by a reviewer to include a large number of regression results in a manuscript I am revising. In my experience, attempting to display more than a few regression results in tabular format is a fool's errand so I went looking for a more visual means of delivering the content. My attempt at doing this is complicated by the estimation taking place in one piece of software (Stata) and visualization taking place in another ( R ).

<!--more-->

This disconnect between estimation and visualization adds an extra step (and could be solved by doing the estimation in R, something I have decided not to do for the time being) and prevents me from using one of the many R packages for coefficient plotting. Therefore, I estimate 4 regressions in Stata (using my preferred `reghdfe` command) and extract the coefficients, standard errors, and standard deviation (for standardization) of each variable along with the model label. I then move over to R. Borrowing heavily from [Thomas Leeper](https://thomasleeper.com/Rcourse/Tutorials/olscoefplot.html) and [Andrew Heiss](https://gist.github.com/andrewheiss/91250f9d23e889b30ccf), I import the data, standardize the coefficients and standard errors, and build the plot (see below).

{{< gist cbgoodman e0f399f3e8d691a9907285a406d050ec >}}

The primary issue is the 4 models are highly related so using something like `facet_wrap` is a bit inappropriate. I want the coefficients stacked. This is easily achieved using the `group` option in `geom_pointrange`. A little adjustment is necessary to get the points and ranges to be more visible in what will eventually be a printed figure. The output can be seen below.

{{% figure src="files/misc/popgrow-coeff.png" alt="" caption="" %}}

I think this is a very clean way to display a lot of dense information. An added benefit is `facet_wrap` can be used for subgroup analysis.
