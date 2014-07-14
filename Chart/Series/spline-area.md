---
title: Spline Area
page_title: Spline Area Series
position: 3
---

# Chart Series: Spline Area

<code>TKChartSplineAreaSeries</code> series is a derivative of TKChartAreaSeries. It allows the area between the curve and the corresponding axis to be colored in an arbitrary way. Below is a sample snippet that demonstrates how to set up a spline series:

	TKChartAreaSeries* seriesForAnnualRevenue = [[TKChartAreaSeries alloc] initWithItems:annualRevenueData];
	[chart addSeries:seriesForAnnualRevenue];

<img src="../../images/chart-series-spline-area001.png"/>

