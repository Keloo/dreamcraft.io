---
layout: post
title: "SwiftUI gestures:  How to add gestures in SwiftUI."
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
overlay: orange
published: true
---
SwiftUI gives us an elegant and easy way of working with gestures. At the moment of writing this post, SwiftUI provides us with five gestures:  DragGesture, LongPressGesture, MagnificationGesture, RotationGesture, and TapGesture.
<!–-break-–>

## Drag gesture

In the following example, we will drag a bubble view, and at the end of the drag gesture, we will bring that bubble to its initial place.Also, the drag gesture provides us with minimum distance property, which allows us to set the minimum distance that must be dragged before the gesture starts.

```swift

struct DragGestureExample: View {
    
    @State private var offset: CGSize = .zero
    
    var body: some View {
        
        let dragGesture = DragGesture(minimumDistance: 20).onChanged { (value) in
            self.offset = value.translation
        }.onEnded { _ in
            self.offset = CGSize.zero
        }
        
        return Bubble().offset(offset).gesture(dragGesture).animation(.spring())
    }
}

struct Bubble: View {
    var body: some View {
        
        let gradient = Gradient(colors: [.blue, .white, .purple])
        let angularGradient = AngularGradient(gradient: gradient, center: UnitPoint.trailing, angle: .degrees(0))
        
       return ZStack{
        Circle().stroke(lineWidth: 1)
        Circle().fill(angularGradient)
       }.frame(height: 100)
    }
}
```

## Long press gesture


In the following example, we scale the bubble by 1.4 only after the long press end event. We are using the minimum duration property to specify how much we must wait before the end event is triggered.

```swift
struct LongPressGestureExample: View {
    
    @State private var scale: CGFloat = 1.0
    
    var body: some View {
        
        let longPressGesture = LongPressGesture(minimumDuration: 1).onEnded { value in
            self.scale = 1.4
        }
        
        return Bubble().scaleEffect(scale).gesture(longPressGesture).animation(.spring())
    }
}
```

## Magnification gesture

To test the magnification gesture, we need to pinch with two fingers over the view that support that gesture. 

>If you want to test that gesture in Live Preview or simulator hold option(alt) key.  If you wish to change the center of touches, hold shift while holding option(alt) key.


```swift

struct MagnificationGestureExample: View {
    
    @State private var scale: CGFloat = 1.0
    
    var body: some View {
        
        let magnificationGesture = MagnificationGesture().onChanged { (value) in
            self.scale = value.magnitude
        }
        
        return Bubble().scaleEffect(scale).gesture(magnificationGesture).animation(.linear)
    }
}

```
## Rotation gesture

To test rotation gesture in Simulator or Live Preview, use tip from magnification gesture.

```swift

struct RotationGestureExample: View {
    
    @State private var degrees: Double = 0
    
    var body: some View {
        
        let rotationGesture = RotationGesture().onChanged { (value) in
            self.degrees = value.degrees
        }
        
        return Bubble().rotationEffect(Angle(degrees: degrees)).gesture(rotationGesture)
    }
}

struct Bubble: View {
    var body: some View {
        
        let gradient = Gradient(colors: [.blue, .white, .purple])
        let angularGradient = AngularGradient(gradient: gradient, center: UnitPoint.center, angle: .degrees(0))
        
       return ZStack{
        Circle().stroke(lineWidth: 1)
        Circle().fill(angularGradient)
       }.frame(height: 200)
    }
}

```

## Tap gesture

And the last but not least important gesture, the tap gesture. This one might be one of the most used.

```swift
struct TapGestureExample: View {
    
    @State private var scale: CGFloat = 1
    
    var body: some View {
        
        let tapGesture = TapGesture().onEnded {
            if self.scale == 1 {
                self.scale = 1.5
            } else {
                self.scale = 1
            }
        }
        
        return Bubble().gesture(tapGesture).scaleEffect(self.scale).animation(.easeInOut)
    }
}
```

