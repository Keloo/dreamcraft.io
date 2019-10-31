---
layout: post
title: "SwiftUI: About smaller screens and views prioritization."
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: orange
published: true
---

SwiftUI is a powerful framework that allows you to write UI for different screen sizes.  But even if we write our app only for iOS, we might find ourselves having our UI shrunk on smaller devices. For such cases, SwiftUI lets us decide what view is more important than another.<!–-break-–> 

```swift
struct ExampleView: View {
    
    var body: some View {
        Form{
            HStack {
                Text("Important text")
                Color.red
                Text("Additional Text")
            }.lineLimit(1)
        }
    }
}
```

<img src="https://dreamcraft.io/assets/img/priorityPost/broken.png" style="width: 50%; height: 50%"/>​

[Here you can find  how to check that your app looks great on all devices.](https://dreamcraft.io/posts/previews-multiple-devices)

This example shows how the same elements may look different on smaller displays. To fix that, we need to raise the layout priority of our important text view. To define the priority of an element, you can use the `layout priority`. If a UI is displayed on a small screen, items with low priority can automatically be hidden. To define importance, you can pass a Double.

```swift
struct ExampleView: View {
    
    var body: some View {
        Form{
            HStack {
                Text("Important text").layoutPriority(1) //<---Here
                Color.red
                Text("Additional Text")
            }.lineLimit(1)
        }
    }
}
```
<img src="https://dreamcraft.io/assets/img/priorityPost/fixed.png" style="width: 50%; height: 50%"/>​

