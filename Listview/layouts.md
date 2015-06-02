---
title: Layouts
page_title: ListView Layouts
position: 6
---

# ListView: Layouts

TKListView provides the same layout mechanism as UICollectionView. There are three additionally implemented layouts and you can also create your own by inheriting from UICollectionViewLayout class. However, all list view features will be available only when using a layout which inherits from TKListViewLinearLayout.

## Getting started##

By default TKListView will use TKListViewLinearLayout but you can easily change that with the layout property. The layouts that are implemented are:

- Linear - the default layout which orders items in a simple list.
- Grid - lays out items in a grid.
- Staggered - lays out items in a staggered grid formation.

Each of these layouts can layout items in either horizontal or vertical direction. Here is one example of setting grid layout with two columns and horizontall scroll direction.

```Objective-C
TKListViewGridLayout *layout = [TKListViewGridLayout new];
layout.spanCount = 2;
layout.scrollDirection = TKListViewScrollDirectionHorizontal;

listView.layout = layout;
```
```Swift
let layout = TKListViewGridLayout()
layout.spanCount = 2
layout.scrollDirection = TKListViewScrollDirection.Horizontal

listView.layout = layout
```
```C#
var layout = new TKListViewGridLayout ();
layout.SpanCount = 2;
layout.ScrollDirection = TKListViewScrollDirection.Horizontal;

ListView.Layout = layout;
```

## Linear layout##

In linear layout cells are distributed in a simple list horizontally or vertically depending on the selected scroll direction.

<img src="../images/listview-layouts001.png"/>

```Objective-C
TKListViewLinearLayout *layout = [TKListViewLinearLayout new];
layout.itemSpacing = 4;
layout.itemSize = CGSizeMake(100, 100);
listView.layout = layout;
```
```Swift
let layout = TKListViewLinearLayout()
layout.itemSpacing = 4
layout.itemSize = CGSizeMake(100, 100)
listView.layout = layout
```
```C#
var layout = new TKListViewLinearLayout ();
layout.ItemSpacing = 4;
layout.ItemSize = new CGSize (100, 100);
ListView.Layout = layout;
```

Cells can be aligned (left, right, center, stretch) by setting the itemAlignment property:

```Objective-C
layout.itemAlignment = TKListViewItemAlignmentCenter;
```
```Swift
layout.itemAlignment = TKListViewItemAlignment.Center
```
```C#
layout.ItemAlignment = TKListViewItemAlignment.Center;
```

## Grid layout##

The grid layout allows for distributing cells in a fixed number of columns/rows. The grid layout inherits from TKListViewLinearLayout, therefore all properties of TKListViewLinearLayout are also available in TKListViewGridLayout.

<img src="../images/listview-layouts002.png"/>

```Objective-C
TKListViewGridLayout *layout = [TKListViewGridLayout new];
layout.itemSize = CGSizeMake(100, 100);
layout.itemSpacing = 0;
layout.lineSpacing = 0;
layout.spanCount = 2;
listView.layout = layout;
```
```Swift
let layout = TKListViewGridLayout()
layout.itemSize = CGSizeMake(100, 100)
layout.itemSpacing = 0
layout.lineSpacing = 0
layout.spanCount = 2
listView.layout = layout
```
```C#
var layout = new TKListViewGridLayout ();
layout.ItemSize = new CGSize (100, 100);
layout.ItemSpacing = 0;
layout.LineSpacing = 0;
layout.SpanCount = 2;
ListView.Layout = layout;
```

## Staggered layout##

The staggered layout lays out items in a staggered grid formation. It supports horizontal & vertical layout as well as an ability to align cells. It inherits from TKListViewGridLayout. 

<img src="../images/listview-layouts003.png"/>

Staggered layout lays its items based on their size. The item size is determined by using the staggeredLayout:sizeForItemAtIndexPath: method of TKListViewStaggeredLayoutDelegate protocol:

```Objective-C
- (CGSize)staggeredLayout:(TKListViewStaggeredLayout *)layout sizeForItemAtIndexPath:(NSIndexPath *)indexPath
{
    if (layout.scrollDirection == TKListViewScrollDirectionVertical) {
        return CGSizeMake(100, [_sizes[indexPath.row] floatValue]);
    }
    else {
        return CGSizeMake([_sizes[indexPath.row] floatValue], 100);
    }
}
```
```Swift
func staggeredLayout(layout: TKListViewStaggeredLayout!, sizeForItemAtIndexPath indexPath: NSIndexPath!) -> CGSize {
    if layout.scrollDirection == TKListViewScrollDirection.Vertical {
        return CGSizeMake(100, sizes[indexPath.row]);
    }
    else {
        return CGSizeMake(sizes[indexPath.row], 100);
    }
}
```
```C#
public class StaggeredLayoutDelegate: TKListViewStaggeredLayoutDelegate
{
	List<nfloat> sizes = new List<nfloat>();

	public override CGSize SizeForItem (TKListViewStaggeredLayout layout, NSIndexPath indexPath)
	{
		if (layout.ScrollDirection == TKListViewScrollDirection.Vertical) {
			return new CGSize(100, sizes[indexPath.Row]);
		}
		else {
			return new CGSize(sizes[indexPath.Row], 100);
		}
	}
}
```

Staggered grids are likely to have gaps at the edges of the layout. To avoid these gaps, set the alignLastLine property to YES.

```Objective-C
TKListViewStaggeredLayout *layout = [TKListViewStaggeredLayout new];
layout.itemSpacing = 1;
layout.lineSpacing = 1;
layout.spanCount = 2;
layout.alignLastLine = YES;
layout.delegate = self;
listView.layout = layout;
```
```Swift
let layout = TKListViewStaggeredLayout()
layout.itemSpacing = 1
layout.lineSpacing = 1
layout.spanCount = 2
layout.alignLastLine = true
layout.delegate = self
listView.layout = layout
```
```C#
var layout = new TKListViewStaggeredLayout ();
layout.ItemSpacing = 1;
layout.LineSpacing = 1;
layout.SpanCount = 2;
layout.AlignLastLine = true;
layout.Delegate = new StaggeredLayoutDelegate();
ListView.Layout = layout;
```


