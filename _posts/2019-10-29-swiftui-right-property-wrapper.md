---
layout: post
title: "SwiftUI: How to use the right property wrapper"
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: red
published: true
---
One of the SwfitUI principles is that every piece of data has a single source of truth. In SwiftUI, we have two options for managing these sources of truth: **@State** or **BindableObject**.<!–-break-–> 

## @State
`@State` is excellent for data that's view local, a value type, managed, allocated, and created by the framework.
 One of the great uses of state might be the **UIButton**. 
 While the user presses the button, it internally goes through a few states. Some of the [button states](https://developer.apple.com/documentation/uikit/uicontrol/state) are: normal, highlighted, selected.
 And what's great about using the state for the button is that when you create a button, you don't need to care about the highlight state. That is data that is truly owned by the button.

## BindableObject
Most of the time, your data is going to live outside SwiftUI. For example, your data might live in a database, and that will probably be represented by something like a BindableObject. BindableObject is excellent for representing external data to SwiftUI. It allows your components to read and write a value without owning it. And this makes it great for reusability.


## Conclusion
  In general, you should prefer immutable access. To decide whether you need @State or a BindableObject, ask yourself if you have a case that's like button? And if you do, `@State` might be a great tool either go with `BindableObject`.
