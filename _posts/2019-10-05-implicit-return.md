---
layout: post
title: "Single-expression functions and implicit return keyword."
tags:
  - Swift Evolution
  - Swift
hero: https://source.unsplash.com/collection/145103/
overlay: purple
published: true
---

Swift provides a pleasant shorthand for short closures: if a closure contains just a single expression, the return keyword is implicit. So in the following example, learn1 and learn2 will be the same.
{: .lead}
<!–-break-–>
<pre><code>
let learn1= ["D", "R", "E", "A", "M"].map { $0.lowercased() }
let learn2 = ["D", "R", "E", "A", "M"].map { return $0.lowercased() }
</code></pre>

Swift Evolution proposal SE-0255  extended this behavior on functions and computed properties. Wich means that in single-expression functions, the return keyword is implicit.

In the following example, two implementations act in the same way.
<pre><code>
struct PersonInfo: View {
    var body: some View {
        return Text("Loading...")
    }
}

struct PersonInfo: View {
    var body: some View {
        Text("Loading...")
    }
}
</code></pre>


##  Availability  

Available from Swift 5.1
