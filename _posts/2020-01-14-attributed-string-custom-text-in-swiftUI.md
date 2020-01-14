---
layout: post
title: "SwiftUI: How to simulate NSAttributedString in SwiftUI"
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
  - dreamcraft
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: blue
published: true
---

Since SwiftUI is relatively new, not all of the functionality from UIKit is available there. In the following post, we will reproduce NSAttributedString in two different ways.
First is to wrap an UILabel in UIViewRepresentable, and the second one is to use the native SwiftUI way by combining text views using the plus "+" operator.

<!–-break-–>


### UIViewRepresentable to wrap our UILabel.

The example below shows a basic example of using an UILabel in SwiftUI by creating a struct that conforms to the UIViewRepresentable protocol. [Here you can find more on how to use any UIView subclass in SwiftUI](https://dreamcraft.io/posts/swiftui-use-uikit-view-in-swiftui).

```swift
struct TextWithAttributedString: UIViewRepresentable {
    
    var attributedString:NSMutableAttributedString
    
    func makeUIView(context: Context) -> UILabel {
        let label = UILabel()
        label.numberOfLines = 0
        label.lineBreakMode = .byWordWrapping
        label.autoresizesSubviews = true
        label.autoresizingMask = [.flexibleWidth, .flexibleHeight]
        return label
    }
    
    func updateUIView(_ uiView: UILabel, context: UIViewRepresentableContext<TextWithAttributedString>) {
        uiView.attributedText = attributedString
        
    }
}
```

In our example, we will create a struct that will hold our attributed string. In your real-life application, you will keep that code in your ViewModel.

```swift

struct MyCustomTextModel {
    var myCustomAttributedString: NSMutableAttributedString = {
        let myTestString = "Attributed string"
        let attributedString = NSMutableAttributedString(string: myTestString)
        
        let attributes1 = [NSAttributedString.Key.font: UIFont(name: "Chalkduster", size: 25)!, .foregroundColor: UIColor.orange, NSAttributedString.Key.kern: 10] as [NSAttributedString.Key : Any]
        
        attributedString.addAttributes(attributes1, range: NSRange(location: 0, length: "Attributed ".count))
        
        let attributes2 = [NSAttributedString.Key.font: UIFont(name: "Chalkduster", size: 25)!, .foregroundColor: UIColor.black]

        attributedString.addAttributes(attributes2, range: NSRange(location: "Attributed".count + 1, length: "string".count))

        return attributedString
    }()
}

```

1. To mime the same behavior in SwiftUI as the example above, we will need only a few lines of code.


```swift

struct NSAttributedStringExample: View {
    
    var myCustomAttributedModel = MyCustomTextModel()
    
    var body: some View {
        Form{
            //SwiftUI way using plus "+" operator  // 1.
            Text("Attributed ").foregroundColor(.orange).kerning(10).font(.custom("Chalkduster", size: 25))
            + Text("string").foregroundColor(.black).font(.custom("Chalkduster", size: 25))

            //Wrapping an UILabel
            TextWithAttributedString(attributedString: myCustomAttributedModel.myCustomAttributedString)
        }
    }
}

//Previewing our code
struct NSAttributedStringExample_Previews: PreviewProvider {
    static var previews: some View {
        NSAttributedStringExample()
    }
}
```
