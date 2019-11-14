---
layout: post
title: "SwiftUI : @GestureState property wrapper."
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: purple
published: true
---
**@GestureState**is a property wrapper thot stores states of a view during the performance of a gesture. That's cool, but we can store the state of a view during the performance of a gesture using **@State** property wrapper. <!–-break-–>Fortunately, **@GestureState** comes with an extra feature that updates its data as the gesture changes and implicitly resets state to its default value when the gesture becomes inactive.

In the following example,  we have a translation property with a default value equal to **.zero**. During the drag, we will update the **translation** property, which will trigger SwiftUI to update the circle offset. Translation property will become **.zero** (initial vale) as soon as the drag gesture ends, which will bring the circle back to the center.


```swift
struct GestureStateWrapperExample: View {
    
    @GestureState var translation: CGSize = .zero
    
    var body: some View {
        
        let dragGesture = DragGesture().updating($translation) { (currentState, gestureState, transaction) in
            gestureState = currentState.translation
        }
        
        return Circle()
        .fill(Color.blue)
        .frame(width: 100, height: 100, alignment: .center)
        .offset(translation)
            .gesture(dragGesture).animation(.spring())
    }
}
```

