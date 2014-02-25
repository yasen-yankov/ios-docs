---
title: Pie
meta_title: Pie Series
slug: chart-series-pie
tags: Chart, iOS, pie, series
publish: true
ordinal: 5
---

# Chart Series: Pie

Unlike all other series, <code>TKChartPieSeries</code> do not require axes. They visualize each data point as pie slices with arc size directly proportional to the magnitude of the raw data point's value. Pie slices represent data in one direction contrasting with the other series which represent data in two dimensions. Here is an example of how to create a pie chart with pie series populated with data:

    NSMutableArray *array = [[NSMutableArray alloc] init];
    [array addObject:[[TKChartDataPoint alloc] initWithValue:@20 name:@"Google"]];
    [array addObject:[[TKChartDataPoint alloc] initWithValue:@30 name:@"Apple"]];
    [array addObject:[[TKChartDataPoint alloc] initWithValue:@10 name:@"Microsoft"]];
    [array addObject:[[TKChartDataPoint alloc] initWithValue:@5 name:@"IBM"]];
    [array addObject:[[TKChartDataPoint alloc] initWithValue:@8 name:@"Oracle"]];
    
    TKChartPieSeries *series = [[TKChartPieSeries alloc] init];
    [chart addSeries:series withItems:array];

<img src="../images/chart-series-pie001.png"/>

##Configure visual appearance of pie series

Pie series can be customized using the following properties:

The <code>labelDisplayMode</code> property controls whether to show labels and the label style. The possible choices are: 

- <code>TKChartPieSeriesLabelDisplayModeName</code> - labels show the slice value.
- <code>TKChartPieSeriesLabelDisplayModePercentage</code> - labels show the slice value in percentage.
- <code>TKChartPieSeriesLabelDisplayModeName</code> - labels show the slice name.

Another interesting options that can be used to customize pie labels are <code>labelFormat</code> and <code>labelFormatter</code> properties. For example, you can use the <code>labelFormatter</code> property in order to format labels as percents:

    NSNumberFormatter *numberFormatter = [[NSNumberFormatter alloc] init];
    [numberFormatter setPositiveFormat:@"0.%;0.%;-0.%"];
    series.labelFormatter = numberFormatter;
    
The same can be done also with the labelFormat property:

    series.labelFormat = @"%.0f %%";

<img src="../images/chart-series-pie002.png"/>

The <code>outerRadius</code> property can increase and decrease the diameter of the series. By default, it occupies the whole plot area and is equal to 1. Setting the outerRadius to 0.9 will decrease the radius of the series by 10 percent. Similarly, the value 1.1 will increase it. Leaving the property with value 1 will make the donut fill the available space.

The <code>innerRadius</code> property is measured in the same way a the <code>outerRadius</code> By default, its value is 0. Setting a 0.5 value will produce a donut.

    series.innerRadius = 0.5;
	
<img src="../images/chart-series-pie003.png"/>

The <code>expandRadius</code> property is used when selecting a pie segment. It defines the extent to which the selected pie segment is shifted. Again, this property is measured in percents. A value of 1.1 defines that the selected segment will expand by 10% of the pie radius.

The <code>startAngle</code> and <code>endAngle</code> properties are used to define the pie range. The <code>startAngle</code> sets the angle in radians from which the drawing of the pie segments will begin. Its default value is 0. The <code>endAngle</code> determines whether the chart will appear as a full circle or a partial circle. Its default value is Pi*2.

The following code sets the startAngle and endAngle properties to show a half circle:

    series.startAngle = - M_PI_4/2;
    series.endAngle = M_PI + M_PI_4/2;
    series.rotationAngle = M_PI;
	
<img src="../images/chart-series-pie004.png"/>

By default, the pie chart starts drawing its segments from 0 radians. You can customize this angle and rotate the chart. This is done by setting the <code>rotationAngle</code> property.

The <code>selectionAngle</code> property is used to rotate the chart when selecting a pie segment. It rotates the chart so that the selected pie segment appears at the specified by the property angle.

In order to select the second pie segment, call the select method of TKChart:

 	[chart select:[[TKChartSelectionInfo alloc] initWithSeries:chart.series[0] dataPointIndex:1]];
 	
Further information about selection in chart is available in this [help article](../selection).
