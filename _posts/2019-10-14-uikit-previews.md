---
layout: post
title: "Preview your UIView (UIKit) with Xcode Previews."
tags:
  - Swift Evolution
  - SwiftUI
  - How to
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: blue
published: true
---
Since I played with Xcode Previews and SwiftUI, I was impressed how great those two works together. But once I opened my existing project that was written with UIKit(even if I am using [code injection](https://github.com/johnno1962/InjectionIII) to optimize my workflow). I was wondering if Xcode Previews can do the same excellent job with my existing code. After a little research, the answer was yes.<!–-break-–>

For that purpose, we will use an existing project ["GitFeed"](https://github.com/dresetnic/GitFeed) We are going to put our cell form the feed in the Xcode Previews.
<img src="https://dreamcraft.io/assets/img/uikitpreview/feed.png" style="width: 50%; height: 50%"/>​
It turns out that that cell from feed was written as a UITableViewCell called GFFeedTableViewCell.
Previews are just code, so we absolutely could go ahead and create the preview right alongside this UITableViewCell in this file. 

First, we will need to import SwiftUI since the Previews API is part of that framework. To view our GFFeedTableViewCell displayed in the Canvas, we will need to create a new type (FeedTableViewCellPreview) that conforms to the preview provider protocol.
Now the preview provider protocol has a single requirement that you must implement, namely, the Static Previews Property.

```swift
import SwiftUI

struct FeedTableViewCellPreview: PreviewProvider {

  // MARK: PreviewProvider
   
  static var previews: some View{
    FeedTableViewCellPreview() //1
  }
}
```

We'll return an instance of the type that conforms to UIViewRepresentable(we will add that in the next steps), namely, FeedTableViewCellPreview.

SwiftUI has rich support for embedding UIViews into SwiftViews in the form of Representable. In our case, we want to add a conformant to UIViewRepresentable. [More about UIViewRepresentable and how to use any UIView in SwiftUI.](https://dreamcraft.io/posts/swiftui-uiview)

 Now for our purposes, the UIView representable protocol has three requirements that we need to implement. 

 1. Specify the type of UIView that's being represented. In our case, that's the GFFeedTableViewCell.
 
 2. Describe how to create GFFeedTableViewCell.
 
 3. We need to implement is updateUIView. In our case, we want to create a preview, so I am going to leave this implementation blank.
 
 ```swift
 import SwiftUI

 struct FeedTableViewCellPreview: PreviewProvider, UIViewRepresentable {

     // MARK: PreviewProvider
     
     static var previews: some View{
         FeedTableViewCellPreview()
     }
     
     //MARK: UIViewRepresentable
     typealias UIViewType = GFFeedTableViewCell
     
     func makeUIView(context: UIViewRepresentableContext<FeedTableViewCellPreview>) -> GFFeedTableViewCell {
         let cell = GFFeedTableViewCell()
         cell.setupWith(GFEvent.example)
         return cell
     }
     
     func updateUIView(_ uiView: GFFeedTableViewCell, context: UIViewRepresentableContext<FeedTableViewCellPreview>) {
     }
 }
 ```
 
With just those few lines of code, you can see a preview for your UIView in Xcode.

<img src="https://dreamcraft.io/assets/img/uikitpreview/cellpreview.png" style="width: 50%; height: 50%"/>​

