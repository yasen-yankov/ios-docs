---
title: Load on demand
page_title: ListView load on demand
position: 11
---

# ListView: Load on demand

There are certain scenarios typically with remote data over the wire where data needs to be loaded continuously on small portions. TKListView may load data on demand.




## Enabling the feature  ##



TODO:// describe the following properties and methods:
@property (nonatomic) NSInteger cellBufferSize;

- (BOOL)listView:(TKListView *)listView shouldLoadMoreDataAtIndexPath:(NSIndexPath*) indexPath;

- (void)didLoadDataOnDemand;
