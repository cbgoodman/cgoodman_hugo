---
title: "County Supervisors per 100,000 Residents"
date: 2018-11-30T17:32:26-06:00
categories: [R, dataviz, counties, local-govt]
footnotes: false
htmlwidgets: false
mathjax: false
draft: true
---

Created in **R** with `ggplot2`. The relevant code is below.


{{% figure src="files/misc/supervisors.png" alt="" caption="County supervisors per 100,000 residents" %}}
<!--more-->

Full code and data can be found on [Github](https://github.com/cbgoodman/county-elect). Code to create the figure can be found below.

{{< highlight r >}}
library(tidyverse)

# read in data
county <- read.csv("county.csv")

# calculate supervisors per 100,000 population
county$pc.supervisor <- county$supervisors/(county$pop17/100000)

# create annotation

annot <- read.table(text=
  "county|number|just|text
  15.5|0.625|0|Broward & Orange County, FL are the median county<br>with 0.45 supervisors per 100,000 residents.
  40.5|0.375|1|Some of the largest U.S. counties have the<br>fewest supervisors per 100,000 residents.",
  sep="|", header=TRUE, stringsAsFactors=FALSE)
annot$text <- gsub("<br>", "\n", annot$text)

# plot
p <- ggplot(data=county,
  aes(x=reorder(county, -pc.supervisor), y=pc.supervisor, width=0.9))+
  geom_bar(stat="identity", fill="#E69F00")+
  scale_y_continuous(breaks=seq(0, 1.75, by=0.25))+
  # read in annotations
  geom_label(data=annot, aes(x=county, y=number, label=text, hjust=just),
    family="Open Sans Condensed Light", lineheight=0.95,
    size=3.5, label.size=0, color="#2b2b2b")+
  # Theming
  labs(
    title="Boards of supervisors tend to be small relative to population",
    subtitle="County supervisors/commissioners per 100,000 residents, 40 largest U.S. counties, 2017",
    caption="Author: Chris Goodman (@cbgoodman), Data: U.S. Census Bureau & Author's calculations.",
    y=NULL,
    x=NULL) +
  theme_minimal(base_family="Open Sans Condensed Light") +
  # light, dotted major y-grid lines only
  theme(panel.grid=element_line())+
  theme(panel.grid.major.y=element_line(color="#2b2b2b", linetype="dotted", size=0.15))+
  theme(panel.grid.major.x=element_blank())+
  theme(panel.grid.minor.x=element_blank())+
  theme(panel.grid.minor.y=element_blank())+
  # light x-axis line only
  theme(axis.line=element_line())+
  theme(axis.line.y=element_blank())+
  theme(axis.line.x=element_blank())+
  # tick styling
  theme(axis.ticks=element_line())+
  theme(axis.ticks.x=element_blank())+
  theme(axis.ticks.y=element_blank())+
  theme(axis.ticks.length=unit(5, "pt"))+
  # x-axis labels
  theme(axis.text.x=element_text(size=10, angle=90, hjust=0.95,vjust=0.2))+
  # breathing room for the plot
  theme(plot.margin=unit(rep(0.5, 4), "cm"))+
  # move the y-axis tick labels over a bit
  #theme(axis.text.y=element_text(margin=margin(r=-5)))+
  # make the plot title bold and modify the bottom margin a bit
  theme(plot.title=element_text(family="Open Sans Condensed Bold", margin=margin(b=15)))+
  # make the subtitle italic
  theme(plot.subtitle=element_text(family="Open Sans Condensed Light Italic"))+
  theme(plot.caption=element_text(size=8, hjust=0, margin=margin(t=15)))

ggsave(plot=p, "supervisors.png", width=10, height=6, units="in", dpi="retina")
{{< /highlight >}}
