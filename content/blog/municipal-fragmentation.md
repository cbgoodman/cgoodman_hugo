---
title: "Municipal Fragmentation in U.S. Metro Areas in 3 Maps"
date: 2021-04-16T15:52:02-05:00
categories: [R, dataviz, maps]
footnotes: false
htmlwidgets: false
mathjax: false
---

Over on Twitter, Dan Immergluck (GSU) asked about what municipal fragmentation in the U.S. at the metropolitan level looked like. I, an expert on local government fragmentation, saw it as my duty to get to the bottom of this. I have the data to do it. It only needs to be reworked slightly.

<!--more-->

Ultimately, it matters which CBSAs you include in how the map (and rankings) look. This is obvious but essential. Including the smaller CBSAs (50,000 to 250,000 in population) leads to many of these smaller areas dominating the rankings, largely in the Upper Midwest and Plains.

{{% figure src="/files/misc/munifrag-ragg.png" alt="Municipal fragmentation, 2017, all CBSAs" caption="" %}}

Limiting the sample of CBSAs to those larger than 250,000 changes things slightly, with the center of gravity moving south and east somewhat.

{{% figure src="/files/misc/munifrag-250k-ragg.png" alt="Municipal fragmentation, 2017, CBSAs larger than 250,000" caption="" %}}

Lastly, constraining the sample to only those CBSAs larger than 1,000,000 in population gives the prototypical ranking with Pittsburgh and St. Louis at the top of the list. Generally, the most fragmented CBSAs are located in Rust Belt areas.

{{% figure src="/files/misc/munifrag-1m-ragg.png" alt="Municipal fragmentation, 2017, CBSAs larger than 1,000,000" caption="" %}}

H/T to Andrew Rumbach (TAMU) for suggesting these maps needed a permanent home (more permanent than Twitter).
