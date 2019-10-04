---
layout: post
title: "SwiftUI - Preparing a model for a List."
tags:
  - Identifiable
  - SwiftUI
hero: https://source.unsplash.com/collection/145103/
overlay: red
published: true
---

Lists work with identifiable data. You can make your data identifiable in one of two ways: by passing along with your data a key path to a property that uniquely identifies each element, or by making your data type conform to the Identifiable protocol.

{: .lead}
<!–-break-–>

## Passing a key path to a property that uniquely identifies each element.

<pre><code>
import SwiftUI

struct Contact{
let uid: UUID // unique property
public let firstName: String
public let secondName: String
}

struct ContactsList: View {
    
var contacts:[Contact]
    
var body: some View {
        List {
            ForEach(contacts, id: \.uid) { contact in
                Text("\(contact.secondName) \(contact.firstName)")
            }
        }
    }
}
</code></pre>


## Making your data type conform to the Identifiable protocol

This protocol has only one requirement, which is that conforming types must have a property called **id** that can identify them uniquely.

<pre><code>
import SwiftUI

struct Contact: Identifiable{    
    let id: UUID
    public let firstName: String
    public let secondName: String
}

struct ContactsList: View {

var contacts:[Contact]
    
var body: some View {
        List {
            ForEach(contacts) { contact in
                Text("\(contact.secondName) \(contact.firstName)")
            }
        }
    }
}
</code></pre>


##  Availability  

Available from OSX 10.15, iOS 13, tvOS 13, watchOS 6