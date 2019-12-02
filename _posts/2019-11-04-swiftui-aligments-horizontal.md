---
layout: post
title: "SwiftUI: How to align views (horizontal alignments)"
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
  - iphone
  - architecture
  - guide
  - apple
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: purple
published: true
---
Alignments are critical in the building of the UI. In the [previous post](https://dreamcraft.io/posts/swiftui-aligments-vertical), we have covered vertical alignments, but in this one, we will focus on horizontal alignments.<!–-break-–>

In the following example, we have two colors and one text with the background set up.

<img src="https://dreamcraft.io/assets/img/alignments/centerH.png" style="width: 50%; height: 50%"/>​

```swift
struct HorizontalAlignmentExample: View {
    var body: some View {
        VStack{
            Color.red.frame(width: 100, height: 25)
            Text("Hello vertical alignment").font(.headline).foregroundColor(Color.white).background(Color.blue)
            Color.green.frame(width: 250, height: 25)
            }.frame(width: 300, height: 200).background(Color.yellow)
    }
}
```
To demonstrate all alignments, we are going to add an alignment parameter to our VStack:
```swift
struct ExmpleView: View {
    var body: some View {
        VStack(alignment: .center){ //<--- Here
            ....
        }
    }
}
```
## Leading
<img src="https://dreamcraft.io/assets/img/alignments/leading.png" style="width: 50%; height: 50%"/>​
```swift
    HStack(alignment: .leading) {...}
```
## Center
<img src="https://dreamcraft.io/assets/img/alignments/centerH.png" style="width: 50%; height: 50%"/>​
By default, we have a center alignment, and that is why it doesn't differ from our initial example. 
```swift
    VStack(alignment: .center) {...}
```
Is equal to:
```swift
    HStack{...} 
```
## Trailing
<img src="https://dreamcraft.io/assets/img/alignments/trailing.png" style="width: 50%; height: 50%"/>​
```swift
    VStack(alignment: .trailing) {...}
```
