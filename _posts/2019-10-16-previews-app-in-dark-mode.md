---
layout: post
title: " Xcode Previews: How to preview your app in light and dark mode."
tags:
- Swift Evolution
- SwiftUI
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
- preview dark mode
- light and dark
- light and dark mode
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: red
published: true
---
Even for that task, there is an API provided. You change the color scheme by setting the `\.colorScheme` environment value (`.light` or `.dark`), it depends on which one you want to see a preview. And almost immediately in the canvas will display the desired color scheme.
<!–-break-–>

```swift
struct ExampleView: View {
    var body: some View {
            VStack{
                Color.green
                Text("Dreamcraft.io").foregroundColor(.red)
                Color.blue
            }
    }
}

struct Example_Previews: PreviewProvider {
    static var previews: some View {
            ExampleView().environment(\.colorScheme, .dark)
    }
}
```
But we can preview both color schemes by embedding this view in a group. Then add one more instance of the ExampleView to it, this time setting environment color scheme value to light. We will see in the canvas a preview for our ExampleView running in `light` and `dark` modes.

```swift
 struct Example_Previews: PreviewProvider {
     static var previews: some View {
         Group {
             ExampleView().environment(\.colorScheme, .light)
             ExampleView().environment(\.colorScheme, .dark)
         }
     }
 }
 ```
 If you're writing custom drawing code that depends on the current color scheme, you should also consider the `colorSchemeContrast` property. You can specify images and colors in asset catalogs according to either the `light` or `dark` color scheme, as well as standard or increased contrast. The correct image or color displays automatically for the current environment.
