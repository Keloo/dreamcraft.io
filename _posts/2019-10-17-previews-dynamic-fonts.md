---
layout: post
title: "Xcode Previews: How to make 25% of your users happier, or how to preview your app with dynamic font sizes."
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
  - happy users
  - dynamic font
  - preview dynamic font
  - dynamic font sizes
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: purple
published: true
---
According to a few researches ( in example [PSPDFKit research](https://twitter.com/steipete/status/1052589183225815040?lang=en) and [@bloom_life](https://twitter.com/Apokrupto/status/1098917839073931264), more than a quarter of your users might choose non-default text size.When we build our app, it is essential to take advantage of dynamic font sizes.
<!–-break-–>


```swift
struct ExampleView: View {
    var body: some View {
        VStack{
            Color.green
            Text("Dreamcraft.io").foregroundColor(.black).fontWeight(.black)
            Color.blue
        }
    }
}
```
While writing our app, we might want to take a look at how our view will look like when the user changes the dynamic font size to extra-large.
Because the preview of API is part of SwiftUI, we can take advantage of all of SwiftUI when we are writing our previews. In particular, in this case, we can use the environment modifier and specify the value for the `sizeCategory` keypath to be `.accessibilityLarge`.

```swift
 struct Example_Previews: PreviewProvider {
   static var previews: some View {
     ExampleView().environment(\.sizeCategory, .accessibilityLarge)
   }
 }
 ```
 We can embed this view in a group, and for each ExampleView specify a different `sizeCategory`, but there is a better way. SwiftUI has the [for each feature](https://dreamcraft.io/posts/model-for-list-swiftui). For each of the content `sizeCategory` cases, we will have a preview, and for each of those cases, we will specify into the environment the value for the size category keypath to be that case.

```swift
struct Example_Previews: PreviewProvider {
  static var previews: some View {
    ForEach(ContentSizeCategory.allCases, id: \.self){ item in
      ExampleView().environment(\.sizeCategory, item)
    }
  }
}
```
