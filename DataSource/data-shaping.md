---
title: Data Shaping Operations
page_title: DataSource Data Shaping Operations
position: 4
---

# DataSource: Data Shaping Operations

<code>TKDataSource</code> supports a full range of data shaping operations with APIs specific for your scenario. 

The simplest way to shape your data is to use the block API. Just specify the block function responsible for the data operation:

```Objective-C
[dataSource filter:^BOOL(id item) { return [item intValue] > 5; }];

[dataSource sort:^NSComparisonResult(id obj1, id obj2) {
    int a = [obj1 intValue];
    int b = [obj2 intValue];
    if (a < b) { return NSOrderedAscending; }
    else if (a > b) { return NSOrderedDescending; }
    return NSOrderedSame;
}];

[dataSource group:^id(id item) { return @([item intValue] % 2 == 0); }];
```
```Swift
dataSource.filter { $0 as Int > 5 }

dataSource.sort {
    let a = $0 as Int
    let b = $1 as Int
    if a < b { return NSComparisonResult.OrderedDescending }
    else if a > b { return NSComparisonResult.OrderedAscending }
    return NSComparisonResult.OrderedSame
}

dataSource.group { ($0 as Int) % 2 == 0 }
```
```C#
dataSource.Filter ((NSObject obj) => { return ((NSNumber)obj).Int32Value > 5; });

dataSource.Sort ((NSObject obj1, NSObject obj2) => {
	int a = ((NSNumber)obj1).Int32Value;
	int b = ((NSNumber)obj2).Int32Value;
	if (a<b) return NSComparisonResult.Descending;
	else if (a>b) return NSComparisonResult.Ascending;
	return NSComparisonResult.Same;
});

dataSource.Group ((NSObject obj) => { return NSObject.FromObject( ((NSNumber)obj).Int32Value % 2 == 0 ); });
```

The block API is not limited to sorting, filtering, and grouping. A range of functional methods like <code>map</code>, <code>reduce</code> and <code>enumerate</code> are also available:

```Objective-C
TKDataSource *dataSource = [[TKDataSource alloc] initWithArray:@[ @10, @5, @12, @13, @7, @44 ]];

[dataSource map:^id(id item) {
    return @([item intValue] * 10);
}];

NSNumber *maxValue = [dataSource reduce:@0 with:^id(id item, id value) {
    NSInteger a = [item intValue];
    NSInteger b = [value intValue];
    if (a>b) { return @(a); }
    return @(b);
}];

[dataSource enumerate:^(id item) {
    NSLog(@"%@", item);
}];
```
```Swift
let dataSource = TKDataSource(array: [ 10, 5, 12, 13, 7, 44 ])

dataSource.map { (AnyObject item) -> AnyObject! in
    return (item as! Int) * 10
}

let maxValue = dataSource.reduce(0, with: { (AnyObject item, AnyObject value) -> AnyObject! in
    let a = item as! Int
    let b = value as! Int
    if a>b { return a }
    return b
}) as! Int

dataSource.enumerate { (AnyObject item) -> Void in
    println(item)
}
```
```C#
NSObject[] array = new NSObject[] {
	NSObject.FromObject (10),
	NSObject.FromObject (5),
	NSObject.FromObject (12),
	NSObject.FromObject (13),
	NSObject.FromObject (7),
	NSObject.FromObject (44)
};

TKDataSource dataSource = new TKDataSource (array);

dataSource.Map ((NSObject item) => {
	return NSObject.FromObject(((NSNumber)item).Int32Value * 10);
});

NSObject maxValue = dataSource.Reduce (NSObject.FromObject (0), (NSObject item, NSObject value) => {
	int a = ((NSNumber)item).Int32Value;
	int b = ((NSNumber)value).Int32Value;
	if (a>b) return item;
	return value;
});

dataSource.Enumerate ((NSObject item) => {
	Console.WriteLine(item);
});
```

<code>TKDataSource</code> supports also <code>NSPredicate</code> style queries. The following methods use queries and property names instead of block methods:

