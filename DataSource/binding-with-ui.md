---
title: Binding with UI Controls
page_title: DataSource Binding with UI Controls
position: 5
---

# DataSource: Binding with UI Controls

<code>TKDataSource</code> works well with data enabled controls and provides an easy way to shape and present your data. The currently supported UI controls are:

- UITableView
- UICollectionView
- TKListView
- TKChart
- TKCalendar

This article will describe how to bind <code>TKDataSource</code> and customize those controls.

**UITableView**

<img>

Setting the <code>dataSource</code> property is enough in order to present data in <code>UITableView</code>. <code>TKDataSource</code> will take care of the implementation of all <code>UITableViewDataSource</code> methods:

```Objective-C
self.dataSource = [[TKDataSource alloc] initWithArray:@[ @10, @5, @12, @13, @7, @44 ]];

UITableView *tableView = [[UITableView alloc] initWithFrame:self.view.bounds];
tableView.autoresizingMask = UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight;
tableView.dataSource = self.dataSource;
[self.view addSubview:tableView];
```
```Swift
self.dataSource = TKDataSource(array: [ 10, 5, 12, 13, 7, 44 ])

let tableView = UITableView(frame: self.view.bounds)
tableView.autoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight;
tableView.dataSource = self.dataSource;
self.view.addSubview(tableView)
```
```C#
this.dataSource = new TKDataSource (array);

UITableView table = new UITableView (this.View.Bounds);
table.AutoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight;
table.DataSource = this.dataSource;
this.View.AddSubview (table);
```

You can specify <code>displayKey</code> and <code>valueKey</code> properties to specify what to display in table view cells:

```Objective-C
NSMutableArray *items = [NSMutableArray new];
[items addObject:[[DataSourceItem alloc] initWithName:@"John" value:50 group:@"A"]];
[items addObject:[[DataSourceItem alloc] initWithName:@"Abby" value:33 group:@"A"]];
[items addObject:[[DataSourceItem alloc] initWithName:@"Smith" value:42 group:@"B"]];
[items addObject:[[DataSourceItem alloc] initWithName:@"Peter" value:28 group:@"B"]];
[items addObject:[[DataSourceItem alloc] initWithName:@"Paula" value:25 group:@"B"]];

self.dataSource.displayKey = @"name";
self.dataSource.valueKey = @"value";
self.dataSource.itemSource = items;
```
```Swift
var items = [DataSourceItem]()
items.append(DataSourceItem(name: "John", value: 50))
items.append(DataSourceItem(name: "Abby", value: 33))
items.append(DataSourceItem(name: "Smith", value: 42))
items.append(DataSourceItem(name: "Peter", value: 28))
items.append(DataSourceItem(name: "Paula", value: 25))

if let dataSource = self.dataSource {
    dataSource.displayKey = "name"
    dataSource.valueKey = "value"
    dataSource.itemSource = items
}
```
```C#
NSMutableArray items = new NSMutableArray ();
items.Add (new DataSourceItem () { Name = "John", Value = 50 });
items.Add (new DataSourceItem () { Name = "Abby", Value = 33 });
items.Add (new DataSourceItem () { Name = "Smith", Value = 42 });
items.Add (new DataSourceItem () { Name = "Peter", Value = 28 });
items.Add (new DataSourceItem () { Name = "Paula", Value = 25 });

this.dataSource.ItemSource = items;
this.dataSource.DisplayKey = "Name";
this.dataSource.ValueKey = "Value";
```

In most scenarios this is not enough because the cell appearance should be customized. In this case you can mplement the <code>initCell</code> block from <code>TKDataSourceTableViewSettings</code> class:

