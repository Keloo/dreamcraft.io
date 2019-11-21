---
layout: post
title: "SwiftUI: How to use existing UIKit ViewControllers in SwiftUI?"
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: orange
published: true
---
In this post, we will learn how to use existing UIKit ViewControllers in the SwiftUI project. This tutorial will allow you to prepare your UIKit ViewController for Xcode Preview. 
 <!–-break-–>
 SwiftUI provides us with two protocols that will enable us to use existing UIKit code, UIViewRepresentable designated for view, and UIViewControllerRepresentable designated for ViewControllers. For our purpose, we will need the last one. We will do that by simply creating a struct that conforms to the UIViewControllerRepresentable protocol.

```swift
struct FeedViewControllerSwiftUIView: UIViewControllerRepresentable {
   
    typealias UIViewControllerType = FeedViewController
    
    // 1
    func makeUIViewController(context: UIViewControllerRepresentableContext<FeedViewControllerSwiftUIView>) -> FeedViewController { 
        let feedViewController = FeedViewController()
        let _ = FeedModuleInitializer(feedViewController: feedViewController)
        return feedViewController
    }
    
    // 2
    func updateUIViewController(_ uiViewController: FeedViewController, context: UIViewControllerRepresentableContext<FeedViewControllerSwiftUIView>) {
        
    }
}

struct FeedViewControllerSwiftUIView_Previews: PreviewProvider {
    static var previews: some View {
        FeedViewControllerSwiftUIView()
    }
}
```

1. Implementing makeUIViewController - we use that method to create and prepare our ViewController. In our case, we are using VIPER architecture, which means that we also have to use FeedModuleInitializer to chain our VIPER components.

2. Implementing updateUIViewController method that allow us to update our UIViewController subclass(FeedViewController). In our case, we will leave this method empty. 

