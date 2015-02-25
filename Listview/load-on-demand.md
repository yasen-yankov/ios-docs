---
title: Load on demand
page_title: ListView load on demand
position: 11
---

# ListView: Load on demand

There are certain scenarios typically with remote data over the wire where data needs to be loaded continuously on small portions. TKListView may load data on demand.




## Enabling the feature  ##

To enable the load on demand feature you shoud set the <code>cellBufferSize</code> property. This property defines the number of cells from the bottom of the ListView up at which to start requestion data.

```Objective-C
listView.cellBufferSize = 5;
```

```Swift
listView.cellBufferSize = 5
```

```C#
listView.CellBufferSize = 5;
```

After a cell buffer size is set you should implement <code>TKListViewDelgate</code> method <code>listView:shouldLoadMoreDataAtIndexPath:</code> to determine if more data shoude be loaded. After the data is loaded you should notify the ListView by calling its <code>didLoadDataOnDemand</code> method.

```Objective-C
- (BOOL)listView:(TKListView *)listView shouldLoadMoreDataAtIndexPath:(NSIndexPath *)indexPath
{
	// call logic to load more data here. After data is loaded notify the listview
	// by calling     [listView didLoadDataOnDemand]; 
	

    return YES; //return NO here if no more data is available.
}
```

```Swift
func listView(listView: TKListView!, shouldLoadMoreDataAtIndexPath indexPath: NSIndexPath!) -> Bool {

    // call logic to load more data here. After data is loaded notify the listview
	// by calling     listView.didLoadDataOnDemand()
        
        return true //return false here if no more data is available.
    }
```

```C#
public override bool ShouldLoadMoreDataAtIndexPath (TKListView listView, NSIndexPath indexPath)
{
	// call logic to load more data here. After data is loaded notify the listview
	// by calling     listView.DidLoadDataOnDemand();
	
	return true; //return false here if no more data is available.
}
```