---
title: Axes
page_title: Axes Overview
position: 1
---

# Chart Axes: Overview

<code>TKChart</code> renders its points in a coordinate system defined by its axes. To do this, axes specify the minimum and maximum values that can be presented on the plot area. There are a few different types of axes that can be used with <code>TKChart</code>. They include: numeric, date/time and categoric. You can assign each axis to different series and you can show multiple axes in chart. Axes contain various properties to control their position, style and behavior. All chart axes subclass from TKChartAxis.

- Use <code>TKChartNumericAxis</code> to present numeric values.
- Use <code>TKChartDateTimeAxis</code> to present date/time values.
- Use <code>TKChartCategoryAxis</code> to present categoric values.

This article discusses the common characteristics of the abstract class <code>TKChartAxis</code>, which is the single class all <code>TKChart</code> axes derive from. The axes automatically calculate its maximum and minimum properties, based on the incoming data.

## Axes Common Properties##

There are several important properties which allow customization of the behavior and appearance of each axis:

- <code>style</code> - contains a set of properties which define the visual styling of an axis and its labels.

- <code>position</code> - defines where the axis is positioned in relation to the plot area.

- <code>plotMode</code> - defines how the associated series is rendered in relation to the axis.

- <code>allowZoom</code> - allows zooming by this axis.

- <code>zoom</code> - determines the zoom level for this axis.

- <code>allowPan</code> - allows panning by this axis.

- <code>pan</code> - determines the pan level for this axis.

- <code>title</code> - defines the axis title. Note that it sets internally the attributedTitle property.

- <code>attributedTitle</code> - defines the axis attributedTitle, which allows text formatting.

- <code>labelFormat</code> - defines a format string for axis labels.

- <code>labelFormatter</code> - defines a label formatter for axis labels.

- <code>tickCount</code> - returns the count of axis labels.

## Configure Axes Position##

You can change the axis position by setting its position property to one of the following values:
<code>TKChartAxisPositionLeft</code>, <code>TKChartAxisPositionRight</code>, <code>TKChartAxisPositionTop</code> and <code>TKChartAxisPositionBottom</code>.

The following lines of code demonstrate how you can create multiple axes at different positions:

```Objective-C
TKChartNumericAxis *gdpInPoundsYAxis = [[TKChartNumericAxis alloc] initWithMinimum:@1050 andMaximum:@1400];
gdpInPoundsYAxis.position = TKChartAxisPositionLeft;
[chart addAxis:gdpInPoundsYAxis];

TKChartNumericAxis *gdpInvestmentYAxis = [[TKChartNumericAxis alloc] initWithMinimum:@0 andMaximum:@20];
gdpInvestmentYAxis.position = TKChartAxisPositionRight;
[chart addAxis:gdpInvestmentYAxis];
```
```Swift
let gdpInPoundsYAxis = TKChartNumericAxis(minimum: 1050, andMaximum: 1400)
gdpInPoundsYAxis.position = TKChartAxisPosition.Left
chart.addAxis(gdpInPoundsYAxis)
    
let gdpInvestmentYAxis = TKChartNumericAxis(minimum: 0, andMaximum: 20)
gdpInvestmentYAxis.position = TKChartAxisPosition.Right
chart.addAxis(gdpInvestmentYAxis)
```
```C#
var gdpInPoundsYAxis = new TKChartNumericAxis (new NSNumber(1050), new NSNumber(1400));
gdpInPoundsYAxis.Position = TKChartAxisPosition.Left;
chart.AddAxis (gdpInPoundsYAxis);

var gdpInvestmentYAxis = new TKChartNumericAxis(new NSNumber(0), new NSNumber(20));
gdpInvestmentYAxis.Position = TKChartAxisPosition.Right;
chart.AddAxis (gdpInvestmentYAxis);
```

<img src="../../images/chart-axes-types009.png"/>

## Configure Axes Appearance##

You can customize any feature of the axis appearance. If you want to hide its line or change its line stroke or background, you can use the following peace of code:

```Objective-C
xAxis.style.lineStroke = [TKStroke strokeWithColor:[UIColor blueColor]];
xAxis.style.backgroundFill = [TKSolidFill solidFillWithColor:[UIColor lightGrayColor]];
```
```Swift
xAxis.style.lineStroke = TKStroke(color: UIColor.blueColor())
xAxis.style.backgroundFill = TKSolidFill(color: UIColor.lightGrayColor())
```
```C#
xAxis.Style.LineStroke = new TKStroke (UIColor.Blue);
xAxis.Style.BackgroundFill = new TKSolidFill (UIColor.LightGray);
```

