---
title: Load-on-demand
page_title: ListView Load-on-demand
position: 11
---

# ListView: Load-on-demand

There are certain scenarios typically with remote data over the wire where data needs to be loaded continuously on small portions. TKListView can load data on demand.

## Enabling the load-on-demand  ##

To enable the load on demand feature, you shoud set the <code>loadOnDemandMode</code> property to one of the two supported modes <code>TKListViewLoadOnDemandModeAuto</code> or <code>TKListViewLoadOnDemandModeManual</code>.

```Objective-C
listView.loadOnDemandMode = TKListViewLoadOnDemandMode.Auto;
```
```Swift
listView.loadOnDemandMode = TKListViewLoadOnDemandMode.Auto
```
```C#
listView.LoadOnDemandMode = TKListViewLoadOnDemandMode.Auto;
```

When using the auto mode the <code>loadOnDemandBufferSize</code> property defines the number of cells from the bottom of the list view up at which to start requesting data. 

```Objective-C
listView.loadOnDemandBufferSize = 5;
```
```Swift
listView.loadOnDemandBufferSize = 5
```
```C#
listView.LoadOnDemandBufferSize = 5;
```

After setting the desired <code>loadOnDemandMode</code> you should implement the <code>TKListViewDelgate</code> method <code>listView:shouldLoadMoreDataAtIndexPath:</code> to determine if more data should be loaded. After the data is loaded you should notify the ListView by calling its <code>didLoadDataOnDemand</code> method:

```Objective-C
- (BOOL)listView:(TKListView *)listView shouldLoadMoreDataAtIndexPath:(NSIndexPath *)indexPath
{
	// call logic to load more data here. After data is loaded notify the listview
	// by calling [listView didLoadDataOnDemand]; 
	
	//return NO here if no more data is available
    return YES; 
}
```
```Swift
func listView(listView: TKListView!, shouldLoadMoreDataAtIndexPath indexPath: NSIndexPath!) -> Bool {
    // call logic to load more data here. After data is loaded notify the listview
	// by calling listView.didLoadDataOnDemand()
        
	//return false here if no more data is available
	return true 
}
```
```C#
public override bool ShouldLoadMoreDataAtIndexPath (TKListView listView, NSIndexPath indexPath)
{
	// call logic to load more data here. After data is loaded notify the listview
	// by calling listView.DidLoadDataOnDemand();
	
	//return false here if no more data is available
	return true; 
}
```

When using manual mode, TKListView appends a special cell at the end of the list. Touching this cell starts the process of loading more data. In this scenario you should process listView:cellForItemAtIndexPath: method of TKListViewDataSource and check whether this is a "load on demand cell":

```Objective-C
- (TKListViewCell*)listView:(TKListView *)listView cellForItemAtIndexPath:(NSIndexPath *)indexPath
{
    TKListViewCell *cell = [listView dequeueLoadOnDemandCellForIndexPath:indexPath];
    if (cell == nil) {
    	// initialize a regular cell here
    }
    return cell;
}
```
```Swift
func listView(listView: TKListView!, cellForItemAtIndexPath indexPath: NSIndexPath!) -> TKListViewCell! {
    var cell = listView.dequeueLoadOnDemandCellForIndexPath(indexPath)
    if (cell == nil) {
    	// initialize a regular cell here
    }
    return cell
}
```
```C#
public override TKListViewCell CellForItem (TKListView listView, NSIndexPath indexPath)
{
	TKListViewCell cell = listView.DequeueLoadOnDemandCell (indexPath);
	if (cell == null) {
    	// initialize a regular cell here
	}
	return cell;
}
```

You can replace the default "load on demand cell" by registering a new class which inherits from TKListViewLoadOnDemandCell:

```Objective-C
[_listView registerLoadOnDemandCell:[MyCustomLoadOnDemandCell class]];
```
```Swift
listView.registerLoadOnDemandCell(MyCustomLoadOnDemandCell.self)
```
```C#
listView.RegisterLoadOnDemandCell (new ObjCRuntime.Class (typeof(MyCustomLoadOnDemandCell)));
```
