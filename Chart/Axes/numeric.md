---
title: Numeric
page_title: Numeric Axis
position: 4
---

# Chart Animations: Custom Animations

<code>TKChart</code> uses Linear axes to plot data containing numerical values. It is valid only in the context of Cartesian Area, this axis is created by default when you add Bar, Line, Area and Scatter series. It also introduces several important properties:

- <code>majorTickInterval</code> - defines the interval between major axis ticks.
- <code>minorTickInterval</code> - defines the interval between minor axis ticks.
- <code>baseline</code> - defines how the series data should be aligned. For example, The TKChartBarSeries might render its bars up and down side depending on whether its value is greater or less than the baseline value.
- <code>offset</code> - Determines an axis value where the axis is crossed with another axis.

## Configure a TKChartNumericAxis##

You can configure a numeric axis by initializing it and setting it as the main x-axis or y-axis of the chart:

```Objective-C
TKChartNumericAxis *yAxis = [[TKChartNumericAxis alloc] init];
chart.yAxis = yAxis;
```
```Swift
let yAxis = TKChartNumericAxis()
chart.yAxis = yAxis;
```
```C#
var yAxis = new TKChartNumericAxis ();
chart.YAxis = yAxis;
```

You can specify the axis range by setting the minimum and maximum indexes of categories:

```Objective-C
yAxis.range = [TKRange rangeWithMinimum:@0 andMaximum:@100];
yAxis.majorTickInterval = @25;
```
```Swift
yAxis.range = TKRange(minimum: 0, andMaximum: 100)
yAxis.majorTickInterval = 25
```
```C#
yAxis.Range = new TKRange (new NSNumber(0), new NSNumber(100));
yAxis.MajorTickInterval = 25;
```

<img src="../../images/chart-axes-numeric001.png">

## Formatting a TKChartNumericAxis##

You can format the axis labels in percentage by setting the <code>formatTicksAsPercents</code> property:

```Objective-C
yAxis.labelDisplayMode = TKChartNumericAxisLabelDisplayModePercentage;
```
```Swift
yAxis.labelDisplayMode = TKChartNumericAxisLabelDisplayMode.Percentage
```
```C#
yAxis.LabelDisplayMode = TKChartNumericAxisLabelDisplayMode.Percentage;
```

<img src="../../images/chart-axes-numeric002.png">
