---
layout: post
title: "SwiftUI: Xcode Previews"
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: orange
published: true
---

Xcode Previews is a new feature of Xcode that allows you to minimize the amount of time you spend building and running and configuring your views to verify the changes that you are making.
{: .lead}
<!–-break-–>
    
## How does it work?

Since Xcode knows what view and what file you are currently working on, it compiles, builds, and runs just that file, separate from the rest of your application, and then inject that implementation back into your application using Swift's dynamic replacement feature. And because the amount of code that needs to be recompiled for every change is significantly smaller than the entirety of the rest of your application, Xcode can continuously and repeatedly do this for every modification you make.

## Good to know

For changes that involve only the literal values, like strings or numbers, the compilation is not required.

## How does Xcode know what to show you?

When you create a new SwiftUI View, Xcode will provide you with everything you need. But in other cases, you will have to create something similar to the below code.
```swift
import SwiftUI

//1
struct ExmpleView: View {
   
  var name: String
   
  var body: some View { //2
    Text("Hello \(name)!")
  }
}


struct ExmpleView_Previews: PreviewProvider { //3
  static var previews: some View { 
    ExmpleView(name: "Peter") //4
  }
}
```

1. Implementing our Example view.
2. [Click here for more info about **opaque return types** and **some** keyword.](https://dreamcraft.io/posts/opaque-return-return-types)
3. Implementing a small type that conforms to a PreviewProvider protocol, which is a part of a SwiftUI framework.
4. You are telling Xcode what view to preview and how to configure the data.


## Tip

Sometimes Xcode Previews stop when you make a mistake. Just press Opt-Cmd-P to make it resume.
