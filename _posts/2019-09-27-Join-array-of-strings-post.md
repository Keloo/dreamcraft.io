---
layout: post
title: Join an array of strings into a single string
tags:
  - string
  - merge
description: >
How to join an array of strings into a single string
hero: https://images.unsplash.com/photo-1495653797063-114787b77b23
overlay: red
published: true
---

## How to join an array of strings into a single string

If you have an array of strings and want to merge all the elements into a single string, you should use joined().
<!–-break-–>

## Code example

~~~swift

let elements = ["A1", "B2", "C3", "D4"]

let joinedElements = elements.joined()

//Result is "A1B2C3D4"
~~~

<!–-break-–>
Available from iOS 7.0
