---
title: Layouts
page_title: ListView Layouts
position: 6
---

# ListView: Layouts

TKListView supports two different layout modes - wrap and columns.

## Wrap layout##

In wrap layout cells are distributed evenly in rows or columns according to the available space, scroll orientation, cell size, minimum inter item spacing and minimum line spacing.

<img src="../images/listview-layouts001.png"/>

```Objective-C
_listView.contentInset = UIEdgeInsetsMake(4, 4, 0, 4);
TKListViewLinearLayout *layout = [TKListViewLinearLayout new];
layout.itemSpacing = 4;
layout.itemSize = CGSizeMake(100, 100);
_listView.layout = layout;
```
```Swift
listView.contentInset = UIEdgeInsetsMake(4, 4, 0, 4)
let layout = TKListViewLinearLayout()
layout.itemSpacing = 4
layout.itemSize = CGSizeMake(100, 100)
listView.layout = layout
```
```C#
this.ListView.ContentInset = new UIEdgeInsets (4, 4, 0, 4);
TKListViewLinearLayout layout = new TKListViewLinearLayout ();
layout.ItemSpacing = 4;
layout.ItemSize = new CGSize (100f, 100f);
this.ListView.Layout = layout;
```

## Columns layout##

The columns layout allows for distributing cells in a fixed number of columns and aligning the cells (left, right, center and justify) within the columns.

<img src="../images/listview-layouts002.png"/>

```Objective-C
_listView.contentInset = UIEdgeInsetsZero;
TKListViewGridLayout *layout = [TKListViewGridLayout new];
layout.itemSize = CGSizeMake(100, 100);
layout.lineSpacing = 4;
layout.spanCount = 2;
layout.itemAlignment = TKListViewItemAlignmentCenter;
_listView.layout = layout;
```
```Swift
listView.contentInset = UIEdgeInsetsZero
let layout = TKListViewGridLayout()
layout.itemSize = CGSizeMake(100, 100)
layout.lineSpacing = 4
layout.spanCount = 2
layout.itemAlignment = TKListViewItemAlignment.Center
listView.layout = layout        
```
```C#   
this.ListView.ContentInset = UIEdgeInsets.Zero;
TKListViewGridLayout layout = new TKListViewGridLayout ();
layout.ItemSize = new CGSize (100f, 100f);
layout.LineSpacing = 4;
layout.SpanCount = 2;
layout.ItemAlignment = TKListViewItemAlignment.Center;
this.ListView.Layout = layout;
```
