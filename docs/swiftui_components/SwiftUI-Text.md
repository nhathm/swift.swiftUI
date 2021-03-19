---
layout: default
title: Text
parent: SwiftUI's components
nav_order: 2
---
Giống như Label trong UIKit, Text được sinh ra với nhiệm vụ hiển thị dữ liệu dưới dạng String

```swift
struct ContentView: View {
    private let name: String = "Rai"
    
    var body: some View {
        Text("Hello, world! My name is \(name)")
    }
}
```