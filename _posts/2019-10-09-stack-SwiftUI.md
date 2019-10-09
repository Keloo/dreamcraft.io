---
layout: post
title: "Codable - converting between JSON and Swift types"
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: red
published: true
---

SwiftUI have three stack types that allow you to arrange stack children on three-axis x (**HStack**), y (**VStack**), z (**ZStack**).

{: .lead}
<!–-break-–>

![393x700](https://dreamcraft.io/assets/img/postImages/stackExample.png "Large example image"){:.lead}

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

1. VStack arranges its children (yellow and blue colors) in a vertical line.

2. ZStack overlays its children(purple and green), aligning them in both axes (I added an offset on green color so you can see the purple color behind).

3. HStack arranges its children in a horizontal line (red and black).