```Objective-C
[self.dataSource.settings.tableView initCell:^(UITableView *tableView, NSIndexPath *indexPath, UITableViewCell *cell, id item) {
    cell.backgroundColor = [UIColor redColor];
}];
```
```Swift
self.dataSource?.settings.tableView .initCell({ (UITableView tableView, NSIndexPath indexPath, UITableViewCell cell, id item) -> Void in
    cell.backgroundColor = UIColor.redColor()
});
```
```C#
this.dataSource.Settings.TableView.InitCell ((UITableView tableView, NSIndexPath indexPath, UITableViewCell cell, NSObject item) => {
	cell.BackgroundColor = UIColor.Red;
});
```

If this is not enough you can create your custom cells by using the <code>createCell</code> block function:

```Objective-C
[self.dataSource.settings.tableView createCell:^UITableViewCell *(UITableView *tableView, NSIndexPath *indexPath, id item) {
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"cell"];
    if (cell == nil) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleValue1 reuseIdentifier:@"cell"];
    }
    return cell;
}];
```
```Swift
self.dataSource?.settings.tableView.createCell { (UITableView tableView, NSIndexPath indexPath, AnyObject item) -> UITableViewCell in
    var cell = tableView.dequeueReusableCellWithIdentifier("cell") as UITableViewCell?
    if cell == nil {
        cell = UITableViewCell(style:UITableViewCellStyle.Value1, reuseIdentifier:"cell")
    }
    return cell!
}
```
```C#
this.dataSource.Settings.TableView.CreateCell ((UITableView tableView, NSIndexPath indexPath, NSObject item) => {
	UITableViewCell cell = tableView.DequeueReusableCell("cell");
	if (cell == null) {
		cell = new UITableViewCell(UITableViewCellStyle.Value1, "cell");
	}
	return cell;
});
```

<code>TKDataSource</code> will take care of everything and no code is necessary even when your data is grouped:

<img>

```Objective-C
[self.dataSource group:^id(id item) {
    return @([item intValue] % 2 == 0);
}];
```
```Swift
self.dataSource?.group({ (NSNumber item) -> AnyObject! in
    return item.intValue % 2 == 0;
})
```
```C#
this.dataSource.Group ((NSObject item) => {
	return NSObject.FromObject(((NSNumber)item).Int32Value % 2 == 0);
});
```

**UICollectionView**

<img>

<code>TKDataSource</code> integrates well with <code>UICollectionView</code> too. Just set the <code>dataSource</code> property and prepare the collection view:

```Objective-C
UICollectionViewFlowLayout *layout = [UICollectionViewFlowLayout new];
layout.itemSize = CGSizeMake(140, 140);

UICollectionView *collectionView = [[UICollectionView alloc] initWithFrame:CGRectInset(self.view.bounds, 10, 10) collectionViewLayout:layout];
collectionView.autoresizingMask = UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight;
collectionView.dataSource = self.dataSource;
collectionView.backgroundColor = [UIColor whiteColor];
[self.view addSubview:collectionView];
```
```Swift
let layout = UICollectionViewFlowLayout()
layout.itemSize = CGSizeMake(140, 140)

let collectionView = UICollectionView(frame:CGRectInset(self.view.bounds, 10, 10), collectionViewLayout:layout)
collectionView.autoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight
collectionView.dataSource = self.dataSource
collectionView.backgroundColor = UIColor.whiteColor()
self.view.addSubview(collectionView)
```
```C#
var layout = new UICollectionViewFlowLayout();
layout.ItemSize = new CGSize (140, 140);

var collectionView = new UICollectionView (this.View.Bounds, layout);
collectionView.AutoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight;
collectionView.DataSource = this.dataSource;
collectionView.BackgroundColor = UIColor.White;
this.View.AddSubview(collectionView);
```

Use the collection view settings class and its <code>initCell</code> in case you want to customize the cell appearance:

