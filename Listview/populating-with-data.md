---
title: Populating with data
page_title: ListView populating with data
position: 3
---

# ListView: Populating with data

There are two ways to feed TKListView data you need to display. You can do that by implementing several methods from the TKListViewDataSource protocol or you could let the  TKDataSource component do the dirty work for you. 

## Populating with data using TKDataSource ##
TKDataSource contains implementation of the TKListViewDataSource protocol that you may use out-of-the box. In addition TKDataSource provides handy data shaping capabilities such as sorting and filtering.

The following example shows how to initialise TKDataSource with data and feed that data to TKListView.

```Objective-C
_sampleArrayOfStrings =@[@"Kristina Wolfe",@"Freda Curtis",@"Jeffery Francis",@"Eva Lawson",@"Emmett Santos", @"Theresa	Bryan", @"Jenny Fuller", @"Terrell Norris", @"Eric Wheeler", @"Julius Clayton", @"Alfredo Thornton", @"Roberto Romero",@"Orlando Mathis",@"Eduardo Thomas",@"Harry Douglas"];
    
_dataSource = [[TKDataSource alloc] initWithArray:_sampleArrayOfStrings];
    
TKListView *_listView = [[TKListView alloc] initWithFrame: self.view.bounds];
_listView.dataSource = _dataSource;
[self.view addSubview:_listView];
```
```Swift
self.sampleArrayOfStrings = ["Kristina Wolfe","Freda Curtis","Jeffery Francis","Eva Lawson","Emmett Santos", "Theresa Bryan", "Jenny Fuller", "Terrell Norris", "Eric Wheeler", "Julius Clayton", "Alfredo Thornton", "Roberto Romero","Orlando Mathis","Eduardo Thomas","Harry Douglas"]

dataSource = TKDataSource(array:sampleArrayOfStrings)

let listView = TKListView(frame: self.view.bounds)
listView.dataSource = dataSource
self.view.addSubview(listView)
```
```C#
this.sampleArrayOfStrings = NSArray.FromStrings (new String [] {
	"Kristina Wolfe",
	"Freda Curtis",
	"Jeffery Francis",
	"Eva Lawson",
	"Emmett Santos",
	"Theresa Bryan",
	"Jenny Fuller",
	"Terrell Norris",
	"Eric Wheeler",
	"Julius Clayton",
	"Alfredo Thornton",
	"Roberto Romero",
	"Orlando Mathis",
	"Eduardo Thomas",
	"Harry Douglas"
});

this.dataSource = new TKDataSource (sampleArrayOfStrings);

TKListView listView = new TKListView (this.View.Bounds);
listView.WeakDataSource = this.dataSource;
this.View.AddSubview (listView);
```

## Populating with data using TKListViewDataSource protocol##

Alternatively TKListView may be populated with data by manually implementing several methods from the TKListViewDataSource protocol. This way requires a bit more code but gives more flexibility.
First we need to set the datasource property of TKListView to a class adopting the TKListViewDatasource protocol. In the sample code bellow it is our view controller.

```Objective-C
- (void)viewDidLoad
{
	[super viewDidLoad];

	_sampleArrayOfStrings =@[@"Kristina Wolfe",@"Freda Curtis",@"Jeffery Francis",@"Eva 	Lawson",@"Emmett Santos", @"Theresa	Bryan", @"Jenny Fuller", @"Terrell Norris", 	@"Eric Wheeler", @"Julius Clayton", @"Alfredo Thornton", @"Roberto Romero",@"Orlando 	Mathis",@"Eduardo Thomas",@"Harry Douglas"];
    
	TKListView *_listView = [[TKListView alloc] initWithFrame: self.view.bounds];
	[_listView registerClass:[TKListViewCell class] forCellWithReuseIdentifier:@"cell"];
	_listView.dataSource = self;

	[self.view addSubview:_listView];
}

-(NSInteger)listView:(TKListView *)listView numberOfItemsInSection:(NSInteger)section  {
	return _sampleArrayOfStrings.count;
}

-(NSInteger)numberOfSectionsInListView:(TKListView *)listView
{
	return 1;
}

- (TKListViewCell *)listView:(TKListView *)listView cellForItemAtIndexPath:(NSIndexPath *)indexPath
{
	TKListViewCell *cell = [listView dequeueReusableCellWithReuseIdentifier:@"cell" forIndexPath:indexPath];
	cell.textLabel.text = _sampleArrayOfStrings[indexPath.row];
    
	return cell;
}

```
```Swift
override func viewDidLoad() {
	super.viewDidLoad()
	self.sampleArrayOfStrings = ["Kristina Wolfe","Freda Curtis","Jeffery Francis","Eva Lawson","Emmett Santos", "Theresa Bryan", "Jenny Fuller", "Terrell Norris", "Eric Wheeler", "Julius Clayton", "Alfredo Thornton", "Roberto Romero","Orlando Mathis","Eduardo Thomas","Harry Douglas"]
	let listView = TKListView(frame:  self.view.bounds)
	listView.registerClass(TKListViewCell.self, forCellWithReuseIdentifier: "cell")
	listView.dataSource = self
	listView.selectionBehavior = TKListViewSelectionBehavior.None
	self.view.addSubview(listView)
}
    
func  listView(listView: TKListView!, cellForItemAtIndexPath indexPath: NSIndexPath!) -> TKListViewCell! {
	let cell = listView.dequeueReusableCellWithReuseIdentifier("cell", forIndexPath: indexPath)  as TKListViewCell
        
	cell.textLabel.text = self.sampleArrayOfStrings[indexPath.row] as NSString
        
	return cell
}
    
func listView(listView: TKListView!, numberOfItemsInSection section: Int) -> Int {
	return self.sampleArrayOfStrings.count
}

func numberOfSectionsInListView(listView: TKListView!) -> Int {
	return 1
}
```
```C#
this.sampleArrayOfStrings = NSArray.FromStrings (new String [] { 
	"Kristina Wolfe",
	"Freda Curtis",
	"Jeffery Francis",
	"Eva Lawson",
	"Emmett Santos",
	"Theresa Bryan",
	"Jenny Fuller",
	"Terrell Norris",
	"Eric Wheeler",
	"Julius Clayton",
	"Alfredo Thornton",
	"Roberto Romero",
	"Orlando Mathis",
	"Eduardo Thomas",
	"Harry Douglas"
});
				
TKListView listView = new TKListView (this.View.Bounds);
listView.RegisterClassForCell (new Class (typeof(TKListViewCell)), "cell");
listView.DataSource = new ListViewDataSource (this);

this.View.AddSubview (listView);

class ListViewDataSource: TKListViewDataSource
{
	ViewController owner;

	public ListViewDataSource(ViewController owner)
	{
		this.owner = owner;
	}

	public override int NumberOfItemsInSection (TKListView listView, int section)	{
		return (int)this.owner.sampleArrayOfStrings.Count;
	}

	public override int NumberOfSectionsInListView (TKListView listView)
	{
		return 1;
	}

	public override TKListViewCell CellForItem (TKListView listView, NSIndexPath indexPath)
	{
		TKListViewCell cell = listView.DequeueReusableCell ("cell", indexPath) as TKListViewCell;
		cell.TextLabel.Text = this.owner.sampleArrayOfStrings.GetItem<NSString> ((uint)indexPath.Row);
		return cell;
	}
}
```
