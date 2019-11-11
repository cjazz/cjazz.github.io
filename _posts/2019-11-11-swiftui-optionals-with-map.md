---
title: "SwiftUI - Map replacing Optionals"
date: 2019-11-11
categories:
  - blog
tags:
  - SwiftUI
  - Optionals
  - Map
---

<span style="font-size:12pt">Continuing on with exploring SwiftUI, below I'll demonstrate how to display a failable (optional) image in a psudo message type app.  Pseudo will take the form of an Xcode Playground</span>


<span style="font-size:12pt">
If you've been using Swift for a while you're accustomed to an Optional which is basically a value that can contain something or nothing.  Normally in Swift using a construct called "If let" which means if this value can be allocated...
 </span>

```swift

let me: String? = "Adam"
if let me2 = me{
  print(me2)
}

```
<span style="font-size:12pt">This works in a typical UIKit application, but in SwiftUI inside of a body of a View, it wont.  You'll get an error stating "Closure containg control flow statement cannot be used with function builder". Reason being, SwiftUI builds views using the ViewBuilder struct, which harnesses a new Swift feature called Function Builders.</span>

<span style="font-size:12pt">At this point in time the way around this is to leverage map.</span>

<span style="font-size:12pt">I won't get into detail on Map, but for reference I'll provide this useful link
[Swift Guide to Map Filter Reduce](https://useyourloaf.com/blog/swift-guide-to-map-filter-reduce/)
</span>

<span style="font-size:12pt">Going back to the original problem of displaying an image if it exists in SwiftUI, have a look at this [Xcode playground](https://github.com/cjazz/Swift-Playgrounds/blob/master/SwiftUI-OptionalsToMapConstruct.playground/Contents.swift), and code below:</span>

```swift

import PlaygroundSupport
import SwiftUI

// Create a listView with a failable image leveraging .map as a replacement to "if let" optional

struct Message: Identifiable {
  var id: UUID
  let message: String
  let imageName: String?

  init(message: String, imageName: String? = nil) {
    self.id = UUID()
    self.message = message
    self.imageName = imageName
  }
}

struct MessageStream: View {
  // simulate two instances of text messages
  let messages: [Message] = [
    Message(message: "You there?"),
    Message(message: "Yes! Here's a neat system image -> ", imageName: "cube.fill"),
    Message(message: "Cool, but I like this one better: ", imageName: "dot.radiowaves.left.and.right")
  ]
  var body: some View {
    List(messages) { msg  in
      HStack {
        
        Text(msg.message)
          .font(.subheadline)
        
        msg.imageName.map { Image(systemName: $0) }
        .padding()
          .foregroundColor(.blue)
      }
    }
  }
}
let msgStream = MessageStream().self
PlaygroundPage.current.liveView = UIHostingController(rootView: msgStream)

```


<span style="font-size:12pt">Here you can see upon constructing the List, I'm iterating thru messages, and populating a horzontal stack (row) with text **AND** the optional image referencing $0</span>

<span style="font-size:12pt">For non Swift developers, this may be a lot to un-pack/comprehend.</span>

<span style="font-size:12pt">If you want to learn more about techniques levaraged in this example, I encourage you to look into:  Swift 4, Swift 5, Swift Closures, SwiftUI - ViewBuilders, Swift Optionals</span>

<span style="font-size:12pt">My next Swift blog will be on the promising new Framework called "Combine" that Apple announced this year at WWDC 2019 [Combine in Practice](https://developer.apple.com/videos/play/wwdc2019/721/)</span>








