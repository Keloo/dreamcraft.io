---
layout: post
title: "SwiftUI : How to draw borders or strokes in SwiftUI?"
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
  - iphone
  - architecture
  - guide
  - apple
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: blue
published: true
---
SwiftUI provides us with various modifiers for drawing borders on views and shapes. Specifically: stroke, stroke border, and border. At first glance, those modifiers may look identical, but they have different behavior and different places where they can be applied.
 <!–-break-–>
 
 In any image redactor like Photoshop or Sketch, when you add a Stroke (border), you select the position. Outside, Inside, or Center.  In the following image, you may see how those look. 
 <img src="https://dreamcraft.io/assets/img/borders/borderdraw.png" style="width: 50%; height: 50%"/>​
 Outside is where the entire border wraps around the object. Inside is where it sits on the inside and center being half and half.

 
##  For Shapes, use **stroke** or **strokeBorder** modifier.

## Stroke
The stroke modifier draws borders centered(half inside half outside).

```swift
Rectangle()
.stroke(Color.purple, lineWidth: 10)
```

## Stroke Border

Stroke Border draws border inside a shape.

```swift
Rectangle()
.strokeBorder(Color.blue, lineWidth: 10)
```

## For Views, use **border** modifier.

## Border

The border modifier draws borders outside of view.

```swift
Image("piano").border(Color.black)
Image("piano").border(Color.black, width: 3)
```