<img src="../../images/chart-axes-types001.png"/>

## Configure Axes Ticks Appearance##

In numeric/date-time axes you can specify the interval between axis ticks by setting the <code>majorTickInterval</code> and <code>minorTickInterval</code> properties:

```Objective-C
TKChartNumericAxis *yAxis = (TKChartNumericAxis*)chart.yAxis;
yAxis.majorTickInterval = 20;
yAxis.minorTickInterval = 3;
yAxis.style.majorTickStyle.ticksHidden = NO;
```
```Swift
let yAxis = chart.yAxis as! TKChartNumericAxis
yAxis.majorTickInterval = 20
yAxis.minorTickInterval = 3
yAxis.style.majorTickStyle.ticksHidden = false
```
```C#
var yAxis = chart.YAxis as TKChartNumericAxis;
yAxis.MajorTickInterval = 20;
yAxis.MinorTickInterval = 3;
yAxis.Style.MajorTickStyle.TicksHidden = false;
```

<img src="../../images/chart-axes-types008.png"/>

You can customize the major and minor ticks of axis by manipulating the <code>majorTickStyle</code> and <code>minorTickStyle</code> properties.

```Objective-C
xAxis.style.minorTickStyle.ticksHidden = NO;
xAxis.style.majorTickStyle.ticksStroke = [TKStroke strokeWithColor:[UIColor blueColor]];
xAxis.style.majorTickStyle.ticksLength = 10;
xAxis.style.majorTickStyle.ticksWidth = 1;
xAxis.style.majorTickStyle.ticksOffset = 5;
```
```Swift
xAxis.style.majorTickStyle.ticksHidden = false
xAxis.style.majorTickStyle.ticksStroke = TKStroke(color: UIColor.blueColor())
xAxis.style.majorTickStyle.ticksLength = 10
xAxis.style.majorTickStyle.ticksWidth = 1
xAxis.style.majorTickStyle.ticksOffset = 5
```
```C#
xAxis.Style.MajorTickStyle.TicksHidden = false;
xAxis.Style.MajorTickStyle.TicksStroke = new TKStroke (UIColor.Blue);
xAxis.Style.MajorTickStyle.TicksLength = 10;
xAxis.Style.MajorTickStyle.TicksWidth = 1;
xAxis.Style.MajorTickStyle.TicksOffset = 5;
```

<img src="../../images/chart-axes-types002.png"/>

In addition to the common tick style customizations, you can specify the first and last ticks visibility by setting <code>minTickClippingMode</code> and <code>maxTickClippingMode</code> properties:

```Objective-C
xAxis.style.majorTickStyle.minTickClippingMode = TKChartAxisClippingMode.Hidden;
xAxis.style.majorTickStyle.maxTickClippingMode = TKChartAxisClippingMode.Visible;
```
```Swift
xAxis.style.majorTickStyle.minTickClippingMode = TKChartAxisClippingModeHidden
xAxis.style.majorTickStyle.maxTickClippingMode = TKChartAxisClippingModeVisible
```
```C#
xAxis.Style.MajorTickStyle.MinTickClippingMode = TKChartAxisClippingMode.Hidden;
xAxis.Style.MajorTickStyle.MaxTickClippingMode = TKChartAxisClippingMode.Visible;
```

<img src="../../images/chart-axes-types003.png"/>

## Configure Axes Label Appearance##

You can configure the axis label appearance by manipulating the <code>labelStyle</code> property of the axis style object. If you want to change the font, text color, shadow color and offset, you should modify the corresponding properties:

```Objective-C
xAxis.style.labelStyle.font = [UIFont boldSystemFontOfSize:10];
xAxis.style.labelStyle.textColor = [UIColor blueColor];
xAxis.style.labelStyle.shadowColor = [UIColor grayColor];
xAxis.style.labelStyle.shadowOffset = CGSizeMake(1, 1);
[chart reloadData];
```
```Swift
xAxis.style.labelStyle.font = UIFont.systemFontOfSize(10)
xAxis.style.labelStyle.textColor = UIColor.blueColor()
xAxis.style.labelStyle.shadowColor = UIColor.grayColor()
xAxis.style.labelStyle.shadowOffset = CGSizeMake(1, 1)
chart.reloadData()
```
```C#
xAxis.Style.LabelStyle.Font = UIFont.SystemFontOfSize (10);
xAxis.Style.LabelStyle.TextColor = UIColor.Blue;
xAxis.Style.LabelStyle.ShadowColor = UIColor.Gray;
xAxis.Style.LabelStyle.ShadowOffset = new CGSize (1f, 1f);
chart.ReloadData ();
```

