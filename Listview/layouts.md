---
title: Layouts
page_title: ListView layouts
position: 6
---

# ListView: Layouts

TKListView supports two different layout modes - wrap and columns.

##Wrap layout##
In wrap layout cells are distributed evenly in rows or columns according to the available space, scroll orientation, cell size, minimum inter item spacing and minimum line spacing.

<img src="../images/listview-layouts001.png"/>

```Objective-C

    _listView.insets = UIEdgeInsetsMake(4, 4, 0, 4);
    TKListViewWrapLayout *layout = [TKListViewWrapLayout new];
    layout.minimumLineSpacing = 4;
    layout.minimumInteritemSpacing = 4;
    layout.itemSize = CGSizeMake(100, 100);
    _listView.layout = layout;

```

```Swift

        listView.insets = UIEdgeInsetsMake(4, 4, 0, 4)
        let layout = TKListViewWrapLayout()
        layout.minimumLineSpacing = 4
        layout.minimumInteritemSpacing = 4
        layout.itemSize = CGSizeMake(100, 100)
        listView.layout = layout
        
```

```C#
            
            this.ListView.Insets = new UIEdgeInsets (4, 4, 0, 4);
			TKListViewWrapLayout layout = new TKListViewWrapLayout ();
			layout.MinimumLineSpacing = 4;
			layout.MinimumInteritemSpacing = 4;
			layout.ItemSize = new CGSize (100f, 100f);
			this.ListView.Layout = layout;
```

##Columns layout##
The columns layout allows distributing cells in a fixed columns count and aligning the cells (left, right, center and justify) within the columns.
<img src="../images/listview-layouts002.png"/>

```Objective-C

    _listView.insets = UIEdgeInsetsZero;
    TKListViewColumnsLayout *layout = [TKListViewColumnsLayout new];
    layout.itemSize = CGSizeMake(100, 100);
    layout.columnsCount = 2;
    layout.cellAlignment = TKListViewCellAlignmentCenter;
    _listView.layout = layout;


```

```Swift

        listView.insets = UIEdgeInsetsZero
        let layout = TKListViewColumnsLayout()
        layout.itemSize = CGSizeMake(100, 100)
        layout.columnsCount = 2
        layout.cellAlignment = TKListViewCellAlignment.Center
        listView.layout = layout        
```

```C#
            
            this.ListView.Insets = UIEdgeInsets.Zero;
			TKListViewColumnsLayout layout = new TKListViewColumnsLayout ();
			layout.ItemSize = new CGSize (100f, 100f);
			layout.ColumnsCount = 2;
			layout.CellAlignment = TKListViewCellAlignmentCenter;
			this.ListView.Layout = layout;
```
