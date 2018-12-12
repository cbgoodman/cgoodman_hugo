---
title: "Douglas County Migration Patterns, 2016"
date: 2018-12-09T23:14:08-06:00
categories: [R, dataviz]
footnotes: false
htmlwidgets: false
mathjax: false
draft: true
---
Among the many things that I do professionally, I am involved with the [Greater Omaha Chamber Young Professionals](https://www.omahachamber.org/omahayp/). One of the primary goals of this group is the help the Chamber devise strategies to attract and retain young talent in Omaha. As an urban minded data person, this calls for taking a look at how well Omaha (or in this instance, Douglas County, NE) is doing, particularly on the retention piece.
<!--more-->
Luckily, there are a few data source that allow someone to get some idea of the migration inflows and outflows from a particular county. The first is from the American Community Survey (ACS) conducted by the Census Bureau. The county-to-county migration flow data from the ACS can be access through the [Census Flow Mapper](https://flowsmapper.geo.census.gov/map.html). The second source is from the Internal Revenue Service's [Sources of Income tax data](https://www.irs.gov/statistics/soi-tax-stats-migration-data). Based on changes in address on individual income tax returns, these data give us another picture of county-to-county migration patterns.

## American Community Survey
{{% figure src="http://localhost:1313/files/misc/douglas-acs-net.png" alt="Douglas County ACS Net Migration" caption="" %}}

{{% figure src="http://localhost:1313/files/misc/douglas-acs-out.png" alt="Douglas County ACS Out Migration" caption="" %}}
{{% figure src="http://localhost:1313/files/misc/douglas-acs-in.png" alt="Douglas County ACS Out Migration" caption="" %}}

## IRS Sources of Income
{{% figure src="http://localhost:1313/files/misc/douglas-irs-out.png" alt="Douglas County IRS Out Migration" caption="" %}}

{{% figure src="http://localhost:1313/files/misc/douglas-irs-in.png" alt="Douglas County IRS Out Migration" caption="" %}}


{{< highlight r >}}


{{< /highlight >}}
