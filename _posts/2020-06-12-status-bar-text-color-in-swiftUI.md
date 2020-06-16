---
layout: post
title: "SwiftUI: How to change the status bar text color in SwiftUI?"
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
  - animation
  - architecture
  - guide
  - apple
  - dreamcraft
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: blue
published: true
---

For such purpose, we will need the UIHostingController. UIHostingController is a UIKit view controller that manages a SwiftUI view hierarchy.

<!–-break-–>

First, we will need to create a new UIHostingController. And will specify the desired status bar content color.

```swift

import SwiftUI

class MainHost: UIHostingController<MySwiftUIContentView> {
    override var preferredStatusBarStyle: UIStatusBarStyle{
        return .lightContent
    }
}

struct MySwiftUIContentView: View {
    var body: some View {
        Text("My Swift UI Content View")
    }
}

```
Then we have to update our "scenewillConnectTo" function is SceneDelegate.swift file.  At creation time, specify the SwiftUI view you want to use as the root view for this view controller.

```swift
func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
       
       if let windowScene = scene as? UIWindowScene {
           let window = UIWindow(windowScene: windowScene)
           //This line
           window.rootViewController = MainHost(rootView: MySwiftUIContentView())
           self.window = window
           window.makeKeyAndVisible()
       }
   }
```
