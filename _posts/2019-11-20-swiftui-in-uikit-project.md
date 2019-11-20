---
layout: post
title: "SwiftUI: HostingController or how to adopt SwiftUI in existing UIKit/AppKit/WatchKit project."
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: pink
published: true
---
I think that  SwiftUI and Combine will change the way people will write code in 2 years. In this post, we will discuss how to start using SwiftUI in an existing UIKit project so that you can have a smoother transition to SwiftUI projects. Especially if your application support starts from iOS 13, you should do that transition.
 <!–-break-–>
 
 For our purpose, Apple provides us with a container that can carry our SwiftUI view. Its called UIHostingController(for UIKit), NSHostingController(for AppKit) and WKHostingController(for WatchKitt). All of them are subclasses of ViewControllers specific to the platform.

## By code.
We can use the SwiftUI view by directly initializing the HostingController with our SwfitUI view.

```swift

let mySwiftUIView = MySwiftUIView()
let hostViewController = UIHostingController(rootView: mySwiftUIView)

```
## By interface builder
Apple has introduced the Hosting View Controller component in Interface Builder.