```Objective-C
NSMutableArray *items = [NSMutableArray new];
[items addObject:[[DataSourceItem alloc] initWithName:@"John" value:50 group:@"A"]];
[items addObject:[[DataSourceItem alloc] initWithName:@"Abby" value:33 group:@"A"]];
[items addObject:[[DataSourceItem alloc] initWithName:@"Smith" value:42 group:@"B"]];
[items addObject:[[DataSourceItem alloc] initWithName:@"Peter" value:28 group:@"B"]];
[items addObject:[[DataSourceItem alloc] initWithName:@"Paula" value:25 group:@"B"]];

TKDataSource *dataSource = [TKDataSource new];
dataSource.itemSource = items;
[dataSource filterWithQuery:@"value > 30"];
[dataSource sortWithKey:@"value" ascending:true];
[dataSource groupWithKey:@"group"];
```
```Swift
var items = [DataSourceItem]()
items.append(DataSourceItem(name: "John", value: 50, group: "A"))
items.append(DataSourceItem(name: "Abby", value: 33, group: "A"))
items.append(DataSourceItem(name: "Smith", value: 42, group: "B"))
items.append(DataSourceItem(name: "Peter", value: 28, group: "B"))
items.append(DataSourceItem(name: "Paula", value: 25, group: "B"))

let dataSource = TKDataSource()
dataSource.itemSource = items
dataSource.filterWithQuery("value > 30")
dataSource.sortWithKey("value", ascending: true)
dataSource.groupWithKey("group")
```
```C#
NSMutableArray items = new NSMutableArray();
items.Add (new DataSourceItem () { Name = "John", Value = 50, Group = "A" });
items.Add (new DataSourceItem () { Name = "Abby", Value = 33, Group = "A" });
items.Add (new DataSourceItem () { Name = "Smith", Value = 42, Group = "B" });
items.Add (new DataSourceItem () { Name = "Peter", Value = 28, Group = "B" });
items.Add (new DataSourceItem () { Name = "Paula", Value = 25, Group = "B" });

TKDataSource dataSource = new TKDataSource ();
dataSource.ItemSource = items;
dataSource.FilterWithQuery ("Value > 30");
dataSource.SortWithKey ("Value", true);
dataSource.GroupWithKey ("Group");
```

All the methods mentioned above execute immediately when called. They operate directly on the current <code>items</code> view in <code>TKDataSource</code>. <code>TKDataSource</code> extends its API by supporting three collections with sorting, filtering and group descriptors. 

The descriptors API supports both code blocks and queries with property names. This allows for specifying the data shaping operations before loading the data. In this scenario all descriptors are applied after the data is actually loaded in <code>TKDataSource</code>. This data-loading operation can happen on setting the <code>itemSource</code> property. The following code demonstrates this API:

```Objective-C
TKDataSource *dataSource = [TKDataSource new];
[dataSource addFilterDescriptor:[[TKDataSourceFilterDescriptor alloc] initWithQuery:@"value > 30"]];
[dataSource addSortDescriptor:[[TKDataSourceSortDescriptor alloc] initWithProperty:@"value" ascending:true]];
[dataSource addGroupDescriptor:[[TKDataSourceGroupDescriptor alloc] initWithProperty:@"group"]];

//...

dataSource.itemSource = items;
```
```Swift
let dataSource = TKDataSource()
dataSource.addFilterDescriptor(TKDataSourceFilterDescriptor(query: "value > 30"))
dataSource.addSortDescriptor(TKDataSourceSortDescriptor(property: "value", ascending: true))
dataSource.addGroupDescriptor(TKDataSourceGroupDescriptor(property: "group"))

//...

dataSource.itemSource = items
```
```C#
TKDataSource dataSource = new TKDataSource ();
dataSource.AddFilterDescriptor (new TKDataSourceFilterDescriptor ("Value > 30"));
dataSource.AddSortDescriptor (new TKDataSourceSortDescriptor ("Value", true));
dataSource.AddGroupDescriptor (new TKDataSourceGroupDescriptor ("Group"));

// ...

dataSource.ItemSource = items;
```

You can modify descriptor collections by using the corresponding add and remove methods. You can reaplly all descriptors when data has changed by calling the <code>reloadData</code> method:

```Objective-C
[dataSource reloadData];
```
```Swift
dataSource.reloadData()
```
```C#
dataSource.ReloadData();
```