```Objective-C
[self.dataSource.settings.collectionView initCell:^(UICollectionView *collectionView, NSIndexPath *indexPath, UICollectionViewCell *cell, id item) {
    TKCollectionViewCell *tkcell = (TKCollectionViewCell*)cell;
    tkcell.label.text = [self.dataSource textFromItem:item inGroup:nil];
}];

//...

[collectionView registerClass:[DSCollectionViewCell class] forCellWithReuseIdentifier:@"cell"];
```
```Swift
self.dataSource?.settings.collectionView.initCell({ (UICollectionView collectionView, NSIndexPath indexPath,
    UICollectionViewCell cell, AnyObject item) -> Void in
    let tkCell = cell as TKCollectionViewCell
    tkCell.label.text = self.dataSource?.textFromItem(item, inGroup: nil)
})

//...

collectionView.registerClass(TKCollectionViewCell.self, forCellWithReuseIdentifier: "cell")
```
```C#
this.dataSource.Settings.CollectionView.InitCell ((UICollectionView collection, NSIndexPath indexPath, UICollectionViewCell cell, NSObject item) => {
	var tkCell = cell as TKCollectionViewCell;
	tkCell.Label.Text = this.dataSource.TextFromItem(item, null);
});

//...

collectionView.RegisterClassForCell (typeof(TKCollectionViewCell), "cell");
```

**TKListView**

<img>

Just like the build-in <code>UICollectionView</code> it is easy to use <code>TKListView</code> with <code>TKDataSource</code>:

```Objective-C
TKListView *listView = [[TKListView alloc] initWithFrame:self.view.bounds];
listView.autoresizingMask = UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight;
listView.dataSource = self.dataSource;
[self.view addSubview:listView];
```
```Swift
let listView = TKListView(frame:self.view.bounds)
listView.autoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight
listView.dataSource = self.dataSource
self.view.addSubview(listView)
```
```C#
var listView = new TKListView (this.View.Bounds);
listView.AutoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight;
this.dataSource.SetDataSourceFor (listView);
this.View.AddSubview (listView);
```

The <code>initCell</code> and <code>createCell</code> methods can be used to customize the cell appearance:

```Objective-C
[self.dataSource.settings.listView createCell:^TKListViewCell *(TKListView *listView, NSIndexPath *indexPath, id item) {
    return [listView dequeueReusableCellWithReuseIdentifier:@"myCustomCell" forIndexPath:indexPath];
}];

[self.dataSource.settings.listView initCell:^(TKListView *listView, NSIndexPath *indexPath, TKListViewCell *cell, id item) {
    cell.textLabel.text = [self.dataSource textFromItem:item inGroup:nil];
    ((TKView*)cell.backgroundView).fill = [TKSolidFill solidFillWithColor:[UIColor yellowColor]];
}];

//...

[listView registerClass:[CustomListViewCell class] forCellWithReuseIdentifier:@"myCustomCell"];
```
```Swift
self.dataSource?.settings.listView.createCell({ (TKListView listView, NSIndexPath indexPath, AnyObject item) -> TKListViewCell! in
    return listView.dequeueReusableCellWithReuseIdentifier("myCustomCell", forIndexPath:indexPath) as TKListViewCell
})

self.dataSource?.settings.listView.initCell({ (TKListView listView, NSIndexPath indexPath, TKListViewCell cell, AnyObject item) -> Void in
    cell.textLabel.text = self.dataSource?.textFromItem(item, inGroup:nil)
    (cell.backgroundView as TKView).fill = TKSolidFill(color: UIColor.yellowColor())
})

//...

listView.registerClass(TKCollectionViewCell.self, forCellWithReuseIdentifier: "cell")
```
```C#
this.dataSource.Settings.ListView.CreateCell ((TKListView list1, NSIndexPath indexPath, NSObject item) => {
	return list1.DequeueReusableCell("myCustomCell", indexPath) as TKListViewCell;
});

this.dataSource.Settings.ListView.InitCell ((TKListView list2, NSIndexPath indexPath, TKListViewCell cell, NSObject item) => {
	cell.TextLabel.Text = this.dataSource.TextFromItem(item, null);
	(cell.BackgroundView as TKView).Fill = new TKSolidFill(UIColor.Yellow);
});

//...

listView.RegisterClassForCell(new ObjCRuntime.Class(typeof(TKCollectionViewCell)), "cell");
```

