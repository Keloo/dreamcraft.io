---
layout: post
title: "How to split a string into an array"
tags:
  - string
  - split
  - array
hero: https://source.unsplash.com/collection/145103/
overlay: purple
published: true
---

## How to split a string

You can convert a string to an array of substrings by breaking it up using the components(separatedBy:) method. It can split a string by space, but also by any character set you need.

{: .lead}
<!–-break-–>
## Code example using components(separatedBy:).

let myString = "A1,B2,C3,D4"

let substringsArray = myString.components(separatedBy: ",")

//Result is  ["A1", "B2", "C3", "D4"]

##  Availability  

Available from iOS 7.0
