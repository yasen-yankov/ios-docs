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

	- (void)chart:(TKChart *)chart selectedSeries:(TKChartSeries *)series dataPoint:(id<TKChartData>)dataPoint dataIndex:(NSInteger)dataIndex
	{
		// Here you can perform the desired action when the selection is changed.
	}

In addition, you can change the selection programmatically by calling the <code>select</code> method in the following manner:

	series.selectionMode = TKChartSelectionModeDataPoint;

	- (void)viewDidAppear:(BOOL)animated
	{
    	[super viewDidAppear:animated];
    	[_pieChart select:[[TKChartSelectionInfo alloc] initWithSeries:_pieChart.series[0] dataPointIndex:0]];
	}

<img src="../images/chart-selection001.png"/>

Note that you can clear the selection by passing *nil* value.
