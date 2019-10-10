---
layout: post
title: "SwiftUI: Spacers and Dividers"
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: blue
published: true
---

**Spacer** and **divider** are used to separate content. They may have the same purpose, but under the same circumstances, they may behave differently. Let's figure it out.
{: .lead}

## Spacer

A flexible space that expands along the **major axis** of its containing stack layout, or on **both axes** if not contained in a stack.

<img src="https://dreamcraft.io/assets/img/postImages/spacerExample.png" style="width: 25%; height: 25%"/>​
```swift
struct SpacerExample: View {

    var body: some View {
        HStack{
            VStack{
                Color.red
                Spacer()
                Color.green
            }
            HStack{
                Color.red
                Spacer()
                Color.green
            }

        }
    }
}
```
## Divider

A visual element that can be used to separate other content. When contained in a stack, the divider extends across the **minor axis** of the stack, or **horizontally** when not in a stack. In the following example, we might see that he also offer some out of the box view that has a light gray color and height of 1 pixel (if it extends horizontally) or width  (if it extends vertically).

<img src="https://dreamcraft.io/assets/img/postImages/dividerExample.png" style="width: 25%; height: 25%"/>​

```swift
struct DividerExample: View {

    var body: some View {
        HStack{
            VStack{
                Color.orange
                Divider()
                Color.blue
            }
            HStack{
                Color.red
                Divider()
                Color.green
            }
        }
    }
}
```

## Same circumstances, different behaviour.


In the following example, we have a **divider**(between orange and blue) and a **spacer**(between red and green) with a fixed frame and embedded in VStacks. We can see that even with zero width and zero height applied on the divider between orange and blue color, we have a space with height of 10 pixels.

<img src="https://dreamcraft.io/assets/img/postImages/dividerVsSpacer.png" style="width: 25%; height: 25%"/>​
```swift
struct Example: View {

    var body: some View {
        HStack{
            VStack{
                Color.orange
                Divider().frame(width: 0, height: 0, alignment: .center)
                Color.blue
            }
            VStack{
                Color.red
                Spacer().frame(width: 0, height: 0, alignment: .center)
                Color.green
            }
        }
    }
}
```
## Conclusion

As we saw from the previous two examples, spacer and divider do the same job but with few differences. Starting from the way they extend in different circumstances and ending with that extra gray line provided in the divider. In coclusion: as with alcohol, use them responsible.
