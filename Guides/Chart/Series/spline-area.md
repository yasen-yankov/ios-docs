---
title: Spline Area
meta_title: Spline Area Series
slug: chart-series-spline-area
tags: Chart, iOS, spline, area, series
publish: true
ordinal: 3
---

#Chart Series: Spline Area

TKChartSplineAreaSeries series is a derivative of TKChartAreaSeries. It allows the area between the curve and the corresponding axis to be colored in an arbitrary way. Below is a sample snippet that demonstrates how to set up a spline series:

	TKChartAreaSeries* seriesForAnnualRevenue = [[TKChartAreaSeries alloc] initWithItems:annualRevenueData];
	[chart addSeries:seriesForAnnualRevenue];

<img src="../images/chart-series-spline-area001.png"/>

