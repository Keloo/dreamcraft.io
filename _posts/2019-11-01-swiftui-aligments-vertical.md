---
layout: post
title: "SwiftUI: How to align views (vertical alignments)"
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: purple
published: true
---
Alignments are critical in the building of the UI. While SwiftUI spacing between UI elements follows the Human Interface Guidelines by Apple out of the box,  some  UI elements need some adjustments to they positing regarding other UI elements. In this post, we will cover the basics of alignments. We have two types of alignments Horizontal and Vertical.<!–-break-–>

## Vertical Alignments.
There are five types of vertical alignments, and we will cover each one by using the following example:
<img src="https://dreamcraft.io/assets/img/alignments/center.png" style="width: 50%; height: 50%"/>​
```swift
struct ExmpleView: View {
    var body: some View {
        HStack{
            Color.yellow.frame(width: 50, height: 10)
            Text("Headline text!").font(.headline)
            Color.red.frame(width: 50, height: 50)
            Text("footnote text!").font(.footnote)
            Color.green.frame(width: 50, height: 100)
            Text("Caption text!").font(.caption)
            Color.blue.frame(width: 50, height: 200)
        }
    }
}
```
To demonstrate all alignments, we are going to add an alignment parameter to our HStack:
```swift
struct ExmpleView: View {
    var body: some View {
        HStack(alignment: .center){ //<--- Here
            ....
        }
    }
}
```
## Top
<img src="https://dreamcraft.io/assets/img/alignments/top.png" style="width: 50%; height: 50%"/>​
```swift
    HStack(alignment: .top) {...}
```
## Center
<img src="https://dreamcraft.io/assets/img/alignments/center.png" style="width: 50%; height: 50%"/>​
By default, we have a center alignment, and that is why it doesn't differ from our initial example. 
```swift
    HStack(alignment: .center) {...}
```
Is equal to:
```swift
    HStack{...} 
```
## Bottom
<img src="https://dreamcraft.io/assets/img/alignments/bottom.png" style="width: 50%; height: 50%"/>​
```swift
    HStack(alignment: .bottom) {...}
```
## Last Text Baseline
<img src="https://dreamcraft.io/assets/img/alignments/lastTextBaseline.png" style="width: 50%; height: 50%"/>​
In our example, we have Text in our HStack, but if we haven't got one, all views will align as we would pass **.bottom** alignment. 
```swift
    HStack(alignment: .lastTextBaseline) {...}
```
## First Text Baseline
<img src="https://dreamcraft.io/assets/img/alignments/firstTextBaseline.png" style="width: 50%; height: 50%"/>​
As with the last text baseline, if we haven't got ani text in our HStack, then all views will align as we were passed **.bottom** alignment. 
```swift
    HStack(alignment: .firstTextBaseline) {...}
```
