---
layout: post
title: "SwiftUI: About modifiers and how to create your own."
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
  - modifier
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: red
published: true
---
Whenever we want to change the way a view look, we call a modifier on it. The background color, font, or foreground are a few examples of methods that are known as a modifier in SwiftUI.  A modifier is just a method that creates a new view from a current view.
 <!–-break-–>

## How to create a modifier.
To create your modifier, you need to define a struct that conforms to the `ViewModifier` protocol. This one requires you to implement the `body(content: Content)` method. That method provides us with the `content` parameter that we will use for our transformations. In our example, we set a blue background with a large font and white foreground with a corner radius equal to 5 and padding.

```swift
struct MainStyleLabel: ViewModifier{
    func body(content: Content) -> some View{
        content
            .background(Color.blue)
            .font(.title).foregroundColor(.white)
            .cornerRadius(5)
            .padding()
    }
}

struct ExampleView: View {
    var body: some View {
        VStack{
            Text("Dreamcraft.io").foregroundColor(.green).modifier(MainStyleLabel())
            Text("🔥🔥🔥🔥🔥🔥").modifier(MainStyleLabel())
            Text(" custom modified label ").modifier(MainStyleLabel())
        }
    }
}
```
