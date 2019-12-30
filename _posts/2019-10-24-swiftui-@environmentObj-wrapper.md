---
layout: post
title: "SwiftUI: @EnvironmentObject property wrapper"
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
  - property wrapper
  - @environmentobject
  - environmentobject
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: purple
published: true
---
If we have data that should be shared between multiple views, and all of them should automatically update when data changes, then `@EnvironmentObject` is our way to go.The most crucial advantage of `EnvironmentObject` is that we don't need to pass it to each view that needs it.<!–-break-–> First and most important is that an ancestor view(ExampleView) supplies our data. The following example will help us to understand it easily.

The `EnvironmentObject` (Parameters) that we plan to share through our views should conform to the `ObservableObject` protocol.

```swift
class Parameters: ObservableObject{
    @Published var showColdColor: Bool = false //1
}
```
1.  `@Published` property wrapper augments properties by adding **willSet** observer. [You can read here about @Published](https://dreamcraft.io/posts/swiftui-published-wrapper).

Once we have set up our object, we will create our property in all views that need that data with `@EnvironmentObject` property wrapper without providing a default value.

```swift
struct ExampleView: View {
    
    @EnvironmentObject var parameters: Parameters
    
    var body: some View {
        ZStack {
            if self.parameters.showColdColor {
                Color.blue
            } else   {
                Color.red
            }
            ExtractedView()
        }
    }
}

struct ExtractedView: View {
    
    @EnvironmentObject var parameters: Parameters
    
    var body: some View {
        Button(
            action: { self.parameters.showColdColor.toggle() },
            label: { Text("Change Color").foregroundColor(Color.white) }
        )
    }
}
```
The first question that pops in our mind might be "Cool, but how do we pass our parameters to our views?".
And the answer is simple we inject our `Parameters` into environment and SwiftUI will automatically figure out that it has a Parameters instance in the environment, and will get it to the right place. The following code shows how to pass our Parameters property into ExampleView as an environment object.
 
```swift
struct Example_Previews: PreviewProvider {
    static var previews: some View {
        ExampleView().environmentObject(Parameters())
    }
}
```
