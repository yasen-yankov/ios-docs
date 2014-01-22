---
title: Categorical Axis
slug: chart-axes-categorical
tags: Chart, iOS, categorical, axis, axes
publish: true
ordinal: 2
---

TKChartCategoryAxis
===================

##Overview##

TKChart uses Categorical axes to plot data that contains categorical values. The axis is valid only in the context of Cartesian series. It also introduces several important properties:

- **majorTickInterval** - defines an interval among major axis ticks.

- **minorTickInterval** - defines an interval among minor axis ticks.

- **baseline** - contains a value, which defines how the series data should be aligned. For example, The TKChartBarSeries might render its bars up and down  depending on whether its value is greater or less than the baseline value.

- **offset** - determines an axis value where the axis is crossed with another axis.

##Configure a TKChartCategoryAxis##

You can configure a category axis by settings its categories property. You should use the following code snippet as a sample:

    NSArray *categories = @[ @"Greetings", @"Perfecto", @"NearBy", @"Family Store", @"Grocery" ];
    NSArray *values = @[ @70, @75, @58, @59, @88 ];
    
    NSMutableArray *array = [[NSMutableArray alloc] init];

    for (int i = 0; i<values.count; i++) {
        [array addObject:[[TKChartDataPoint alloc] initWithX:categories[i] Y:values[i]]];
    }
    
    TKChartCategoryAxis *xAxis = [[TKChartCategoryAxis alloc] initWithCategories:categories];
    chart.xAxis = xAxis;

You can specify the axis range by setting the minumum and maximum indexes of categories:

    [xAxis setRangeWithMinimum:@0 andMaximum:@2];

 <img src="../images/chart-axes-category003.png"/>

##Setting the plot mode of axis##

 The TKChartAxisPlotMode is used by the axis to plot the data. Possible values are TKChartAxisPlotModeBetweenTicks and TKChartAxisPlotModeOnTicks. TKChartAxisPlotModeBetweenTicks plots points in the middle of the range, defined by two ticks. OnTicks plots the points over each tick. 

 You should use the following lines of code to alter this behavior:

	xAxis.plotMode = TKChartAxisPlotModeBetweenTicks;

<img src="../images/chart-axes-category001.png"/>

	xAxis.plotMode = TKChartAxisPlotModeOnTicks;

<img src="../images/chart-axes-category002.png"/>
