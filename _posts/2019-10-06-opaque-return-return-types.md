---
layout: post
title: "Opaque Return Types."
tags:
  - Swift Evolution
  - Swift
hero: https://source.unsplash.com/collection/145103/
overlay: blue
published: true
---

An opaque return type is used to return a value in functions or methods without providing a concrete type. The opaque return type describes return value in terms of protocols its supports. In the code below, we can see that SwiftUI uses opaque return types inside its View protocol that returns some View in the body property.
{: .lead}
<!–-break-–>

```swift

import SwiftUI
struct ContactsList: View {
     var body: some View {  // <-Here
        Text("Hello!")
  }
}
```

Hiding type information is useful at boundaries between a module and code that calls into the module because the underlying type of the return value can remain private. 
```swift

protocol Fruit {
  func name()->String
}

struct Apple: Fruit{
  func name() -> String {
    return "Apple"
  }
}

struct Peach: Fruit {
  func name() -> String {
    return "Peach"
  }
}

func getFruit() -> some Fruit{
  Apple()
}
```
Whoever calls that function knows it will return some sort of Fruit but doesn't know precisely what. Unlike returning a value whose type is a protocol type, opaque types preserve type identity—the compiler has access to the type information, but clients of the module don't. We might think that we can return a different type of concrete value.
```swift

func getFruit() -> some Fruit{
  Bool.random() ? Peach() : Apple()
}

Compiler Error: Cannot convert return expression of type 'Peach' to return type 'some Fruit'
```

The compiler will raise a build time error if you are trying to return different concrete type for opaque return value.


##  More about Opaque return type

[Swift.org - Opaque Types][https://docs.swift.org/swift-book/LanguageGuide/OpaqueTypes.html]


##  Availability  

Available from Swift 5.1
