---
title: Custom Animations
position: 1
---

# Chart Animations: Custom

<code>TKChart</code> uses the Core Animation infrastructure available on iOS that you use to animate the visual points in series. In order to enable the animations, you should set <code>allowAnimations</code> property to *YES*. In that case the default animations are performed for each series. If you handle the <code>TKChartDelegate</code> protocol and implement the <code>chart:animationForSeries:withState:inRect:</code> method, you can perform custom animations. With Core Animation, most of the work required to draw each frame of an animation is done for you. All you have to do is configure a few animation parameters (such as the start and end points).

You can use most of the Core Animation framework to customize the visual points animation. You can read more about Core Animation at [Apple Developer website](https://developer.apple.com/library/mac/documentation/cocoa/Conceptual/CoreAnimation_guide/Introduction/Introduction.html).

## Configuration Prerequisites###

You should handle the <code>TKChartDelegate</code>'s method <code>chart:animationForSeries:withState:inRect:</code> to create a custom animation. In addition, you should group the animation created for each point in CAAnimationGroup to apply animation sequentially. You can access old and new points collection by using the <code>TKChartSeriesRenderState</code> properties <code>oldPoints</code> and <code>points</code>. It allows generation for value key path property for point at a specified index by calling the <code>animationKeyPathForPointAtIndex</code> method.

## Animating Line Series##

The code below animates the line series points by moving them from bottom to top.

```Objective-C
- (CAAnimation *)chart:(TKChart *)chart animationForSeries:(TKChartSeries *)series withState:(TKChartSeriesRenderState *)state inRect:(CGRect)rect
{
    CFTimeInterval duration = 0;
    NSMutableArray *animations = [[NSMutableArray alloc] init];

    for (int i = 0; i<state.points.count; i++) {
        NSString *pointKeyPath = [state animationKeyPathForPointAtIndex:i];
    
        NSString *keyPath = [NSString stringWithFormat:@"%@.y", pointKeyPath];
        TKChartVisualPoint *point = [state.points objectAtIndex:i];
        CGFloat oldY = rect.size.height;
        
        if (i > 0) {
            CAKeyframeAnimation *animation = [CAKeyframeAnimation animationWithKeyPath:keyPath];
            animation.duration = 0.1* (i + 1);
            animation.values = @[ @(oldY), @(oldY), @(point.y) ];
            animation.keyTimes = @[ @0, @(i/(i+1.)), @1 ];
            [animations addObject:animation];
            
            duration = animation.duration;
        }
        else {
            CABasicAnimation *animation = [CABasicAnimation animationWithKeyPath:keyPath];
            animation.fromValue = @(oldY);
            animation.toValue = @(point.y);
            animation.duration = 0.1f;
            [animations addObject:animation];
        }
    }

    CAAnimationGroup *group = [[CAAnimationGroup alloc] init];
    group.duration = duration;
    group.animations = animations;

    return group;
}
```
```Swift
func chart(chart: TKChart!, animationForSeries series: TKChartSeries!, withState state: TKChartSeriesRenderState!, inRect rect: CGRect) -> CAAnimation! {
    var duration = 0.0
    var animations = [CAAnimation]()
    for i in 0 ..< state.points.count() {
        let pointKeyPath = state.animationKeyPathForPointAtIndex(i)
        let keyPath = pointKeyPath + ".y"
        let point = state.points[i] as TKChartVisualPoint
        let oldY = rect.size.height
        
        if i > 0 {
            let animation = CAKeyframeAnimation(keyPath: keyPath)
            animation.duration = 0.1 * Double(i + 1)
            animation.values = [oldY, oldY, point.y]
            animation.keyTimes = [0.0, Double(i) / (Double(i) + 1.0), 1.0]
            animations.append(animation)
            duration = animation.duration
        }
        else {
            let animation = CABasicAnimation(keyPath: keyPath)
            animation.fromValue = oldY
            animation.toValue = point.y
            animation.duration = 0.1
            animations.append(animation)
        }
    }
    
    let group = CAAnimationGroup()
    group.duration = duration
    group.animations = animations
    return group
}
```
```C#
class ChartDelegate: TKChartDelegate
{
    public override CAAnimation AnimationForSeries (TKChart chart, TKChartSeries series, TKChartSeriesRenderState state, CGRect rect)
    {
        var duration = 0.0;
        var animations = new List<CAAnimation> ();
        for (int i=0; i<(int)state.Points.Count; i++) 
        {
            var pointKeyPath = state.AnimationKeyPathForPointAtIndex((uint)i);
            var keyPath = pointKeyPath + ".y";
            var point = state.Points.ObjectAtIndex((uint)i) as TKChartVisualPoint;
            var oldY = rect.Size.Height;

            if (i > 0) {
                var animation = new CAKeyFrameAnimation();
                animation.KeyPath = keyPath;
                animation.Duration = (double)(0.1 * i + 1);
                animation.Values = new NSNumber[] { new NSNumber(oldY), new NSNumber(oldY), new NSNumber(point.Y) };
                animation.KeyTimes = new NSNumber[] { new NSNumber(0), new NSNumber(i / (i + 1.0)), new NSNumber(1.0) };
                animations.Add(animation);
                duration = animation.Duration;
            }
            else {
                var animation = new CABasicAnimation();
                animation.KeyPath = keyPath;
                animation.From = new NSNumber(oldY);
                animation.To = new NSNumber(point.Y);
                animation.Duration = 0.1;
                animations.Add(animation);
            }
        }

        var group = new CAAnimationGroup();
        group.Duration = duration;
        group.Animations = animations.ToArray();
        return group;
    }
}
```

## Animating Pie Series##

The following lines of code animate the pie's segments by moving them to the pie center together with changing their opacity.

```Objective-C
- (CAAnimation *)chart:(TKChart *)chart animationForSeries:(TKChartSeries *)series withState:(TKChartSeriesRenderState *)state inRect:(CGRect)rect
{
    CFTimeInterval duration = 0;
    NSMutableArray *animations = [[NSMutableArray alloc] init];

    for (int i = 0; i<state.points.count; i++) {
        NSString *pointKeyPath = [state animationKeyPathForPointAtIndex:i];
    
        NSString *keyPath = [NSString stringWithFormat:@"%@.distanceFromCenter", pointKeyPath];
        CAKeyframeAnimation *animation = [CAKeyframeAnimation animationWithKeyPath:keyPath];
        animation.values = @[ @50, @50, @0 ];
        animation.keyTimes = @[ @0, @(i/(i+1.)), @1 ];
        animation.duration = 0.5 * (i+1.);
        [animations addObject:animation];
    
        keyPath = keyPath = pointKeyPath + ".opacity"
        animation = [CAKeyframeAnimation animationWithKeyPath:keyPath];
        animation.values = @[ @0, @0, @1 ];
        animation.keyTimes = @[ @0, @(i/(i+1.)), @1 ];
        animation.duration = 0.5 * (i+1.);
        [animations addObject:animation];
    
        duration = animation.duration;
    }

    CAAnimationGroup *group = [[CAAnimationGroup alloc] init];
    group.duration = duration;
    group.animations = animations;
    return group;
}
```
```Swift
func chart(chart: TKChart!, animationForSeries series: TKChartSeries!, withState state: TKChartSeriesRenderState!, inRect rect: CGRect) -> CAAnimation! {
    var duration = 0.0
    var animations = [CAAnimation]()
    
    for i in 0..<state.points.count() {
        let pointKeyPath = state.animationKeyPathForPointAtIndex(i)
        var keyPath = pointKeyPath + ".distanceFromCenter"
        var animation = CAKeyframeAnimation(keyPath: keyPath)
        animation.values = [50, 50, 0]
        animation.keyTimes = [0.0, Double(i) / (Double(i) + 1.0), 1.0]
        animation.duration = CFTimeInterval(0.5 * Double(i) + 1.0)
        animations.append(animation)
        
        keyPath = pointKeyPath + ".opacity"
        animation = CAKeyframeAnimation(keyPath: keyPath)
        animation.values = [0, 0, 1.0]
        animation.keyTimes = [0.0, Double(i) / (Double(i) + 1.0), 1.0]
        animation.duration = CFTimeInterval(0.5 * Double(i) + 1.0)
        animations.append(animation)
        
        duration = animation.duration
    }
    
    let group = CAAnimationGroup()
    group.duration = duration
    group.animations = animations
    return group
}
```
```C#
class ChartDelegate2: TKChartDelegate
{
    public override CAAnimation AnimationForSeries (TKChart chart, TKChartSeries series, TKChartSeriesRenderState state, CGRect rect)
    {
        var duration = 0.0;
        var animations = new List<CAAnimation> ();

        for (int i=0; i<(int)state.Points.Count; i++) {
            var pointKeyPath = state.AnimationKeyPathForPointAtIndex ((uint)i);
            var animation = new CAKeyFrameAnimation();
            animation.KeyPath = pointKeyPath + ".distanceFromCenter";
            animation.Values = new NSNumber[] { new NSNumber(50), new NSNumber(50), new NSNumber(0) };
            animation.KeyTimes = new NSNumber[] { new NSNumber(0), new NSNumber(i / (i + 1.0)), new NSNumber(1) };
            animation.Duration = 0.5 * (double)(i + 1.0);
            animations.Add(animation);

            animation = new CAKeyFrameAnimation();
            animation.KeyPath =  new NSString(string.Format("{0}.opacity", pointKeyPath));
            animation.Values = new NSNumber[] { new NSNumber(0), new NSNumber(0), new NSNumber(1) };
            animation.KeyTimes = new NSNumber [] { new NSNumber(0), new NSNumber(i / (i + 1.0)), new NSNumber(1) };
            animation.Duration = 0.5 * (double)(i + 1.0);
            animations.Add(animation);

            duration = animation.Duration;
        }

        var group = new CAAnimationGroup();
        group.Duration = duration;
        group.Animations = animations.ToArray();

        return group;
    }
}
```
