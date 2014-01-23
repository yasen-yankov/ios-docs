---
title: Column
meta_title: Column Series
slug: chart-series-column
tags: Chart, iOS, column, series
publish: true
ordinal: 3
---

TKColumnSeries are used to visualize data points as column blocks where the height of each bar denotes the magnitude of its value. The following snippet demonstrates how to manually populate one ColumnSeries:

	NSArray *categories = @[ @"Greetings", @"Perfecto", @"NearBy", @"Family Store", @"Fresh & Green" ];
	NSArray *values = @[ @55, @75, @85, @50, @93 ];

	NSMutableArray *array = [[NSMutableArray alloc] init];

	for (int i = 0; i<values.count; i++) {
    	[array addObject:[[TKChartDataPoint alloc] initWithX:categories[i] Y:values[i]]];
	}
    
	TKChartColumnSeries *series = [[TKChartColumnSeries alloc] initWithItems:array];
	[chart addSeries:series];

<img src="../images/chart-series-column001.png"/>

##Configure clustering of column series

If you want to cluster multiple column series side by side, they should use a shared x-axis:

	NSArray *categories = @[ @"Greetings", @"Perfecto", @"NearBy", @"Family Store", @"Fresh & Green" ];

	TKChartCategoryAxis *categoryAxis = [[TKChartCategoryAxis alloc] initWithCategories:categories];
	chart.xAxis = categoryAxis;

	NSArray *values1 = @[ @87, @65, @82, @97, @91 ];
	NSMutableArray *dataPoints1 = [[NSMutableArray alloc] init];

	for (int i = 0; i<values1.count; i++) {
    	[dataPoints1 addObject:[[TKChartDataPoint alloc] initWithX:categories[i] Y:values1[i]]];
	}

	TKChartColumnSeries *series1 = [[TKChartColumnSeries alloc] initWithItems:dataPoints1];
	series1.xAxis = categoryAxis;
	NSArray *values2 = @[ @82, @80, @87, @69, @95 ];
	NSMutableArray *dataPoints2 = [[NSMutableArray alloc] init];

	for (int i = 0; i<values2.count; i++) {
    	[dataPoints2 addObject:[[TKChartDataPoint alloc] initWithX:categories[i] Y:values2[i]]];
	}

	TKChartColumnSeries *series2 = [[TKChartColumnSeries alloc] initWithItems:dataPoints2];
	series2.xAxis = categoryAxis;
	[chart beginUpdates];
	[chart addSeries:series1];
	[chart addSeries:series2];
	[chart endUpdates];

<img src="../images/chart-series-column002.png"/>

##Configure stacking of column series

The TKChartColumnSeries can be combined by using different stack modes.

The Stack plots the points on top of each other:

	TKChartStackInfo *stackInfo = [[TKChartStackInfo alloc] initWithID:@(1) withStackMode:TKChartStackModeStack];
    
	TKChartColumnSeries *series1 = [[TKChartColumnSeries alloc] initWithItems:dataPoints1];
	series1.stackInfo = stackInfo;
    
	TKChartColumnSeries *series2 = [[TKChartColumnSeries alloc] initWithItems:dataPoints2];
	series2.stackInfo = stackInfo;

<img src="../images/chart-series-column003.png"/>

The Stack100 displays the value as percent:

	TKChartStackInfo *stackInfo = [[TKChartStackInfo alloc] initWithID:@(1) withStackMode:TKChartStackModeStack100];
    
	TKChartColumnSeries *series1 = [[TKChartColumnSeries alloc] initWithItems:dataPoints1];
	series1.stackInfo = stackInfo;
    
	TKChartColumnSeries *series2 = [[TKChartColumnSeries alloc] initWithItems:dataPoints2];
	series2.stackInfo = stackInfo;

<img src="../images/chart-series-column004.png"/>

##Configure visual appearance of column series

If you want to customize the appearance of a column series, you should change its **style** properties.

You can change the fill and stroke in the following manner:

	TKChartColumnSeries *series = [[TKChartColumnSeries alloc] initWithItems:array];
	series.style.palette = [[TKChartPalette alloc] init];
	TKChartPaletteItem *palleteItem = [[TKChartPaletteItem alloc] init];
	palleteItem.fill = [TKSolidFill solidFillWithColor:[UIColor redColor]];
	palleteItem.stroke = [TKStroke strokeWithColor:[UIColor blackColor]];
	[series.style.palette addPaletteItem:palleteItem];
	[chart addSeries:series];

<img src="../images/chart-series-column005.png"/>

You can change the gap between columns with the following code snippet:

	TKChartColumnSeries *series = [[TKChartColumnSeries alloc] initWithItems:array];
	series.gapLength = 0.5;
	[chart addSeries:series];

Note that the value should be between 0 and 1, where a value of 0 means that a bar would take the entire space between two ticks, while a value of 1 means the bar will have zero width as all the space should appear as a gap.

<img src="../images/chart-series-column006.png"/>
