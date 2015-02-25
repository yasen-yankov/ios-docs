---
title: Populating with data
page_title: ListView populating with data
position: 3
---

# ListView: Populating with data

There are two ways to feed TKListView data you need to display. You can do that by implementing several methods from the TKListViewDataSource protocol or you could let the  TKDataSource component do the dirty work for you. 

## Populating with data using TKDataSource ##
TKDataSource contains implementation of the TKListViewDataSource protocol that you may use out-of-the box. In addition TKDataSource provides handy data shaping capabilities such as sorting and filtering.

The following example shows how to initialise TKDataSource with data and feed that data to TKListView/
<snippets>


## Populating with data using TKListViewDataSource protocol##

Alternatively TKListView may be populated with data by manually implementing several methods from the TKListViewDataSource protocol. This way requires a bit more code but gives more flexibility.
<snippets>


