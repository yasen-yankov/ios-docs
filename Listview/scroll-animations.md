---
title: Scroll animations
page_title: ListView Scroll Animations
position: 7
---

# ListView: Scroll Animations

TKListView can animate items on scrolling. It provides several animations effects for items appearing in the viewport while the end-user scrolls - fade-in, slide-in, scale-in. Those can be combined.

<img src="../images/listview-scroll-animations001.png" />

## Adding animation behavior for cells 


In order to add an animation behavior for cells, use the <code>TKListViewCellAppearBehavior</code> property. 

```Objective-C
self.listView.cellAppearBehavior = [[TKListViewCellScaleInBehavior alloc] init];
```
```Swift
self.listView.cellAppearBehavior = TKListViewCellAppearBehavior()
```
```C#
this.listView.CellAppearBehavior = new TKListViewCellScaleInBehavior ();
```

## Combining cell animation behaviors 

Animation behaviors may be combined as follows : 

```Objective-C
self.listView.cellAppearBehavior = [[TKListViewCellFadeInBehavior alloc] init];
[self.listView.cellAppearBehavior addChildBehavior:[[TKListViewCellScaleInBehavior alloc] init]];
```
```Swift
self.listView.cellAppearBehavior = TKListViewCellFadeInBehavior()
self.listView.cellAppearBehavior.addChildBehavior(TKListViewCellScaleInBehavior())
```
```C#
this.listView.CellAppearBehavior = new TKListViewCellFadeInBehavior ();
this.listView.CellAppearBehavior.AddChildBehavior (new TKListViewCellScaleInBehavior ());
```
