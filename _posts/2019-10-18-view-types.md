---
layout: post
title: "SwiftUI: View types."
tags:
  - Swift Evolution
  - SwiftUI
  - swift 5
  - tutorial
  - guide
  - ios
  - macOS
  - uikit
  - watchkit
  - tvos
  - watchos
  - guide
  - iphone
  - architecture
  - guide
  - apple
  - dreamcraft
  - property wrapper
  - primitive view
  - container
  - view types
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: purple
published: true
---
Views are the basic building blocks of user interfaces. Controls, containers from your app, everything that you see, is defined by a view. There are two types of views: primitives and containers.
 <!–-break-–>

## Container views
In SwiftUI, a container view is declared as a composition of other views serving as their content.

`List`, `Stacks`([Vstack, HStack, ZStack](https://dreamcraft.io/posts/stack-swiftui)), Form a few examples of container views. The container view content views are declared within a special kind of closer known as a view builder.

  @inlinable public init(alignment: HorizontalAlignment = .center, spacing: CGFloat? = nil, @ViewBuilder content: () -> Content)

View Builders @ViewBuilder allows us to write declarative code in the body of the closure. The Swift Compiler knows how to translate a closure marked by this attribute into a new closure that returns a single view representing all of the contents within our container(stack in our case).

## Primitive Views
Primitive views are views that don't have any contents of their own, and that represents those atomic building blocks on which all other views are built. `Image` and `Text` are other examples of primitive views. SwiftUI also offers primitives for drawing like `Color` and `Shape`, as well as layout primitives like `Spacer`. You can do some pretty sophisticated drawing just using primitive views in SwiftUI.


## Tips
Since in SwiftUI we are writing declarative code, we don't need to bother about keeping our view hierarchies as small and light as possible. So even though we had to wrap our view in multiple wrapper views, SwiftUI collapses that down behind the scenes into an efficient data structure that is then used by the render system. In conclusion, adding a new wrapper view is effectively free since SwiftUI will optimize it down behind the scenes. And so the important thing here is that you no longer have to compromise between organizing your view code the way that makes the most sense to you and getting the best performance from your app.
