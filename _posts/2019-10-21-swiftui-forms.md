---
layout: post
title: "SwiftUI: Forms"
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
  - forms
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: orange
published: true
---

Form signIn/Up views to everything that requires you to enter some information, SwiftUI refers to this as a `Form`. A `Form` is a container just like [VStack](https://dreamcraft.io/posts/stack-swiftui), but one built specifically for building these sections of heterogeneous controls, giving the overall result a standard look and feel no matter what the platform.
<!–-break-–>
We can create a form just by wrapping any primitive view in our `Form` container.
```swift
struct ExampleView: View {
  var body: some View {
    Form{
      Text("Dream comes true")
    }
  }
}
```
This one will appear as it were inside a table view cell with a `UITableViewStyleGrouped`, but if this Text were wrapped in a `VStack`, it would stay centered. As a conclusion `Forms` are scrolling lists of views like buttons, colors, images, texts. We can see that by trying the following example.

```swift
struct ExampleView: View {
  var body: some View {
    Form{
      ForEach(0 ..< 20) { item in
        Text("Dream comes true")
      }
    }
  }
}
```
