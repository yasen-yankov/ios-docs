---
title: Donut
meta_title: Donut Series
slug: chart-series-donut
tags: Chart, iOS, donut, series
publish: true
ordinal: 3
---

#Chart Series: Donut

TKChartDonutSeries derives from <code>TKChartPieSeries</code> and it represents a donut chart. The <code>innerRadius</code> property determines the width of the donut, and it is measured in values between 0 and 1. The higher value you set in the range between 0 and 1, the thinner the donut will be. For example, a value of 0.9 will make the donut chart take only 0.1 percent of the whole pie chart surface.

Here is an example of a donut chart:

    series.innerRadius = 0.5;
    
<img src="../images/chart-series-donut001.png"/>

