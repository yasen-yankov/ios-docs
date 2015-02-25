---
title: Reordering
page_title: ListView reordering
position: 8
---

# ListView: Reordering

TKListView supports cells reordering. When reordering is enabled a drag handle appears in each cell. Using this handle cells can be dragged thus changing the order of items.
<screenshot>
## Enable cell reorder ##
Use the <code>allowsCellReorder</code> property to enable user to reorder cells. When reordering is allowed cells will display a draggable reorder handle as a visual hint.
<snippets>
## Responding to cell reorder interaction ##

After the user performs a reorder gesture the following delegate method from the TKListViewDelegate protocol will be called - listView:didReorderItemFromIndexPath:toIndexPath:

This is the place where you get information which item was reordered from what position and to what position. There you need to reorder your source data. 

<snippet>

*In case you are using TKDataSource you may set it as delegate for TKListVie. With such setup you will not need to reorder your data manually .TKDataSource will handle that for you.
<snippet> 
