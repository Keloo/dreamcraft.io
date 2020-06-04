---
layout: post
title: "SwiftUI: How to add animation to your view?"
tags:
  - Swift Evolution
  - SwiftUI
  - swift 5
  - tutorial
  - guide
  - ios
  - macOS
  - watchkit
  - tvos
  - watchos
  - guide
  - animation
  - architecture
  - guide
  - apple
  - dreamcraft
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: red
published: true
---

SwiftUI includes basic animations with predefined or custom easing, as well as spring and fluid animations. You can adjust an animation’s speed, set a delay before an animation starts, or specify that it repeats.

<!–-break-–>

We will use the following code to test our animation.

```swift
struct ViewAnimationExample: View {
   
  @State private var showChanges = true
  @State private var degrees = 0.0
   
  var body: some View {
    VStack{
      Rectangle().foregroundColor(.blue).frame(width: 100, height: 100, alignment: .center).padding().rotationEffect(.degrees(degrees))
       
      Button(action: {
        self.showChanges.toggle()
        self.degrees += 45
      }) {
        Text("Start animation")
      }
        Circle().foregroundColor(.red).frame(width: 100, height: 100, alignment: .center).scaleEffect(showChanges ? 0.5 : 1)
    }
  }
}
```
We are going to add some animation by using animation(_:) modifier. We will turn on animation for the Rectangle rotation by adding animation(.spring()) and scaling the circle by using animation(.spring()). Anytime when we use the animation(_:) modifier on a view, SwiftUI animates any changes to the animatable properties of the view, a view’s color, opacity, rotation, size, and other properties are all animatable.

```swift
struct ViewAnimationExample: View {
   
  @State private var showChanges = true
  @State private var degrees = 0.0
   
  var body: some View {
    VStack{
      Rectangle().foregroundColor(.blue).frame(width: 100, height: 100, alignment: .center).padding().rotationEffect(.degrees(degrees)).animation(.spring())
       
      Button(action: {
        self.showChanges.toggle()
        self.degrees += 45
      }) {
        Text("Start animation")
      }
        Circle().foregroundColor(.red).frame(width: 100, height: 100, alignment: .center).scaleEffect(showChanges ? 0.5 : 1).animation(.linear)
    }
  }
}
```