You can define the label offset and alignment by setting the <code>textOffset</code> and <code>textAlignment</code> properties:

```Objective-C
xAxis.style.labelStyle.textAlignment = TKChartAxisLabelAlignmentBottom;
xAxis.style.labelStyle.firstLabelTextAlignment = TKChartAxisLabelAlignmentBottom;
xAxis.style.labelStyle.textOffset = UIOffsetMake(10, 50);
xAxis.style.labelStyle.firstLabelTextOffset = UIOffsetMake(10, 50);
[chart reloadData];
```
```Swift
xAxis.style.labelStyle.textAlignment = TKChartAxisLabelAlignment.Bottom
xAxis.style.labelStyle.firstLabelTextAlignment = TKChartAxisLabelAlignment.Bottom
xAxis.style.labelStyle.textOffset = UIOffsetMake(10, 50)
xAxis.style.labelStyle.firstLabelTextOffset = UIOffsetMake(10, 50)
chart.reloadData()
```
```C#
xAxis.Style.LabelStyle.TextAlignment = TKChartAxisLabelAlignment.Bottom;
xAxis.Style.LabelStyle.FirstLabelTextAlignment = TKChartAxisLabelAlignment.Bottom;
xAxis.Style.LabelStyle.TextOffset = new UIOffset(10, 50);
xAxis.Style.LabelStyle.FirstLabelTextOffset = new UIOffset(10, 50);
chart.ReloadData();
```

<img src="../../images/chart-axes-types004.png"/>

You can change the label fitting mode in the following manner:

```Objective-C
xAxis.style.labelStyle.fitMode = TKChartAxisLabelFitModeNone;
```
```Swift
xAxis.style.labelStyle.fitMode = TKChartAxisLabelFitMode.None
```
```C#
xAxis.Style.LabelStyle.FitMode = TKChartAxisLabelFitMode.None;
```

<img src="../../images/chart-axes-types005.png"/>

```Objective-C
xAxis.style.labelStyle.fitMode = TKChartAxisLabelFitModeMultiline;
```
```Swift
xAxis.style.labelStyle.fitMode = TKChartAxisLabelFitMode.Multiline
```
```C#
xAxis.Style.LabelStyle.FitMode = TKChartAxisLabelFitMode.Multiline;
```

<img src="../../images/chart-axes-types006.png"/>

## Configure Axes Title Appearance

In order to change the change the axis title font, text color, shadow color, alignment and offset, you should modify the corresponding properties:

```Objective-C
xAxis.title = @"X-Axis";
xAxis.style.titleStyle.textColor = [UIColor blueColor];
xAxis.style.titleStyle.font = [UIFont boldSystemFontOfSize:11];
xAxis.style.titleStyle.shadowColor = [UIColor grayColor];
xAxis.style.titleStyle.shadowOffset = CGSizeMake(2, 2);
xAxis.style.titleStyle.alignment = TKChartAxisTitleAlignmentRightOrBottom;
[chart reloadData];
```
```Swift
xAxis.title = "X-Axis"
xAxis.style.titleStyle.textColor = UIColor.blueColor()
xAxis.style.titleStyle.font = UIFont.boldSystemFontOfSize(11)
xAxis.style.titleStyle.shadowColor = UIColor.grayColor()
xAxis.style.titleStyle.shadowOffset = CGSizeMake(2, 2)
xAxis.style.titleStyle.alignment = TKChartAxisTitleAlignment.RightOrBottom
chart.reloadData()
```
```C#
xAxis.Title = "X-Axis";
xAxis.Style.TitleStyle.TextColor = UIColor.Blue;
xAxis.Style.TitleStyle.Font = UIFont.BoldSystemFontOfSize (11);
xAxis.Style.TitleStyle.ShadowColor = UIColor.Gray;
xAxis.Style.TitleStyle.ShadowOffset = new CGSize (2f, 2f);
xAxis.Style.TitleStyle.Alignment = TKChartAxisTitleAlignment.RightOrBottom;
chart.ReloadData ();
```

<img src="../../images/chart-axes-types007.png"/>

## Axes Types

Any Cartesian series supports the following axes:

- [TKChartNumericAxis](numeric)
- [TKChartCategoryAxis](categoric)
- [TKChartDateTimeAxis](datetime)

@warning Note that Pie area does not support axes.



