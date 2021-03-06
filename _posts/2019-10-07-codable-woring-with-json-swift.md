---
layout: post
title: "Codable - converting between JSON and Swift types"
tags:
  - Swift Evolution
  - decode json
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
  - json
  - codable
  - how to 
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: black
published: true
---

Codable API was introduced in Swift 4.0, which brought an easy way to convert between swift data types and JSON. Under the hood, it enables us to leverage the compiler to generate a part of the code needed to decode/encode from/to from a serialized format like JSON. 
{: .lead}
<!–-break-–>

Let's decode the following json:
```swift
let jsonInput = """
[
  {
    "name": "Apple",
    "family": "Rosaceae"
  },
  {
    "name": "Peach",
    "family": "Rosaceae"
  }
]
"""
```
To encode and decode a custom type, we need to make it **Codable**. The simplest way to make a type codable is to declare its properties using types that are already Codable (String, Int, Double, and others). Array, Dictionary, Optional are Codable if they contain Codable types. 
```swift
struct Fruit: Codable{
  var name: String
  var family: String
}
//1
let data = Data(jsonInput.utf8) 
//2
let decoder = JSONDecoder()
//3
guard let decoded = try? decoder.decode([Fruit].self, from: data) else {
  fatalError("Failed to decode data.")
}
//4
print(decodedFruits.first!.name)
```

1. Converting jsonInput do Data type since Codable decoder requires it.
2. Initializing decoder
3. We are decoding here an array of fruits(as mentioned before, Array is Codable since it contains our Codable type Fruit ).
4. The result is "Apple."

## Different key names problem.
The example above worked since JSON format matched our  Fruit structure. But if our JSON structure is different than our model and we want to keep our Fruit struct, we might need some additional code to make it work.
```swift
let jsonInput = """
[
  {
  "fruitName": "Apple",
  "fruit_family": "Rosaceae"
  },
  {
  "fruitName": "Peach",
  "fruit_family": "Rosaceae"
  }
]
"""


struct Fruit: Codable{
  var name: String
  var family: String
   
//1
  enum CodingKeys: String, CodingKey{
    case name = "fruitName"
    case family = "fruit_family"
  }
}
```
1. We are providing alternative keys by specifying String as the raw-value type for the CodingKeys enumeration. The string you use as a raw value for each enumeration case is the key name that will be used during encoding and decoding.

If we want to omit properties from the CodingKeys enumeration if they won't be present when decoding instances, or if certain properties shouldn't be included in an encoded representation. A property omitted from CodingKeys needs a default value in order for its containing type to receive automatic conformance to Decodable or Codable.
```swift
struct Fruit: Codable{
  var name: String
  var family: String
   
  var omitedValue: String = "Default value text"
   
  enum CodingKeys: String, CodingKey{
    case name = "fruitName"
    case family = "fruit_family"
  }
}
```
Codable is a type alias for the Encodable and Decodable protocols. When you use Codable as a type or a generic constraint, it matches any type that conforms to both protocols. By only having our struct conformed to Codable protocol, we’re now able to encode a Fruit instance into JSON Data by using a JSONEncoder:

```swift
do {
  let fruit = Fruit(name: "Pear", family: "Rosaceae")
  let encoder = JSONEncoder()
  let data = try encoder.encode(fruit)
} catch {
  print("Failed to encode data.")
}
```

##  More about Encoding and Decoding

[Apple - Encoding and Decoding Custom Types][appleLink]


##  Availability  

Available from Swift 4.0

[appleLink]:     https://developer.apple.com/documentation/foundation/archives_and_serialization/encoding_and_decoding_custom_types

