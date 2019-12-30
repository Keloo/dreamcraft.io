---
layout: post
title: "SwiftUI Stack views - Views that arranges their children"
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
  - stack
  - arrange views
  - xcode previews
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: red
published: true
---

In SwiftUI stacks are container views. They are declared as a composition of other views serving as their content. Those Content views are declared within a special kind of closer known as a view builder. 
SwiftUI has three stack types that allow you to arrange their views on three-axis x (**HStack**), y (**VStack**), z (**ZStack**).
{: .lead}
<!–-break-–>
<img src="https://dreamcraft.io/assets/img/postImages/stackExample.png" style="width: 25%; height: 25%"/>​
```swift
struct StackExamples: View {
  var body: some View {
    HStack{
    //1
      VStack{
        Color.yellow
        Color.blue
      }
      Spacer()
    //2
      ZStack{
        Color.purple
        Color.green.offset(x: 10, y: 10)
      }
      Spacer()
    //3
      HStack{
        Color.red
        Color.black
      }
    }
  }
}
```

1. **VStack** arranges its children (yellow and blue colors) in a vertical line.

2. **ZStack** overlays its children(purple and green), aligning them in both axes (I added an offset on green color so you can see the purple color behind).

3. **HStack** arranges its children in a horizontal line (red and black).
