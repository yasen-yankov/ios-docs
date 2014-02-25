---
title: Area
meta_title: Area Series
slug: chart-series-area
tags: Chart, iOS, area, series
publish: true
ordinal: 1
---

# Chart Series: Area

As a derivative of <code>TKLineSeries</code> series, <code>TKAreaSeries</code> plots its data points in line (spline). Once positioned on a plane the points are connected to form a line (spline). Further, the area enclosed between this line and the axis is filled. Below is a sample snippet that demonstrates how to set up two Area series:

	TKChartAreaSeries* seriesForIncomes = [[TKChartAreaSeries alloc] initWithItems:array1];
	[chart addSeries:seriesForIncomes];
    
	TKChartAreaSeries *seriesForExpenses = [[TKChartAreaSeries alloc] initWithItems:array2];
	[chart addSeries:seriesForExpenses];

<img src="../images/chart-series-area001.png"/>

##Configure stacking of line series

The <code>TKChartAreaSeries</code> can be combined by using different stack modes.

The Stack plots the points on top of each other:

	TKChartStackInfo *stackInfo = [[TKChartStackInfo alloc] initWithID:@(1) withStackMode:TKChartStackModeStack];

	TKChartAreaSeries *series1 = [[TKChartAreaSeries alloc] initWithItems:dataPoints1];
	series1.stackInfo = stackInfo;

	TKChartAreaSeries *series2 = [[TKChartAreaSeries alloc] initWithItems:dataPoints2];
	series2.stackInfo = stackInfo;

	[chart beginUpdates];
	[chart addSeries:series1];
	[chart addSeries:series2];
	[chart endUpdates];

<img src="../images/chart-series-area004.png"/>

The Stack100 displays the value as percent:

	TKChartStackInfo *stackInfo = [[TKChartStackInfo alloc] initWithID:@(1) withStackMode:TKChartStackModeStack100];

	TKChartAreaSeries *series1 = [[TKChartAreaSeries alloc] initWithItems:dataPoints1];
	series1.stackInfo = stackInfo;

	TKChartAreaSeries *series2 = [[TKChartAreaSeries alloc] initWithItems:dataPoints2];
	series2.stackInfo = stackInfo;

	[chart beginUpdates];
	[chart addSeries:series1];
	[chart addSeries:series2];
	[chart endUpdates];

<img src="../images/chart-series-area005.png"/>

##Configure visual appearance of area series

If you want to change series to draw a spline instead of a line, you should set the <code>spline</code> property to *YES*:

	TKChartAreaSeries* seriesForAnnualRevenue = [[TKChartAreaSeries alloc] initWithItems:annualRevenueData];
	seriesForAnnualRevenue.title = @"Annual Revenue";
	seriesForAnnualRevenue.spline = YES;
	[chart addSeries:seriesForAnnualRevenue];

<img src="../images/chart-series-area002.png"/>

If you want to change the series' fill and stroke, you should use the following code snippet:

	TKChartAreaSeries* seriesForAnnualRevenue = [[TKChartAreaSeries alloc] initWithItems:array1];
	seriesForAnnualRevenue.style.palette = [[TKChartPalette alloc] init];
	TKChartPaletteItem *palleteItem = [[TKChartPaletteItem alloc] init];
	palleteItem.stroke = [TKStroke strokeWithColor:[UIColor brownColor]];
	palleteItem.fill = [TKSolidFill solidFillWithColor:[UIColor redColor]];
	[chart addSeries:seriesForAnnualRevenue];

<img src="../images/chart-series-area003.png"/>
