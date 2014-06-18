---
title: Datetime
meta_title: Datetime Axis
slug: chart-axes-datetime
tags: Chart, iOS, axis, axes, datetime
publish: true
ordinal: 3
---

# Chart Axes: Datetime

The <code>TKChartDateTimeAxis</code> Categoric axis is an axis with NSDate values sorted chronologically. It also allows definitions of categories based on specific date time components – year, month, day etc. For example, if data values fall in the range of one year, the points can be plotted in categories for each month. If data values fall in the range of one month, the values can be categorized by days. It also introduces several important properties:

- <code>majorTickInterval</code> - defines an interval between major axis ticks.

- <code>baseline</code> - defines how the series data should be aligned. For example: The <code>TKChartBarSeries</code> might render its bars up and down depending on whether its value is greater or less than the baseline value.

- <code>offset</code> - determines an axis value where the axis is crossed with another axis.

##Configure a TKChartDateTimeAxis##

You can configure a date-time axis by initializing it and setting it as the main x-axis or y-axis of the chart:

  	TKChartDateTimeAxis *periodXAxis = [[TKChartDateTimeAxis alloc] init];
  	chart.xAxis = periodXAxis;

You can specify the axis range by setting the minimum and maximum indexes of categories:

	+ (NSDate *)dateWithYear:(NSInteger)year month:(NSInteger)month day:(NSInteger)day {
    	NSCalendar *calendar = [[NSCalendar alloc] initWithCalendarIdentifier:NSGregorianCalendar];
    	NSDateComponents *components = [[NSDateComponents alloc] init];
    	[components setYear:year];
    	[components setMonth:month];
    	[components setDay:day];
    	return [calendar dateFromComponents:components];
	}

	NSDate *date2001 = [MultipleAxes dateWithYear:2001 month:12 day:31];
    NSDate *date2003 = [MultipleAxes dateWithYear:2003 month:12 day:31];

    [periodXAxis setRangeWithMinimum:date2001 andMaximum:date2003];

You can define the axis categories to be years by changing the interval unit property:

     periodXAxis.interval.unit = TKChartDateTimeAxisIntervalUnitYears;

<img src="../../images/chart-axes-datetime001.png">

##Setting a plotting mode of axis##

 The <code>TKChartAxisPlotMode</code> is used by the axis to plot the data. Possible values are <code>TKChartAxisPlotModeBetweenTicks</code> and <code>TKChartAxisPlotModeOnTicks</code>. <code>TKChartAxisPlotModeBetweenTicks</code> plots points in the middle of the range, defined by two ticks. <code>OnTicks</code> plots the points over each tick. 

 You should use the following lines of code to alter this behavior:

	xAxis.plotMode = TKChartAxisPlotModeBetweenTicks;

<img src="../../images/chart-axes-datetime002.png"/>

	xAxis.plotMode = TKChartAxisPlotModeOnTicks;

<img src="../../images/chart-axes-datetime003.png"/>