---
layout: post
title: "SwiftUI: Available shapes in SwiftUI?"
tags:
  - Swift Evolution
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
  - guide
  - apple
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: pink
published: true
---
In SwiftUI shapes a small 2D pieces that can be used to draw views.
SwiftUI provides us with the following shapes: circle, ellipse, capsule, rectangle, rounded rectangle.
In the following example, we will see an example of each shape.
<!–-break-–>
```swift
struct ShapesExample: View {
    var body: some View {
        VStack {
            Circle()  
                .fill(Color.red)  
                .frame(width: 100, height: 50) //1
            Ellipse()
                .fill(Color.green)
                .frame(width: 100, height: 50) //2
            Capsule()
                .fill(Color.blue)
                .frame(width: 150, height: 50) //3
            Rectangle()
                .fill(Color.yellow)
                .frame(width: 200, height: 100) //4
            RoundedRectangle(cornerRadius: 25, style: .continuous)
                .fill(Color.purple)
                .frame(width: 300, height: 150) //5
        }
    }
}
```
1. A circle centered on the frame of the view containing it. Even if we specified the frame with width equal to 100 and height equal to 50 the circle’s diameter equals the length of the frame rectangle’s smallest edge(height 50).
2. An ellipse aligned inside the frame of the view containing it.
3. A capsule shape aligned inside the frame of the view containing it.
4. Rectangle: A rectangular shape with rounded corners, aligned inside the frame of the view containing it.
5. Rounded rectangle behaves in the same way as rectangle except that you can specify the corner radius and style. While the radius parameter is obvious, the style provides us with two options .circle (Quarter-circle rounded rect corners) and .continuous (Continuous curvature rounded rect corners.)



