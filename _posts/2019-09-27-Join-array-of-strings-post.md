---
layout: post
title: "Join an array of strings into a single string"
tags:
  - string
  - merge
  - How to
  - Swift Evolution
  - opaqe type
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
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: orange
published: true
---

## How to join an array of strings into a single string

If you have an array of strings and want to merge all the elements into a single string, you should use joined().
{: .lead}
<!–-break-–>
## Code example using joined().

```swift
let elements = ["A1", "B2", "C3", "D4"]

let joinedElements = elements.joined()

//Result is "A1B2C3D4"
```

## Join strings together using a separator

Also, you can call joined with the parameter joined(separator: "-#-"), it will just stitch the strings together with specified separator.

## Code example using joined(separator:).

```swift
let elements = ["A1", "B2", "C3", "D4"]

let joinedElements = elements.joined(separator: "+")

//Result is "A1+B2+C3+D4"
```

##  Availability  

Available from iOS 7.0
