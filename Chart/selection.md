---
title: Selection
position: 11
---

# Chart: Selection

This help topic demonstrates how you can make your charts more interactive by enabling a selection behavior.

## Configure ##

You can alter the selection mode for each series by altering the series <code>selectionMode</code> property with the following value:

- TKChartSeriesSelectionModeNone - No selection
- TKChartSeriesSelectionModeSeries - Select a whole series
- TKChartSeriesSelectionModeDataPoint - Select a data point

In addition you can choose between single and multiple item selection by altering the chart <code>selectionMode</code> property:

- TKChartSelectionModeSingle - a single point/series can be selected
- TKChartSelectionModeMultiple - multiple points/series can be selected

Use the <code>selectedSeries</code> and <code>selectedPoints</code> properties to get currently selected series or points respectively.

```Objective-C
for (TKChartSeries *series in chart.selectedSeries) {
    NSLog(@"selected series at index: %d", series.index);
}

for (TKChartSelectionInfo *info in chart.selectedPoints) {
    NSLog(@"selected point at index %d from series %d", info.dataPointIndex, info.series.index);
}
```
```Swift
for series in chart.selectedSeries() as! [TKChartSeries] {
    println("selected series at index: \(series.index)")
}

for info in chart.selectedPoints() as! [TKChartSelectionInfo] {
    NSLog("selected point at index \(info.dataPointIndex) from series \(info.series.index)")
}
```
```C#
foreach (TKChartSeries series in chart.SelectedSeries) {
	Console.WriteLine ("selected series at index {0}", series.Index);
}

foreach (TKChartSelectionInfo info in chart.SelectedPoints) {
	Console.WriteLine ("selected point at index {0} from series {1}", info.DataPointIndex, info.Series.Index);
}
```

The <code>isSelected</code> property of TKChartSeries indicates whether the series is selected.

You can determine whether a selection is changed by adopting <code>TKChartDelegate</code> protocol and implementing one the following methods:

```Objective-C
- (void)chart:(TKChart *)chart didSelectSeries:(TKChartSeries *)series
{
    // Here you can perform the desired action when the selection is changed.
}

- (void)chart:(TKChart *)chart didSelectPoint:(id<TKChartData>)point inSeries:(TKChartSeries *)series atIndex:(NSInteger)index
{
    // Here you can perform the desired action when the selection is changed.
}

- (void)chart:(TKChart *)chart didDeselectSeries:(TKChartSeries *)series
{
    // Here you can perform the desired action when the selection is changed.
}

- (void)chart:(TKChart *)chart didDeselectPoint:(id<TKChartData>)point inSeries:(TKChartSeries *)series atIndex:(NSInteger)index
{
    // Here you can perform the desired action when the selection is changed.
}
```
```Swift
func chart(chart: TKChart!, didSelectSeries series: TKChartSeries!) {
    // Here you can perform the desired action when the selection is changed.
}

func chart(chart: TKChart!, didSelectPoint point: TKChartData!, inSeries series: TKChartSeries!, atIndex index: Int) {
    // Here you can perform the desired action when the selection is changed.
}

func chart(chart: TKChart!, didDeselectSeries series: TKChartSeries!) {
    // Here you can perform the desired action when the selection is changed.
}

func chart(chart: TKChart!, didDeselectPoint point: TKChartData!, inSeries series: TKChartSeries!, atIndex index: Int) {
    // Here you can perform the desired action when the selection is changed.
}
```
```C#
class ChartDelegate: TKChartDelegate
{
	public override void SeriesSelected (TKChart chart, TKChartSeries series)
	{
		// Here you can perform the desired action when the selection is changed.
	}

	public override void PointSelected (TKChart chart, TKChartData point, TKChartSeries series, nint index)
	{
		// Here you can perform the desired action when the selection is changed.
	}

	public override void SeriesDeselected (TKChart chart, TKChartSeries series)
	{
		// Here you can perform the desired action when the selection is changed.
	}

	public override void PointDeselected (TKChart chart, TKChartData point, TKChartSeries series, nint index)
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
    chart.select(TKChartSelectionInfo(series: chart.series()[0] as! TKChartSeries, dataPointIndex: 0))
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

Note that you can clear the selection by passing *nil* value to the <code>series</code> argument.