**TKChart**

<img>

In order to present data in <code>TKChart</code> you need to set the <code>displayKey</code> and <code>valueKey</code> properties. The <code>displayKey</code> defines the x-axis values, and the <code>valueKey</code> defines the y-axis values:

```Objective-C
self.dataSource.displayKey = @"name";
self.dataSource.valueKey = @"value";
self.dataSource.itemSource = items;

TKChart *chart = [[TKChart alloc] initWithFrame:self.view.bounds];
chart.autoresizingMask = UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight;
chart.dataSource = self.dataSource;
[self.view addSubview:chart];
```
```Swift
self.dataSource?.displayKey = "name"
self.dataSource?.valueKey = "value"
self.dataSource?.itemSource = items

let chart = TKChart(frame:self.view.bounds)
chart.autoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight
chart.dataSource = self.dataSource
self.view.addSubview(chart)
```
```C#
this.dataSource.DisplayKey = "name";
this.dataSource.ValueKey = "value";
this.dataSource.ItemSource = items;

var chart = new TKChart(this.View.Bounds);
chart.AutoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight;
chart.DataSource = this.dataSource;
this.View.AddSubview(chart);
```

In order to present different series the data should be grouped. When this is done the <code>createSeries</code> method can be used to customize the series that should be created:

```Objective-C
[self.dataSource.settings.chart createSeries:^TKChartSeries *(TKDataSourceGroup *group) {
    TKChartColumnSeries *series = [TKChartColumnSeries new];
    series.selectionMode = TKChartSeriesSelectionModeDataPoint;
    series.style.paletteMode = TKChartSeriesStylePaletteModeUseItemIndex;
    return series;
}];
```
```Swift
self.dataSource?.settings.chart.createSeries({ (TKDataSourceGroup group) -> TKChartSeries! in
    let series = TKChartColumnSeries()
    series.selectionMode = TKChartSeriesSelectionMode.DataPoint
    series.style.paletteMode = TKChartSeriesStylePaletteMode.UseItemIndex
    return series
})
```
```C#
this.dataSource.Settings.Chart.CreateSeries ((TKDataSourceGroup group) => {
	var series = new TKChartColumnSeries();
	series.SelectionMode = TKChartSeriesSelectionMode.DataPoint;
	series.Style.PaletteMode = TKChartSeriesStylePaletteMode.UseItemIndex;
	return series;
});
```

**TKCalendar**

<img>

<code>TKDataSource</code> is able to represent your data as calendar events. In this scenario you should set the <code>startDateKey</code> and <code>endDateKey</code> properties:

```Objective-C
self.dataSource.settings.calendar.startDateKey = @"startDate";
self.dataSource.settings.calendar.endDateKey = @"endDate";
self.dataSource.settings.calendar.defaultEventColor = [UIColor redColor];

TKCalendar *calendar = [[TKCalendar alloc] initWithFrame:self.view.bounds];
calendar.autoresizingMask = UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight;
calendar.dataSource = self.dataSource;
[self.view addSubview:calendar];
```
```Swift
self.dataSource?.settings.calendar.startDateKey = "startDate"
self.dataSource?.settings.calendar.endDateKey = "endDate"
self.dataSource?.settings.calendar.defaultEventColor = UIColor.redColor()

let calendar = TKCalendar(frame:self.view.bounds)
calendar.autoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight
calendar.dataSource = self.dataSource
self.view.addSubview(calendar)
```
```C#
this.dataSource.Settings.Calendar.StartDateKey = "startDate";
this.dataSource.Settings.Calendar.EndDateKey = "endDate";
this.dataSource.Settings.Calendar.DefaultEventColor = UIColor.Red;

var calendar = new TKCalendar (this.View.Bounds);
calendar.AutoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight;
this.dataSource.SetDataSourceFor (calendar);
this.View.AddSubview (calendar);
```

