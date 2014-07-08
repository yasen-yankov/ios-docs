---
title: Numeric
meta_title: Numeric Axis
slug: chart-axes-numeric
tags: Chart, iOS, axes, axis, numeric
publish: true
ordinal: 4
---

# Chart Axes: Numeric

<code>TKChart</code> uses Linear axes to plot data containing numerical values. It is valid only in the context of Cartesian Area, this axis is created by default when you add Bar, Line, Area and Scatter series. It also introduces several important properties:

- <code>majorTickInterval</code> - defines the interval between major axis ticks.
- <code>minorTickInterval</code> - defines the interval between minor axis ticks.
- <code>baseline</code> - defines how the series data should be aligned. For example, The TKChartBarSeries might render its bars up and down side depending on whether its value is greater or less than the baseline value.
- <code>offset</code> - Determines an axis value where the axis is crossed with another axis.

##Configure a TKChartNumericAxis##

You can configure a numeric axis by initializing it and setting it as the main x-axis or y-axis of the chart:

	TKChartNumericAxis *gdpInPoundsYAxis = [[TKChartNumericAxis alloc] init];
	gdpInPoundsYAxis.majorTickInterval = @50;
	chart.yAxis = gdpInPoundsYAxis;

You can specify the axis range by setting the minimum and maximum indexes of categories:

    [gdpInPoundsYAxis setRangeWithMinimum:@1050 andMaximum:@1400];

<img src="../../images/chart-axes-numeric001.png">

##Formatting a TKChartNumericAxis##

You can format the axis labels in percentage by setting the <code>formatTicksAsPercents</code> property: 

    gdpInPoundsYAxis.labelDisplayMode = TKChartNumericAxisLabelDisplayModePercentage;

<img src="../../images/chart-axes-numeric002.png">