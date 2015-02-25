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
```
```Swift
```
```C#
```

You can specify <code>displayKey</code> and <code>valueKey</code> properties to specify what to display in table view cells:

```Objective-C
```
```Swift
```
```C#
```

In most scenarios this is not enough because the cell appearance should be customized. In this case you can mplement the <code>initCell</code> block from <code>TKDataSourceTableViewSettings</code> class:

```Objective-C
```
```Swift
```
```C#
```

If this is not enough you can create your custom cells by using the <code>createCell</code> block function:

```Objective-C
```
```Swift
```
```C#
```

<code>TKDataSource</code> will take care of everything and no code is necessary if your data is grouped:

<img>

```Objective-C
```
```Swift
```
```C#
```

**UICollectionView**

<img>

<code>TKDataSource</code> integrates well with <code>UICollectionView</code> too. Just set the <code>dataSource</code> property and prepare the collection view:

```Objective-C
```
```Swift
```
```C#
```

Use the collection view settings class and its <code>initCell</code> in case you want to customize the cell appearance:

```Objective-C
```
```Swift
```
```C#
```

**TKListView**

<img>

Just like the build-in <code>UICollectionView</code> it is easy to use <code>TKListView</code> with <code>TKDataSource</code>:

```Objective-C
```
```Swift
```
```C#
```

The <code>initCell</code> and <code>createCell</code> methods can be used to customize the cell appearance:

```Objective-C
```
```Swift
```
```C#
```

**TKChart**

<img>

In order to present data in <code>TKChart</code> you need to set the <code>displayKey</code> and <code>valueKey</code> properties. The <code>displayKey</code> defines the x-axis values, and the <code>valueKey</code> defines the y-axis values:

```Objective-C
```
```Swift
```
```C#
```

In order to present different series the data should be grouped:

```Objective-C
```
```Swift
```
```C#
```

**TKCalendar**

<img>

<code>TKDataSource</code> is able to represent your data as calendar events. In this scenario you should set the <code>startDateKey</code> and <code>endDateKey</code> properties:

```Objective-C
```
```Swift
```
```C#
```

