---
title: Gouping
page_title: ListView grouping
position: 4
---

# ListView: grouping 
ListView may be set up to display items in groups divided visually by section headers and footers.
There are two ways to implement grouping with TKListView - manually implementing the required methods from TKListViewDataSource delegate or using TKDataSource and let it do the dirty work for you.
<screenshot>

## Displaying grouped data using TKDataSource##
```Objective-C- (void)viewDidLoad
{
    [super viewDidLoad];
    
    NSMutableArray *items = [NSMutableArray new];
    [items addObject:[[DataSourceItem alloc] initWithName:@"John" value:50 group:@"A"]];
    [items addObject:[[DataSourceItem alloc] initWithName:@"Abby" value:33 group:@"A"]];
    [items addObject:[[DataSourceItem alloc] initWithName:@"Smith" value:42 group:@"B"]];
    [items addObject:[[DataSourceItem alloc] initWithName:@"Peter" value:28 group:@"B"]];
    [items addObject:[[DataSourceItem alloc] initWithName:@"Paula" value:25 group:@"B"]];
    
    dataSource = [TKDataSource new];
    dataSource.itemSource = items;
    [dataSource groupWithKey:@"group"];
    dataSource.displayKey = @"name";

    TKListView *_listView = [[TKListView alloc] initWithFrame: CGRectMake(20, 20, self.view.bounds.size.width-40,self.view.bounds.size.height-40)];
    _listView.dataSource = dataSource;
    _listView.layout.headerReferenceSize = CGSizeMake(200, 22);

    [self.view addSubview:_listView];
}
```
```Swift
	    var dataSource: TKDataSource?
    override func viewDidLoad() {
        super.viewDidLoad()
        var items = [DataSourceItem]()
        items.append(DataSourceItem(name: "John", value: 50, group: "A"))
        items.append(DataSourceItem(name: "Abby", value: 33, group: "A"))
        items.append(DataSourceItem(name: "Smith", value: 42, group: "B"))
        items.append(DataSourceItem(name: "Peter", value: 28, group: "B"))
        items.append(DataSourceItem(name: "Paula", value: 25, group: "B"))

        dataSource = TKDataSource()
        dataSource?.itemSource = items
        dataSource?.groupWithKey("group")
        dataSource?.displayKey = "name"
        let listView = TKListView(frame: CGRectMake(20, 20, self.view.bounds.size.width-40,self.view.bounds.size.height-40))
        listView.dataSource = dataSource
        listView.layout.headerReferenceSize = CGSizeMake(200, 22)
        self.view.addSubview(listView)
    }
```
```C#

```

## Displaying grouped data using a TKListViewDataSource delegate methods##

```Objective-C

```
```Swift

```
```C#

```
