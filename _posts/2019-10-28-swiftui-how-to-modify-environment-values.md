---
layout: post
title: "SwiftUI: How to modify Environment values"
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
  - evironment
  - dreamcraft
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: red
published: true
---
Earlier, we have discussed about [`Environment` and how to get predefined values](https://dreamcraft.io/posts/swiftui-environment-wrapper) from it. In this article, we will discuss how to set `Environment` value.<!–-break-–> One important thing to remember is that each view inherits `Environment` from its parent. So if we go to our root view and set all the values that we might need, we will propagate them through our entire app. In the following example, we set font, text alignment, and calendar in the `Environment` of our root view, which will hand our `Environment` to all views from our app.

```swift
class SceneDelegate: UIResponder, UIWindowSceneDelegate {

var window: UIWindow?

func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
    // Create the SwiftUI view that provides the window contents.
    let contentView = ContentView()
        .environment(\.font, .body)
        .environment(\.multilineTextAlignment, .leading)
        .environment(\.calendar, .init(identifier: .buddhist))

    // Use a UIHostingController as window root view controller.
    if let windowScene = scene as? UIWindowScene {
        let window = UIWindow(windowScene: windowScene)
        window.rootViewController = UIHostingController(rootView: contentView)
        self.window = window
        window.makeKeyAndVisible()
    }
}
}
```

For example, if we change **multilineTextAlignment** to **.center** in the `Environment` values in one of our children's views, then all its children's views will have **multilineTextAlignment** in their `Environment` set to **center** while all previous views will have that value set to **leading**.
