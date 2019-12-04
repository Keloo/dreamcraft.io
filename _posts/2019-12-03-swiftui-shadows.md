---
layout: post
title: "SwiftUI: How to draw shadows in SwiftUI?"
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
  - architecture
  - guide
  - apple
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: pink
published: true
---
SwiftUI provides us with a shadow modifier that allows us to draw a shadow around views easily. With that modifier, you can specify a color, radius, and vertical and horizontal offset to position the shadow relative to this view.
 <!–-break-–>
  >>Parameters:
Color: The shadow’s color.
Radius:  The shadow’s size.
X: A horizontal offset you use to position the shadow relative to this view.
Y: A vertical offset you use to position the shadow relative to this view.

In the following example, we have two Texts with shadows. The only difference between those two is that one has the background, and the other has x and y offset.
```swift

struct ShadowExample: View {
    var body: some View {
        VStack() {
            Text("Text")
                .foregroundColor(.white)
                .background(Color.yellow) .padding()
                .padding()
                .shadow(color: Color.blue, radius: 2) // 1

            Text("Text")
                .padding()
                .shadow(color: .black, radius: 2, x: 10, y: 50) // 2
        }
    }
}

```
1. First text shadow with blue color and radius 2, the x and y shadow offsets are both zero.
2. Second text shadow with black color and radius 2, the x shadow offset is ten, and y shadow offsets are 50.

Notice that shadow shapes look different since, in the first case, the shadow was applied around text and background. In the second case, since we have not specified the background color, the shadow repeats the text shape.

