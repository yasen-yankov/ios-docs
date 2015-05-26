---
title: Animations
page_title: ListView Animations
position: 7
---

# ListView: Animations

TKListView supports threee predefined item animations: fade-in, slide-in and scale-in. Those animations can be applied when items enter different states. The following list contains all states where animations can be applied:

- when adding/inserting an item
- when removing an item
- when an item appears when scrolling

<img src="../images/listview-animations001.png" />

Animations are controlled by setting properties of TKListViewLinearLayout class. The animation duration is controlled by setting the animationDuration property:

```Objective-C
TKListViewLinearLayout *layout = (TKListViewLinearLayout*)listView.layout;
layout.animationDuration = 0.5;
```
```Swift
let layout = listView.layout as! TKListViewLinearLayout
layout.animationDuration = 0.5
```
```C#
var layout = listView.Layout as TKListViewLinearLayout;
layout.AnimationDuration = 0.5f;
```

## Add/Remove animations

To animate an item on insert set the itemInsertAnimation property:

```Objective-C
layout.itemInsertAnimation = TKListViewItemAnimationScale;
```
```Swift
layout.itemInsertAnimation = TKListViewItemAnimation.Scale
```
```C#
layout.ItemInsertAnimation = TKListViewItemAnimation.Scale;
```

Use the insertItemsAtIndexPaths: method to insert an item with animation:

```Objective-C
[listView insertItemsAtIndexPaths:@[[NSIndexPath indexPathForRow:10 inSection:0]]];
```
```Swift
listView.insertItemsAtIndexPaths([ NSIndexPath(forRow: 10, inSection: 0) ])
```
```C#
listView.InsertItems (new NSIndexPath[]{ NSIndexPath.FromRowSection(10, 0) });
```

To animate an item on delete set the itemDeleteAnimation property:

```Objective-C
layout.itemDeleteAnimation = TKListViewItemAnimationSlide;
```
```Swift
layout.itemDeleteAnimation = TKListViewItemAnimation.Slide
```
```C#
layout.ItemDeleteAnimation = TKListViewItemAnimation.Slide;
```

Use the deleteItemsAtIndexPaths: method to delete an item with animation:

```Objective-C
[listView deleteItemsAtIndexPaths:@[[NSIndexPath indexPathForRow:10 inSection:0]]];
```
```Swift
listView.deleteItemsAtIndexPaths([ NSIndexPath(forRow: 10, inSection: 0) ])
```
```C#
listView.DeleteItems (new NSIndexPath[]{ NSIndexPath.FromRowSection(10, 0) });
```

Be sure to update your data source before triggering item insert/delete methods in TKListView.

## Appear/Disapear animations

Those animations are applied when scrolling the list view. You can add a scroll animation by setting the itemAppearAnimation property of TKListViewLinearLayout:

```Objective-C
layout.itemAppearAnimation = TKListViewItemAnimationFade;
```
```Swift
layout.itemAppearAnimation = TKListViewItemAnimation.Fade
```
```C#
layout.ItemAppearAnimation = TKListViewItemAnimation.Fade;
```

