---
title: UIKit Dynamics Animations
slug: chart-animations-custom-uikit-dynamics
tags: Chart, iOS, UIKit
publish: true
ordinal: 2
---

##Overview##

TKChart can uses the UIKit Dynamics physics engine integrated in iOS 7.0 to animate the points in series. It allows you to create interfaces that feel real by adding behaviors such as gravity, attachments (springs) and forces. You define the physical traits that you would like your interface elements to adopt, and the dynamics engine takes care of the rest.

You should set the **allowAnimations** property to *YES* to enable UIKit Dynamics animations.

##Configuration###

The approach below shows how you can apply a fall down animation to the visual points in line series.

    - (void)viewDidAppear:(BOOL)animated
    {
        [super viewDidAppear:animated];
    
        _animator = [[UIDynamicAnimator alloc] initWithReferenceView:_chart];
    
        NSArray *points = [_chart visualPointsForSeries:_chart.series[0]];
    
        UICollisionBehavior *collision = [[UICollisionBehavior alloc] initWithItems:points];
        collision.translatesReferenceBoundsIntoBoundary = YES;
    
        UIGravityBehavior *gravity = [[UIGravityBehavior alloc] initWithItems:points];
        gravity.gravityDirection = CGVectorMake(0.f, 2.f);
    
        UIDynamicItemBehavior *dynamic = [[UIDynamicItemBehavior alloc] initWithItems:points];
        dynamic.elasticity = 0.5f;
    
        [_animator addBehavior:dynamic];
        [_animator addBehavior:gravity];
        [_animator addBehavior:collision];
    }
