---
layout: post
title: "SwiftUI: @ObservedObject property wrapper"
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: red
published: true
---
`@ObservedObject` is one of SwiftUI property wrappers which came up in Swift 5.1. If we have data that should be shared between multiple views, and all of them should automatically update when data changes, then `@ObservedObject` is our way to go.<!–-break-–>
`@ObservedObject` and [`@EnvironmentObject`](](https://dreamcraft.io/posts/swiftui-environmentobj-wrapper)) by functionality are the same, but the main difference between those two is the way we pass data. In [this post`@EnvironmentObject`](https://dreamcraft.io/posts/swiftui-environmentobj-wrapper), we have discussed that SwiftUI provides us with an [`Environment`](https://dreamcraft.io/posts/swiftui-environment-wrapper) that allows us to inject objects into and later get them. With `@ObservedObject`, we don't have such opportunity, which means that we have to hand our object till he reaches the view that needs it. Also, as with [`@EnvironmentObject`](https://dreamcraft.io/posts/swiftui-environmentobj-wrapper), the class that we pass through the views should conform to the `ObservableObject` protocol.

```swift
class Parameters: ObservableObject{
  @Published var showColdColor: Bool = false
}
```
In the following example, we see that we should pass (🔥) our Parameters to the ExtractedView. Wich is not the case for `@EnvironmentObject`.

```swift    
struct ExampleView: View {
    @ObservedObject var parameters: Parameters = Parameters()
    
    var body: some View {
        ZStack {
            if self.parameters.showColdColor {
                Color.blue
            } else   {
                Color.red
            }
            ExtractedView(parameters: parameters) //🔥
        }
    }
}

struct ExtractedView: View {
    
    @ObservedObject var parameters: Parameters
    
    var body: some View {
        Button(
            action: { self.parameters.showColdColor.toggle() },
            label: { Text("Change Color").foregroundColor(Color.white) }
        )
    }
}
```
