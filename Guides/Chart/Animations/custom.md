---
title: Custom Animations
slug: chart-animations-custom
tags: Chart, iOS, animations
publish: true
ordinal: 1
---

TKChart uses the Core Animation infrastructure available on iOS that you use to animate the visual points in series. In order to enable the animations, you should set **allowAnimations** property to *YES*. In that case the default animations are performed for each series. If you handle the TKChartDelegate protocol and implement the **chart:animationForSeries:withState:inRect:**. method, you can perform custom animations. With Core Animation, most of the work required to draw each frame of an animation is done for you. All you have to do is configure a few animation parameters (such as the start and end points).

You can use most of the Core Animation framework to customize the visual points animation. You can read more about Core Animation at [Apple Developer website](https://developer.apple.com/library/mac/documentation/cocoa/Conceptual/CoreAnimation_guide/Introduction/Introduction.html).

##Configuration Prerequisites###

You should handle the TKChartDelegate's method **chart:animationForSeries:withState:inRect:** to create a custom animation. In addition, you should group the animation created for each point in CAAnimationGroup to apply animation sequentially. You can access old and new points collection by using the TKChartSeriesRenderState properties **oldPoints** and **points**. It allows generation for value key path property for point at a specified index by calling the **animationKeyPathForPointAtIndex** method.

##Animating Line Series##

The code below animates the line series points by moving them from bottom to top.

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

##Animating Pie Series##

The following lines of code animate the pie's segments by moving them to the pie center together with changing their opacity.

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
        
        	keyPath = [NSString stringWithFormat:@"%@.opacity", pointKeyPath];
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