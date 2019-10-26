---
layout: post
title: "SwiftUI: @Binding property wrapper"
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: black
published: true
---
`@Binding` is one of SwiftUI property wrappers which came up in Swift 5.1. `@Binding` should be used in subviews/reusable components when the value lives outside the current view.<!–-break-–>
In the following example, we can observe that variable **showColdColor** inside **ExtractedView** doesn't have a default value, and it was passed with **$** sign to the **ExtractedView** initializer inside **ExampleView**. The dollar sign means that we are giving a reference where `@Binding` implies that we are sharing the same property with other View(**ExampleView** in our case), and it is stored elsewhere.

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
            ExtractedView(showColdColor: $showColdColor)
        }
    }
}


struct ExtractedView: View {
    
    @Binding var showColdColor: Bool
    
    var body: some View {
        Button(
            action: { self.showColdColor.toggle() },
            label: { Text("Change Color").foregroundColor(Color.white) }
        )
    }
}
```
