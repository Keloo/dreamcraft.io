---
layout: post
title: "SwiftUI: @Environment property wrapper"
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
  - @environment
  - environment
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: purple
published: true
---
When we create our first view in SwiftUI, the framework generates an **Environment** for it. SwiftUI uses **Environment** to store different system settings like the color scheme and app-specific stuff like default font.<!–-break-–>
All system settings and app-specific stuff except our EnvironmentObjects are pre-defined environment values. In the [previous article](https://dreamcraft.io/posts/swiftui-environmentobj-wrapper), we have discussed how to create [EnvironmentObjects](https://dreamcraft.io/posts/swiftui-environmentobj-wrapper) and how to pass them to the **Environment**.

 `@Environment` property wrapper is specifically to work with pre-defined environment values. With the `@Environment` you can get a lot of things starting from the default font of this Environment and ending with managed object context and undo manager. Here is how to get those values.

```swift
@Environment(\.managedObjectContext) var managedObjectContext
@Environment(\.undoManager) var undoManager
@Environment(\.colorScheme) var colorScheme
```
[Here](https://developer.apple.com/documentation/swiftui/environmentvalues), you can check the full collection of environmental values.
[Suggested post: how to set Environment predefined environment values](https://dreamcraft.io/posts/swiftui-how-to-modify-environment-values)

