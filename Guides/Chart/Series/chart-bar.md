---
title: Bar
slug: chart-series-bar
tags: Chart, iOS, bar, series
publish: true
ordinal: 2
---

Working with TKChartBarSeries
==============================

##Overview

TKChartBarSeries are used to visualize data points as bar blocks where the width of each bar denotes the magnitude of its value. The following snippet demonstrates how to manually populate one Bar series:

	TKChartBarSeries *series = [[TKChartBarSeries alloc] initWithItems:array];
	[chart addSeries:series];

<img src="../images/chart-series-bar001.png"/>

##Configure clustering of bar series

If you want to cluster multiple bar series side by side, they should use a shared y-axis:

	NSArray *categories = @[ @"Greetings", @"Perfecto", @"NearBy", @"Family Store", @"Fresh & Green" ];
	TKChartCategoryAxis *categoryAxis = [[TKChartCategoryAxis alloc] initWithCategories:categories];
	chart.yAxis = categoryAxis;
    
	NSArray *values1 = @[ @87, @65, @82, @97, @91 ];
	NSMutableArray *dataPoints1 = [[NSMutableArray alloc] init];
    
	for (int i = 0; i<values1.count; i++) {
   		[dataPoints1 addObject:[[TKChartDataPoint alloc] initWithX:values1[i] Y:categories[i]]];
	}
    
	TKChartSeries *series1 = [[TKChartBarSeries alloc] initWithItems:dataPoints1];
	series1.yAxis = categoryAxis;
    
	NSArray *values2 = @[ @82, @80, @87, @69, @95 ];
	NSMutableArray *dataPoints2 = [[NSMutableArray alloc] init];

	for (int i = 0; i<values2.count; i++) {
    	[dataPoints2 addObject:[[TKChartDataPoint alloc] initWithX:values2[i] Y:categories[i]]];
	}
    
	TKChartSeries *series2 = [[TKChartBarSeries alloc] initWithItems:dataPoints2];
	series2.yAxis = categoryAxis;
    
	[chart beginUpdates];
	[chart addSeries:series1];
	[chart addSeries:series2];
	[chart endUpdates];

<img src="../images/chart-series-bar002.png"/>

##Configure stacking of bar series

The TKChartBarSeries can be combined by using different stack modes.

The Stack plots the points on top of each other:

	TKChartStackInfo *stackInfo = [[TKChartStackInfo alloc] initWithID:@(1) withStackMode:TKChartStackModeStack];

	TKChartBarSeries *series1 = [[TKChartBarSeries alloc] initWithItems:dataPoints1];
	series1.stackInfo = stackInfo;

	TKChartBarSeries *series2 = [[TKChartBarSeries alloc] initWithItems:dataPoints2];
	series2.stackInfo = stackInfo;

	[chart beginUpdates];
	[chart addSeries:series1];
	[chart addSeries:series2];
	[chart endUpdates];

<img src="../images/chart-series-bar003.png"/>

The Stack100 displays the value as percent:

	TKChartStackInfo *stackInfo = [[TKChartStackInfo alloc] initWithID:@(1) withStackMode:TKChartStackModeStack100];

	TKChartBarSeries *series1 = [[TKChartBarSeries alloc] initWithItems:dataPoints1];
	series1.stackInfo = stackInfo;

	TKChartBarSeries *series2 = [[TKChartBarSeries alloc] initWithItems:dataPoints2];
	series2.stackInfo = stackInfo;

	[chart beginUpdates];
	[chart addSeries:series1];
	[chart addSeries:series2];
	[chart endUpdates];

<img src="../images/chart-series-bar004.png"/>

##Configure visual appearance of bar series

If you would like to customize the appearance of bar series, you should change its **style** properties.

You can change the fill and stroke in the following manner:

	TKChartBarSeries *series = [[TKChartBarSeries alloc] initWithItems:array];
	series.style.palette = [[TKChartPalette alloc] init];
	TKChartPaletteItem *palleteItem = [[TKChartPaletteItem alloc] init];
	palleteItem.fill = [TKSolidFill solidFillWithColor:[UIColor redColor]];
	palleteItem.stroke = [TKStroke strokeWithColor:[UIColor blackColor]];
	[series.style.palette addPaletteItem:palleteItem];
	[chart addSeries:series];

<img src="../images/chart-series-bar005.png"/>

You can change the gap between columns with the following code snippet:

	TKChartBarSeries *series = [[TKChartBarSeries alloc] initWithItems:array];
	series.gapLength = 0.5;
	[chart addSeries:series];

Note that the value should be between 0 and 1, where a value of 0 means that a bar would take the entire space between two ticks, while a value of 1 means the bar will have zero width as all the space should appear as a gap.

<img src="../images/chart-series-bar006.png"/>
