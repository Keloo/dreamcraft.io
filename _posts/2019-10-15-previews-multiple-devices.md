---
layout: post
title: " Xcode Previews: Be sure that your app looks great on all devices."
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: yellow
published: true
---
By default, Xcode Previews will show you view inside the device that was selected as the run destination. After changing the run destination to another device, the canvas will immediately show our view in the selected device. In that tutorial, I will show you how to check all devices without changing the run destination
<!–-break-–>

```swift
struct ExampleView: View {
  var body: some View {
      VStack{
        Color.green
        Text("Dreamcraft.io")
        Color.blue
      }
  }
}

struct Example_Previews: PreviewProvider {
  static var previews: some View {
    ExampleView()
  }
}
```
There is a Previews API provided named **previewDevice**. You pass to that method the name of the device you want to see a preview on. And almost immediately in the canvas, you will see the device displaying your view.
 ```swift
 struct Example_Previews: PreviewProvider {
   static var previews: some View {
     ExampleView().previewDevice("iPhone 7")
   }
 }
 ```
 Preview device method supports the following values:

| iPhone              | iPad                                                     | Watch                                      | Apple Tv   | Mac |
|-------------------|-------------------------------------------|------------------------------------|-------------|------|
| iPhone 7           |iPad mini 4                                           | Apple Watch Series 2 - 38mm |Apple TV  | Mac |
| iPhone 7 Plus   |iPad Air 2                                              |Apple Watch Series 2 - 42mm |Apple TV 4K| |
| iPhone 8           |iPad Pro (9.7-inch)                                |Apple Watch Series 3 - 38mm | Apple TV 4K (at 1080p)| |
|iPhone 8 Plus    |iPad Pro (12.9-inch)                              |Apple Watch Series 3 - 42mm| ||
|iPhone SE         |iPad (5th generation)                             |Apple Watch Series 4 - 40mm|||
|iPhone X            | iPad Pro (12.9-inch) (2nd generation) |Apple Watch Series 4 - 44mm |||
|iPhone Xs          | iPad Pro (10.5-inch)                            |                                                  |||
|iPhone Xs Max  | iPad (6th generation)                           |                                                 |||
|iPhone Xʀ          | iPad Pro (11-inch)                               |                                                  |||
|                          | iPad Pro (12.9-inch) (3rd generation ) |                                                  |||
|                          | iPad mini (5th generation)                   |                                                  |||
|                          |iPad Air (3rd generation)                      |                                                   |||

But again, we need to change the argument to view our ExampleView on different devices. Luckily there is a better way. We can embed this view in a group. Then add two instances of the ExampleView to it, this time calling preview device with iPhone X and iPhone Xʀ. We will see in the canvas a preview for our ExampleView running on three devices.

```swift
struct Example_Previews: PreviewProvider {
  static var previews: some View {
    Group {
      ExampleView().previewDevice("iPhone 7")
      ExampleView().previewDevice("iPhone X")
      ExampleView().previewDevice("iPhone Xʀ")
    }
  }
}
```
