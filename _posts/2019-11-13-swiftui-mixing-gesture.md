---
layout: post
title: "SwiftUI gestures: Composing gestures or how do add and handle multiple gestures."
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
overlay: purple
published: true
---
While working with gesture recognizers, we might find ourselves having multiple gestures recognizers on the same view. And for such situations, we need exactly to know how those interact with each other. SwiftUI allows us to handle such cases in three-way: Simultaneous, Sequenced, Exclusive.<!–-break-–>

## Simultaneous
>When you combine gesture modifiers simultaneously, SwiftUI must recognize all subgesture patterns at the same time for it to recognize the combining gesture.

In the following example, we combine rotation gesture with the magnification gesture to work simultaneously, which means that we can simultaneously magnify and rotate our view.

```swift
struct SimultaneouslyGesturesExample: View {
    
    @State private var degrees: Double = 0
    @State private var scale: CGFloat = 1.0
    
    var body: some View {
        
        let magnificationGesture = MagnificationGesture().onChanged { (value) in
            self.scale = value.magnitude
        }.onEnded { _ in
            self.scale = 1.0
        }
        
        let rotationGesture = RotationGesture().onChanged{ (value) in
            self.degrees = value.degrees
        }.onEnded { _ in
            self.degrees = 0
        }
        
        let magnificationAndDragGesture = magnificationGesture.simultaneously(with: rotationGesture)
        
        return GradientCicle().gesture(magnificationAndDragGesture).rotationEffect(Angle(degrees: degrees)).scaleEffect(scale).animation(.easeInOut)
    }
}

struct GradientCicle: View {
        
    var body: some View {
        
        let gradient = Gradient(colors: [.blue, .black, .purple])
        let angularGradient = AngularGradient(gradient: gradient, center: UnitPoint.center, angle: .degrees(0))
        
       return ZStack{
        Circle().stroke(Color.black, lineWidth: 1)
        Circle().fill(angularGradient)
       }.frame(height: 200)
    }
}
```

## Sequenced

>When you sequence gesture modifiers one after the other, SwiftUI must recognize each subgesture in order.

In this example, we are sequence long-press gesture before drag gesture, which means that we are waiting for the long press to finish before we can start our drag gesture. An overlay will appear once long-press finished, which will notify our user that element is selected, and it is ready to be dragged. 

```swift
 struct SequencedComposeExample: View {
     
     @State var viewState = CGSize.zero
     @State var canBeDragged = false
     @State var translation: CGSize = .zero
     
     var body: some View {

         let longTapGesture = LongPressGesture(minimumDuration: 1).onEnded { _ in
             self.canBeDragged = true
         }
         let dragGesture = DragGesture().onChanged { (value) in
             self.translation = value.translation
             self.canBeDragged = true
         }.onEnded { (value) in
             self.viewState.width += value.translation.width
             self.viewState.height += value.translation.height
             self.translation = .zero
             self.canBeDragged = false
         }
         
         let longTapBeforDragGestures = longTapGesture.sequenced(before: dragGesture)
         
         return Circle()
         .fill(Color.blue)
         .overlay(canBeDragged ? Circle().stroke(Color.gray, lineWidth: 2) : nil)
         .frame(width: 100, height: 100, alignment: .center)
         .offset(
             x: viewState.width + translation.width,
             y: viewState.height + translation.height
         )
         .shadow(radius: canBeDragged ? 8 : 0)
         .gesture(longTapBeforDragGestures)
     }
 }
```

## Exclusive

>A pair of gestures where only one can succeed, which gives precedence to the first of the pair.

In our example, if we tap and hold on our circle more than one second and then try to drag, the drag gesture will be ignored. You can play by changing the order of exclusivity so you can better understand how SwiftUI ignores one in favor of exclusive gesture.



```swift

struct ExclusiveComposeExample: View {
    
    @State var viewState = CGSize.zero
    @State var canBeDragged = false
    @State var translation: CGSize = .zero
    
    var body: some View {

        let longTapGesture = LongPressGesture(minimumDuration: 1).onEnded { _ in
            self.canBeDragged = true
        }
        let dragGesture = DragGesture().onChanged { (value) in
            self.translation = value.translation
            self.canBeDragged = false
        }.onEnded { (value) in
            self.viewState.width += value.translation.width
            self.viewState.height += value.translation.height
            self.translation = .zero
        }
        
//        let dragBeforLongTapGestures = dragGesture.exclusively(before: longTapGesture) // Play with those lines
        let dragBeforLongTapGestures = longTapGesture.exclusively(before: dragGesture)

        
        return Circle()
        .fill(Color.blue)
        .overlay(canBeDragged ? Circle().stroke(Color.red, lineWidth: 4) : nil)
        .overlay(canBeDragged ? Circle().stroke(Color.orange, lineWidth: 2) : nil)
        .frame(width: 100, height: 100, alignment: .center)
        .offset(
            x: viewState.width + translation.width,
            y: viewState.height + translation.height
        )
        .shadow(radius: canBeDragged ? 8 : 0)
        .gesture(dragBeforLongTapGestures)
    }
}

```
