---
layout: post
title: "SwiftUI: How to compute one alignment in terms of other alignments"
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
In this post, we will discuss how to compute one alignment in terms of other alignments. In the following example, we have two texts and one image. <!–-break-–>

<img src="https://dreamcraft.io/assets/img/alignments/defaultPiano.png" style="width: 50%; height: 50%"/>​

```swift
struct AlignmentExample: View {
    var body: some View {
        HStack(alignment: .lastTextBaseline){
            Text("Black")
            Image("piano")
            Text("Piano")
        }
    }
}
```

We can see that our stack has the alignment set to ".lastTextBaseline" which will align the image bottom to last text baseline of the texts. But what if might want to move our piano lower by 10 points.
> iOS screen coordinates are in UI points. One point is one pixel on the original-density screens, and one point is two ore more pixels on the high resolution/retina displays.

We can do that by using the alignment guide API.

<img src="https://dreamcraft.io/assets/img/alignments/fixedPiano.png" style="width: 50%; height: 50%"/>​

```swift
sstruct AlignmentExample: View {
    var body: some View {
        HStack(alignment: .lastTextBaseline){
            Text("Black")
            Image("piano").alignmentGuide(.lastTextBaseline){ d in d[.bottom] - 10} //1
            Text("Piano")
        }
    }
}
```
1. Here we tell SwiftUI how to compute a last text baseline for the image in terms of its bottom alignment. And yes, we can do that with other alignments.
