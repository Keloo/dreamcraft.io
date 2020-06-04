---
layout: post
title: "SwiftUI: @State property wrapper"
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
  - @state
  - state
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: black
published: true
---
Property wrapper, is a powerful new feature in Swift 5.1. When you add the Property Wrapper, you're wrapping this property and augment it with some additional behavior when it's read or written. `@State` is one of the property wrappers provided by SwiftUI.
<!–-break-–>

When we initialize a property that has `@State` property wrapper, we are prompting SwiftUI to monitor it. So every time `@State` variable is written, SwiftUI will know that and will update the views that depend on that variable in their body. I the following example, we have a button on top of a color. As soon as we press the button, it changes the value of `showColdColor` state property, and SwiftUI recreates View.

```swift
struct ExampleView: View {
  
    @State private var showColdColor: Bool = false

    var body: some View {
        ZStack {
            if self.showColdColor {
                Color.blue
            } else {
                Color.red
            }
            Button(
                action: { self.showColdColor.toggle() },
                label: { Text("Change Color").foregroundColor(Color.white) }
            )
        }
    }
}
```
