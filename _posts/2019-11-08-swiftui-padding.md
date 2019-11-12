---
layout: post
title: "SwiftUI : About paddings and how to set size of a padding."
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: orange
published: true
---
Padding allows us to add space around views. We cand do that using the "padding()" modifier. By default, padding will add a default space provided by the system, which conforms to the Apple Human Interface Guidelines. 
<!–-break-–>
```swift
struct PaddingExample: View {
    var body: some View {
        VStack{
        Circle().foregroundColor(.blue).padding() // <--------Here
        }.frame(width: 200, height: 200, alignment: .center).background(Color.red)
    }
}
```
SwiftUI lets us customize that padding in few ways:
1. We can specify in what direction we want to keep our paddings by only passing one of the following options: top, leading, bottom, trailing, all, horizontal, vertical. 

```swift
struct PaddingExample: View {
    var body: some View {
        VStack{
        Circle().foregroundColor(.blue).padding(.leading) // <-- top, leading, bottom, trailing, all, horizontal, vertical 
        }.frame(width: 200, height: 200, alignment: .center).background(Color.red)
    }
}
```
Vertical - will keep top and bottom paddings

Horizontal - will keep leading and trailing paddings


2. Or we can set our padding size:

```swift
 struct PaddingExample: View {
     var body: some View {
         VStack{
             Circle().foregroundColor(.blue).padding(50)
         }.background(Color.red)
     }
 }
```

3. Or even better, we can go and use both parameters by choosing a size and side or sides we want to apply on.

```swift
struct PaddingExample: View {
    var body: some View {
        VStack{
            Circle().foregroundColor(.blue).padding(.leading, 100)
        }.background(Color.red)
    }
}
```
