---
layout: post
title: "Join an array of strings into a single string"
tags:
  - string
  - merge
hero: https://images.unsplash.com/photo-1529156069898-49953e39b3ac
overlay: orange
published: true
---

## How to join an array of strings into a single string

If you have an array of strings and want to merge all the elements into a single string, you should use joined().

## Code example using joined().

let elements = ["A1", "B2", "C3", "D4"]

let joinedElements = elements.joined()

//Result is "A1B2C3D4"


## Join strings together using a separator

Also, you can call joined with the parameter joined(separator: "-#-"), it will just stitch the strings together with specified separator.

## Code example using joined(separator:).

let elements = ["A1", "B2", "C3", "D4"]

let joinedElements = elements.joined(separator: "+")

//Result is "A1+B2+C3+D4"


##  Availability  

Available from iOS 7.0
