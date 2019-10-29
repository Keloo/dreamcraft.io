---
layout: post
title: "SwiftUI: @Published property wrapper"
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: red
published: true
---
`@Published` is a property wrapper, that was introduced in Swift 5.1. `@Published` property wrapper augments properties by adding **willSet** observer.<!–-break-–>
Once we know that a property may change its value, we know then we might need to rebuild our UI. The significant part is that SwiftUI knows to do that out of the box. It knows what part of the UI uses that property, and as soon as it gets notified that our property was changed, SwiftUI will rebuild the UI.
In the following example, we see that as soon as we change the value of **showColdColor** property that is wrapped with `@Published`, our view will get notified and will change its color immediately. And of course, our property should be part of a class that conforms to `ObservableObject` protocol.

```swift
class Parameters: ObservableObject{
    @Published var showColdColor: Bool = false
}

struct ExampleView: View {
    
    @ObservedObject var parameters: Parameters = Parameters()
    
    var body: some View {
        ZStack {
            if self.parameters.showColdColor {
                Color.blue
            } else   {
                Color.red
            }
            Button(
                action: { self.parameters.showColdColor.toggle() },
                label: { Text("Change Color").foregroundColor(Color.white) }
            )
        }
    }
}
```
