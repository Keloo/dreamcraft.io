---
layout: post
title: "SwiftUI: About gradients and how to apply a gradient on a shape or view."
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: red
published: true
---
Gradients conform to view protocol, which means that we can drow them as any other view. SwiftUI provides us with three types of gradients: linear,  angular, and radial. Each type requires a few different parameters. 
<!–-break-–>
Each of the mentioned gradients will require us to pass a spectrum of colors that we want to show. We can do that with a gradient. Represented as an array of colors, and yes we can pass as many colors as we wish to, SwiftUI will space them equally.
```swift
let spectrum = Gradient(colors: [.red, .green, .blue])
```
In the following example, we will see all gradients side by side. I recommend you experiment with parameters so you can better understand each of them.
<img src="https://dreamcraft.io/assets/img/gradients/example.png" style="width: 60%; height: 60%"/>​
```swift
struct SpectrumExample: View {
    var body: some View {
        
        let spectrum = Gradient(colors: [.red, .green, .blue]) //1
        
        let linearGradient = LinearGradient(gradient: spectrum, startPoint: UnitPoint.leading, endPoint: UnitPoint.trailing) //2
        
        let angularGradient = AngularGradient(gradient: spectrum, center: UnitPoint.center, angle: .degrees(0)) //3
        
        let radialGradient = RadialGradient(gradient: spectrum, center: UnitPoint.center, startRadius: 0, endRadius: 190) //4
        
        return VStack{
            Circle().fill(linearGradient)
            Circle().fill(angularGradient)
            Circle().fill(radialGradient)
            Text("Text with cool background").font(.headline).foregroundColor(.white).padding().background(linearGradient) //5
        }
    }
}
```

1. Color spectrum with three colors, red, green, and blue. We will use the same colors for all gradients types.
2. Linear Gradient 
3. Angular Gradient
4. Radial Gradient
5. Text example with the linear gradient as the background.

Use the following image as a guide for UnitPoint parameters.

<img src="https://dreamcraft.io/assets/img/gradients/unitPoint.png" style="width: 60%; height: 60%"/>​
