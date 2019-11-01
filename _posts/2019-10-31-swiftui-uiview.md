---
layout: post
title: "SwiftUI: How to use any UIView in SwiftUI"
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: orange
published: true
---

Even if SwiftUI has a lot of available UI elements that we can use to build our app, they're a lot of missing UI elements from UIKit and a lot of open-source UI elements that we might want to use in our projects.<!–-break-–>  Luckily SwiftUI let us do that by simply creating a struct that conforms to UIViewRepresentable protocol. At the time of writing this post  TextField().lineLimit(nil)  doesn't allow me to mimic the UITextView behavior, so we are going to fix that.

```swift
struct MultilineTextView: UIViewRepresentable { //1
    @Binding var text: String //2

    func makeUIView(context: Context) -> UITextView { //3
        let view = UITextView()
        view.isUserInteractionEnabled = true
        view.isEditable = true
        return view
    }

    func updateUIView(_ uiView: UITextView, context: Context) { //4
        uiView.text = text
    }
}

struct ExampleView: View {
    @State var contents: String = "Our text 🔥";
    
    var body: some View {
        VStack() {
            MultilineTextView(text: $contents)
        }
    }
}
```

1 Creating a MultilineTextView struct that conforms to `UIViewRepresentable` protocol and implementing its methods. Specifically, **makeUIView**(3) and **updateUIView**(4) methods that allow us to create and update our UIView subclass.

2 We pass text to our UITextView through our[ `@Binding` property](https://dreamcraft.io/posts/swiftui-binding-wrapper). [You can find more about @Binding here.](https://dreamcraft.io/posts/swiftui-binding-wrapper)


