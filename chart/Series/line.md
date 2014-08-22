---
title: Line
page_title: Line Series
position: 4
---

# Chart Series: Line

<code>TKChartLineSeries</code> plot their data points on Cartesian Area. Points are connected with straight lines. Here is how to set up two line series:

	TKChartLineSeries* seriesForExpenses = [[TKChartLineSeries alloc] initWithItems:expensesData];
	seriesForExpenses.title = @"Expenses";
	[chart addSeries:seriesForExpenses];

	TKChartLineSeries* seriesForIncomes = [[TKChartLineSeries alloc] initWithItems:incomesData];
	seriesForIncomes.title = @"Incomes";
	[chart addSeries:seriesForIncomes];

	TKChartLineSeries* seriesForProfit = [[TKChartLineSeries alloc] initWithItems:profitData];
	seriesForProfit.title = @"Profit";
	[chart addSeries:seriesForProfit];

<img src="../../images/chart-series-line001.png"/>

## Configure input and selection of line series

If you would like to configure the distance between finger touch and line to perform selection:

	TKChartLineSeries* seriesForProfit = [[TKChartLineSeries alloc] initWithItems:profitData];
	seriesForProfit.marginForHitDetection = 30.f;
	[chart addSeries:seriesForProfit];

If you would like to change the series' stroke, you should use the following code snippet:

	TKChartLineSeries* seriesForSales = [[TKChartLineSeries alloc] initWithItems:salesData];
	seriesForSales.style.palette = [[TKChartPalette alloc] init];
	TKChartPaletteItem *palleteItem = [[TKChartPaletteItem alloc] init];
	palleteItem.stroke = [TKStroke strokeWithColor:[UIColor greenColor]];
	[chart addSeries:seriesForSales];

<img src="../../images/chart-series-line003.png"/>
