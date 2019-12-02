---
layout: post
title: "SwiftUI: The power of alignments or how to align views from different stacks."
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
overlay: red
published: true
---
SwiftUI is a powerful framework that provides us with a lot of built-in stuff, such as support of apple human interface guidelines. But sometimes even if SwiftUI views arrangement follows the apple human interface guidelines, they don't align as our designer may want. 
<!–-break-–>


In this post, we will discuss how to align views from one stack with views from another stack. We will use the following example. Suppose our designer asked us to align the center of the green circle with "green" text.

<img src="https://dreamcraft.io/assets/img/alignments/startFin.png" style="width: 60%; height: 60%"/>​


```swift
struct AlignmentExample: View {
    var body: some View {
        Form{
            HStack{
                VStack{
                    Color.green.clipShape(Circle()).frame(width: 30, height: 30)
                VStack(alignment: .leading){
                    Spacer().frame(height: 20)
                    Text("GREEN").foregroundColor(Color.pink).font(.system(size: 12)).bold()
                    Spacer().frame(height: 8)
                    Text("Avocado Green Smoothie").lineLimit(2).font(.headline)
                    Spacer().frame(height: 15)

                    HStack{
                        VStack(alignment: .leading){
                            Text("2").font(.headline)
                            Text("Servings").foregroundColor(Color.gray)
                        }
                        Spacer()
                        VStack(alignment: .leading){
                            Text("6").font(.headline)
                            Text("Minutes").foregroundColor(Color.gray)
                        }
                    }
                    Spacer().frame(height: 15)
                }.fixedSize()
                Spacer()
            }
        }
    }
}
```
As we see, those two elements circle and text are in two different vertical stacks. To center them, we will need to define our alignment by putting an extension on vertical alignment.

```swift
extension VerticalAlignment{ // 1
    
    private enum MidCircleAndText : AlignmentID {
        static func defaultValue(in context: ViewDimensions) -> CGFloat {
            return context[VerticalAlignment.center]
        }
    }
    static let  midCircleAndText = VerticalAlignment(MidCircleAndText.self) //2
}
```


1. We define an enum conforming to "AlignmentID," which has one requirement, tell SwiftUI how to compute the default value. I defined this default to be center just so that you could see that it's just like defining an alignment guide modifier.
2. We define a static instance of vertical alignment that takes the enum type as its argument.


We can use it to align the stack, explicitly setting it to the center of the circle and of the text. Now the explicit alignment values we've set, they project out through two layers of the nested stack, allowing the outer HStack to align those inner parts.

```swift
struct AlignmentExample: View {
    var body: some View {
        Form{
            HStack(alignment: .midCircleAndText){ //     🔥Here
                VStack{
                    Color.green.clipShape(Circle()).frame(width: 30, height: 30).alignmentGuide(.midCircleAndText){ d in d[VerticalAlignment.center]} //     🔥Here
                }
                VStack(alignment: .leading){
                    Spacer().frame(height: 20)
                    Text("GREEN").foregroundColor(Color.pink).font(.system(size: 12)).bold().alignmentGuide(.midCircleAndText){ d in d[VerticalAlignment.center]}   //     🔥Here
                    Spacer().frame(height: 8)
                    Text("Avocado Green Smoothie").lineLimit(2).font(.headline)
                    Spacer().frame(height: 15)

                    HStack{
                        VStack(alignment: .leading){
                            Text("2").font(.headline)
                            Text("Servings").foregroundColor(Color.gray)
                        }
                        Spacer()
                        VStack(alignment: .leading){
                            Text("6").font(.headline)
                            Text("Minutes").foregroundColor(Color.gray)
                        }
                    }
                    Spacer().frame(height: 15)
                }.fixedSize()
                Spacer()
            }
        }
    }
}
```
