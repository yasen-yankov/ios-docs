---
title: Selection
position: 7
---

# Chart: Selection

This help topic demonstrates how you can make your charts more interactive by enabling a selection behavior.

## Configure##

You can alter the selection mode for each series by altering its <code>selectionMode</code> property with the following value:

- <code>TKChartSelectionModeNone</code> - No selection
- <code>TKChartSelectionModeSeries</code> - Select a whole series
- <code>TKChartSelectionModeDataPoint</code> - Select a data point

You can determine whether a selection is changed by implementing <code>TKChartDelegate</code> protocol:

```Objective-C
- (void)chart:(TKChart *)chart selectedSeries:(TKChartSeries *)series dataPoint:(id<TKChartData>)dataPoint dataIndex:(NSInteger)dataIndex
{
	// Here you can perform the desired action when the selection is changed.
}
```
```Swift
func chart(chart: TKChart!, selectedSeries series: TKChartSeries!, dataPoint: TKChartData!, dataIndex: Int) {
    // Here you can perform the desired action when the selection is changed.
}
```
```C#
class ChartDelegate: TKChartDelegate
{
	public override void SelectedSeries (TKChart chart, TKChartSeries series, TKChartData dataPoint, int dataIndex)
	{
		// Here you can perform the desired action when the selection is changed.
	}
}
```

In addition, you can change the selection programmatically by calling the <code>select</code> method in the following manner:

```Objective-C
series.selectionMode = TKChartSeriesSelectionModeDataPoint;
series.expandRadius = 1.2;

- (void)viewDidAppear:(BOOL)animated
{
	[super viewDidAppear:animated];
	[_pieChart select:[[TKChartSelectionInfo alloc] initWithSeries:_pieChart.series[0] dataPointIndex:0]];
}
```
```Swift
series.selectionMode = TKChartSeriesSelectionModeDataPoint
series.expandRadius = 1.2

override func viewDidAppear(animated: Bool) {
    super.viewDidAppear(animated)
    chart.select(TKChartSelectionInfo(series: chart.series()[0] as TKChartSeries, dataPointIndex: 0))
}
```
```C#
series.SelectionMode = TKChartSeriesSelectionMode.DataPoint;
series.ExpandRadius = 1.2f;

public override void ViewDidAppear (bool animated)
{
	base.ViewDidAppear (animated);
	chart.SelectItem (new TKChartSelectionInfo (chart.Series [0], 0));
}
```

<img src="../images/chart-selection001.png"/>

Note that you can clear the selection by passing *nil* value.

<code>TKChart</code> also provides a method that returns an array containing the selected series. Consider the following code snippet:
```Objective-C
NSArray *selectedSeries = [chart selectedSeries];
```
```Swift
var selectedSeries = chart.selectedSeries();
```
```C#
var selectedSeries = chart.SelectedSeries();
```


