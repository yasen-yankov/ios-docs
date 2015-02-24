---
title: Selection
page_title: ListView selection
position: 2
---

# ListView: Selection

TKListView supports different selection modes and two different gestures to trigger cell selection. Those include:

- Single selection
- Multiple selection
- Selection on press.
- Selection on hold (long press).

Additionaly TKListView provides a few methods to programatically control selection state as well as delegate methods to react to user interactions related to selection.

This article describes the selection API of TKListView in details.

The <code>allowsMultipleSelection</code> property of <code>TKListView</code> allows defines whether the user is allowed to select multiple items at the same time. It also affects the default appearance of selected items.

## Single seletion mode ##

<img src="../images/listview-selection001.png"/>

The default value of the <code>allowsMultipleSelection</code> property is <code>NO (false)</code> 

```Objective-C
	_listView.allowsMultipleSelection = NO;
```
```Swift
	listView.allowsMultipleSelection = false
```



## Multiple selection mode##

<img src="../images/listview-selection002.png"/>

Set the <code>allowsMultipleSelection</code> property to <code>YES (true)</code> to enable this view:

```Objective-C
_listView.allowsMultipleSelection = YES;
```
```Swift
	listView.allowsMultipleSelection = true	
```

## Selection on press##

By default TKListView will allow user to select on press.

```Objective-C
    _listView.selectionBehavior = TKListViewSelectionBehaviorPress;
```
```Swift
	listView.selectionBehavior = TKListViewSelectionBehavior.Press
```

## Selection on hold (long press)##

In this mode a long-press gesture is required in order to select a cell.

```Objective-C
	_listView.selectionBehavior = TKListViewSelectionBehaviorLongPress;
```
```Swift
	listView.selectionBehavior = TKListViewSelectionBehavior.LongPress
```
## Disable selection##
In order to disable selection you need to set the <code>_listView.selectionBehavior</code> property to  <code>TKListViewSelectionBehaviorNone</code>
```Objective-C
    _listView.selectionBehavior = TKListViewSelectionBehaviorNone;
```
```Swift
	listView.selectionBehavior = TKListViewSelectionBehavior.None
```
