---
title: UIKit Dynamics Animations
position: 2
---

# Chart Animations: UIKit Dynamics Animations

<code>TKChart</code> can uses the UIKit Dynamics physics engine integrated in iOS 7.0 to animate the points in series. It allows you to create interfaces that feel real by adding behaviors such as gravity, attachments (springs) and forces. You define the physical traits that you would like your interface elements to adopt, and the dynamics engine takes care of the rest.

You should set the <code>allowAnimations</code> property to *YES* to enable UIKit Dynamics animations.

## Configuration###

The approach below shows how you can apply a fall down animation to the visual points in line series.

```Objective-C
- (void)viewDidAppear:(BOOL)animated
{
    [super viewDidAppear:animated];

    UIDynamicAnimator *animator = [[UIDynamicAnimator alloc] initWithReferenceView:chart];

    NSArray *points = [chart visualPointsForSeries:chart.series[0]];

    UICollisionBehavior *collision = [[UICollisionBehavior alloc] initWithItems:points];
    collision.translatesReferenceBoundsIntoBoundary = YES;

    UIGravityBehavior *gravity = [[UIGravityBehavior alloc] initWithItems:points];
    gravity.gravityDirection = CGVectorMake(0.f, 2.f);

    UIDynamicItemBehavior *dynamic = [[UIDynamicItemBehavior alloc] initWithItems:points];
    dynamic.elasticity = 0.5f;

    [animator addBehavior:dynamic];
    [animator addBehavior:gravity];
    [animator addBehavior:collision];

}
```
```Swift
override func viewDidAppear(animated: Bool) {
    super.viewDidAppear(animated)
    let animator = UIDynamicAnimator(referenceView: chart)
    let points = chart.visualPointsForSeries(chart.series()[0] as TKChartSeries)
    let collisions = UICollisionBehavior(items: points)
    collisions.translatesReferenceBoundsIntoBoundary = true
    
    let gravity = UIGravityBehavior(items: points)
    gravity.gravityDirection = CGVectorMake(0.0, 2.0)
    
    let dynamic = UIDynamicItemBehavior(items: points)
    dynamic.elasticity = 0.5
    
    animator.addBehavior(dynamic)
    animator.addBehavior(gravity)
    animator.addBehavior(collisions)
}
```
